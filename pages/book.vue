<template>
  <div class="container">
    <div>
      <span v-on:mouseup="mouseUP()"
        class="wrd"
        >scanning</span
      >
      <span v-on:mouseup="mouseUP()"
        class="wrd"
        >scanning2</span
      >
      <span v-on:mouseup="mouseUP()"
        class="wrd"
        >scanning3</span
      >
      <span
        v-on:mousedown="changeColor($event)"
        v-on:mouseover="changeColor($event)"
        v-on:mouseup="mouseUP()"
        class="wrd"
        :style="btnStyles"
        >scanning</span
      >
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      color: "#b74f59",
      clicked: false
    };
  },
  computed: {
    btnStyles() {
      if (this.clicked) {
        return {
          "background-color": this.color
        };
      }
    }
  },
  methods: {
    changeColor() {
      this.clicked = !this.clicked;
    },
    mouseUP() {
      console.log(window.getSelection().getRangeAt(0).toString());
    }
  }
};
</script>

<style>
.wrd {
  -webkit-user-select: all;
  -webkit-touch-callout: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: all;
  cursor: pointer;
}
/* .wrd:hover {
  background-color: #ad310b;
} */
</style>
