<template lang="pug">
  #city(:class="{ show }")
    cat(ref="cat")
    street(ref="street")
    img#stray-cat(src="@/assets/stray-cat.png", :class="{ show: showStrayCat }")
    img#catched(src="@/assets/womancat.png", :class="{ show: showCatched }")
    .dialog
    situation-modal(ref="situation", :situation="currentSituation")
</template>

<script>
import Cat from '@/components/Cat'
import Street from '@/components/Street'
import SituationModal from '@/components/SituationModal'

export default {
  name: 'app',
  components: {
    Cat, Street, SituationModal
  },
  data () {
    return {
      show: false,
      showCatched: false,
      showStrayCat: false,
      showSituation: false,
      animatorIndex: 0,
      animators: [
        {
          fn: () => {
            this.$refs.street.show()
            this.$refs.cat.play()
          },
          duration: 1000
        },
        {
          fn: () => {
            this.$refs.cat.toggleOs(true)
          },
          duration: 3000
        },
        {
          fn: () => {
            this.$refs.cat.toggleOs(false)
          },
          duration: 1000
        },
        {
          fn: () => {
            this.$refs.street.goTo('stray-cat')
          },
          duration: 3000
        },
        {
          fn: () => {
            this.showStrayCat = true
          },
          duration: 1000
        },
        {
          fn: () => {
            this.$refs.situation.show()
          },
        },
        {
          fn: () => {
            this.showStrayCat = false
            this.$refs.situation.hide()
          },
          duration: 1000
        },
        {
          fn: () => {
            this.$refs.street.goTo('caught')
          },
          duration: 3000
        },
        {
          fn: () => {
            this.$refs.cat.hide()
            this.showCatched = true
          },
          duration: 2000
        },
        {
          fn: () => {
            this.situationIndex = 1
            this.$refs.situation.show()
          }
        }
      ],
      situationIndex: 0,
      situations: [
        {
          title: '(主角)抬頭一看，牆壁邊上一隻黑貓向下俯視的自己',
          question: ' 原來是要找媽媽呀...啊有了，聽說另一邊的街口據說有其他流浪貓有在那邊遇到不知道是收容所還是中途之家的志工',
          negative: '好喔，那我去那邊看看',
          negativeCallback: () => { this.next() },
        },
        {
          title: '「可惡，被抓住了，該怎麼辦...」',
          question: ' (主角)很努力的想掙脫，但仍徒勞無功。',
          negative: '放棄掙扎',
          negativeCallback: () => {},
          positive: '張口咬Shelly',
          positiveCallback: () => {}
        }
      ]
    }
  },
  computed: {
    currentSituation () {
      return this.situations[this.situationIndex]
    }
  },
  methods: {
    play () {
      this.show = true
      this.playAnimation()
    },
    playAnimation () {
      const animator = this.animators[this.animatorIndex]

      animator.fn()

      if (animator.duration) {
        setTimeout(this.next, animator.duration)
      }
    },
    next () {
      this.animatorIndex++
      this.playAnimation()
    }
  }
}
</script>

<style lang="scss">
#city * {
  z-index: 2;
}

#stray-cat {
  position: fixed;
  left: 612px;
  bottom: 286px;
  transition: all 1s;
  opacity: 0;

  &.show {
    opacity: 1;
  }
}

img#catched {
  transition: all 1s;
  opacity: 0;
  position: fixed;
  width: 400px;
  bottom: 0;
  right: 10%;

  &.show {
    opacity: 1;
  }
}
</style>
