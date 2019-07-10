<template lang="pug">
  #cat(:class="{ show: shown }", :style="{ left, right }")
    img(src="@/assets/cat-walking.gif")
    .os-dialog(:class="{ show: showOs }") {{ osContent }}
</template>

<script>
export default {
  data () {
    return {
      shown: false,
      showOs: false,
      osContent: '(未設定訊息)',
      left: '100px',
      right: 'auto'
    }
  },
  methods: {
    play () {
      this.show()
    },
    show () {
      this.shown = true
    },
    hide () {
      this.shown = false
    },
    setOs (content) {
      this.osContent = content
    },
    toggleOs (show) {
      this.showOs = show
    },
    move (distance) {
      this.left = distance
    }
  }
}
</script>

<style lang="scss">
#cat {
  position: fixed;
  bottom: 0px;
  transition: left 2s, all 1s;
  opacity: 0;
  z-index: 3 !important;

  &.show {
    opacity: 1;
  }

  img {
    height: 250px;
    margin: -43px -84px -54px -41px;
    transform: rotateY(180deg);
  }

  .os-dialog {
    position: absolute;
    top: -90px;
    left: 50%;
    background-color: white;
    padding: 10px 20px;
    border-radius: 10px;
    z-index: 5;
    opacity: 0;
    transition: all 1s;

    &.show {
      opacity: 1;
    }

    &:before, &:after {
      content: '';
      display: inline-block;
      background-color: white;
      border-radius: 50%;
      position: absolute;
    }

    &:before {
      width: 30px;
      height: 15px;
      bottom: -22px;
      left: 30px;
    }

    &:after {
      width: 20px;
      height: 10px;
      bottom: -40px;
      left: 50px;
    }
  }
}
</style>
