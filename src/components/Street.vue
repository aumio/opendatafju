<template lang="pug">
  #street.full-screen(:class="{ show: shown }")
    img.bg-image(src="@/assets/street.jpg", :style="{ left: position + 'px' }")
</template>

<script>
export default {
  data () {
    return {
      shown: false,
      position: 0
    }
  },
  methods: {
    show () {
      this.shown = true
    },
    forward () {
      this.position = -5000
    }
  }
}
</script>

<style lang="scss">
#street {
  overflow: scroll;
  opacity: 0;
  transition: all .5s;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: -1;

  &.show {
    opacity: 1;
    z-index: auto;
  }

  .bg-image {
    height: 100%;
  }

  img {
    position: absolute;
    transition: all 3s;
    z-index: -1;
  }
}
</style>
