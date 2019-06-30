<template lang="pug">
  #cat(:class="{ hide: isHidden }"): img(src="@/assets/cat-walking.gif")
</template>

<script>
export default {
  data () {
    return {
      isHidden: true
    }
  },
  methods: {
    play () {
      this.isHidden = false
    },
    hide () {
      this.isHidden = true
    }
  }
}
</script>

<style lang="scss">
#cat {
  position: fixed;
  bottom: 0px;
  left: 100px;
  z-index: 1;
  transition: all 1s;

  &.hide {
    opacity: 0;
    z-index: -1;
  }

  img {
    height: 250px;
    margin: -43px -84px -54px -41px;
    transform: rotateY(180deg);
  }
}
</style>
