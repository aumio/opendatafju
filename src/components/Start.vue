<template lang="pug">
  #start.full-screen(:class="{ show: shown }")
</template>

<script>
export default {
  data () {
    return {
      shown: false,
      expanded: false
    }
  },
  mounted () {
    //
  },
  methods: {
    play () {
      this.shown = true
    }
  }
}
</script>

<style lang="scss">
#start {
  opacity: 0;
  transition: all .5s;
  transition-delay: .5s;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  &.show {
    opacity: 1;
  }


}
</style>
