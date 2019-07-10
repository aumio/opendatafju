<template lang="pug">
  #cat(:class="{ show }")
    img(src="@/assets/cat-walking.gif")
    .os-dialog(:class="{ show: showOs }") 媽媽在哪裡...？
</template>

<script>
export default {
  data () {
    return {
      show: false,
      showOs: false
    }
  },
  methods: {
    play () {
      this.show = true
    },
    hide () {
      this.show = false
    },
    toggleOs (show) {
      this.showOs = show
    }
  }
}
</script>

<style lang="scss">
#cat {
  position: fixed;
  bottom: 0px;
  left: 100px;
  transition: all 1s;
  opacity: 0;

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
