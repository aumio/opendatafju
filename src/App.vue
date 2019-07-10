<template lang="pug">
  #app
    intro(ref="intro", @done="next")
    city(ref="city", @done="next")
</template>

<script>
import Intro from '@/components/Intro'
import City from '@/components/City'

export default {
  name: 'app',
  components: {
    Intro, City
  },
  data () {
    return {
      animatorIndex: 0,
      animators: [
        // 'intro',
        'city'
      ]
    }
  },
  mounted () {
    this.playAnimation()
  },
  methods: {
    playAnimation () {
      const ref = this.animators[this.animatorIndex]

      this.$refs[ref].play()
    },
    next () {
      this.animatorIndex++
      this.playAnimation()
    }
  }
}
</script>

<style lang="scss">
#intro, #city {
  opacity: 0;
  transition: all 1s;
  z-index: -1;

  &.show {
    opacity: 1;
    z-index: 1;
  }
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // background: #eee;
  background: rgb(28, 35, 70);
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;

  .full-screen {
    height: 100%;
    width: 100%;
    position: absolute;
  }
}

body {
  background: rgb(19, 65, 91);
}
</style>
