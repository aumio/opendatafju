<template lang="pug">
  #cat(:class="{ show }"): img(src="@/assets/cat-walking.gif")
</template>

<script>
export default {
  data () {
    return {
      show: false
    }
  },
  methods: {
    play () {
      this.show = true
    },
    hide () {
      this.show = false
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
}
</style>
