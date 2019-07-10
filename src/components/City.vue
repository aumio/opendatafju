<template lang="pug">
  #city(:class="{ show }")
    cat(ref="cat")
    street(ref="street")
    img#stray-cat(src="@/assets/stray-cat.png", :class="{ show: showStrayCat }")
    img#catched(src="@/assets/womancat.png", :class="{ show: showCatched }")
    .dialog
    .situation-modal(:class="{ show: showSituation }")
      .situation-title {{ currentSituation.title }}
      .situation-question {{ currentSituation.question }}
      .situation-actions
        .action-negative(v-if="currentSituation.negative", @click="currentSituation.negativeCallback") {{ currentSituation.negative }}
        .action-positive(v-if="currentSituation.positive", @click="currentSituation.positiveCallback") {{ currentSituation.positive }}
</template>

<script>
import Cat from '@/components/Cat'
import Street from '@/components/Street'
import Start from '@/components/Start'

export default {
  name: 'app',
  components: {
    Cat, Street, Start
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
            // this.showStrayCat = true
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
            this.showSituation = true
          },
        },
        {
          fn: () => {
            this.showStrayCat = false
            this.showSituation = false
          },
          duration: 2000
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
            this.showSituation = true
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
          // positive: '好喔，那我去那邊看看',
          potiveCallback: () => {}
        },
        {
          title: '「可惡，被抓住了，該怎麼辦...」',
          question: ' (主角)很努力的想掙脫，但仍徒勞無功。',
          negative: '放棄掙扎',
          negativeCallback: () => {},
          positive: '張口咬Shelly',
          potiveCallback: () => {}
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

.situation-modal {
  position: fixed;
  top: 50px;
  left: 100px;
  right: 100px;
  padding: 30px;
  background-color: rgba(0, 0, 0, .3);
  color: white;
  border-radius: 10px;
  transition: all 1s;
  opacity: 0;

  &.show {
    opacity: 1;
  }

  .situation-title {
    font-size: 24px;
    margin-bottom: 20px;
  }

  .situation-question {
    font-size: 18px;
  }

  .situation-actions {
    margin-top: 40px;
    display: flex;

    .action-positive, .action-negative {
      width: 100%;
      border-radius: 4px;
      padding: 10px;
      text-align: center;
      font-size: 18px;
      margin: 0 20px;
      transition: all .3s;

      &:hover {
        background-color: white;
        border: 1px solid black;
        color: black;
        cursor: pointer;
      }
    }

    .action-positive {
      background-color: orange;
      border: 1px solid transparent;
      color: black;
    }

    .action-negative {
      background-color: transparent;
      border: 1px solid white;
      color: white;
    }
  }
}
</style>
