<template>
  <div>
    <p>{{ view_message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      view_message: '',
    }
  },
  props: ['message'],
  methods: {
    init: function() {
      this.message_array = [...this.message].map(function(value, index) {
          return {value:value, index:index};
      });
      this.view_message = ''
      for (var i = 0; i < this.message.length; i++) {
        this.view_message += ' '
      }
      this.index = 0
    },

    discript: function () {
      var index = Math.floor(Math.random() * this.message_array.length)

      var character = this.message_array[index]
      this.message_array.splice(index, 1);

      this.view_message = this.view_message.slice(0, character.index) + character.value
        + this.view_message.slice(character.index + 1, this.view_message.length);

      if(this.message_array.length <= 0) {
        this.stop()
      }
    },

    start: function() {
      if (!this.message) {
        return
      }
      this.init()
      let self = this
      this.timer = setInterval(function() {
        self.discript()
      }, 50)
    },

    stop: function() {
      clearInterval(this.timer);
    },
  },
  mounted() {
    this.start();
  },
}
</script>
