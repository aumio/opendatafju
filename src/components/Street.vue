<template lang="pug">
  #street.full-screen(:class="{ show: shown }")
    img.bg-image(src="@/assets/street.jpg", :style="{ left: position + '%' }")
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
    hide () {
      this.shown = false
    },
    goTo (target) {
      if (target == 'initial') {
        this.position = 0
      } else if (target == 'stray-cat') {
        this.position = -40
      } else if (target == 'caught') {
        this.position = -380
      }
    }
  }
}
</script>

<style lang="scss">
#street {
  overflow: scroll;
  opacity: 0;
  transition: left .5s, opacity 1.5s;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: -1;

  &.show {
    opacity: 1;
    z-index: 1;
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
