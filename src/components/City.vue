<template lang="pug">
  #city(:class="{ show }")
    cat(ref="cat")
    street(ref="street")
    img.stray-cat(src="@/assets/stray-cat.png", :class="{ show: showStrayCat }")
    img.garbage(src="@/assets/garbage.jpg", :class="{ show: showGarbage }")
    .sleeping-cat(src="@/assets/cat-sleeping.png", :class="{ show: showSleepingCat }")
      img.cat(src="@/assets/cat-sleeping.png")
      img.box(src="@/assets/box.png")
      img.z(src="@/assets/z.png")
    .night-overlay(:class="{ show: showNight }")
    img#catched(src="@/assets/womancat.png", :class="{ show: showCatched }")
    situation-modal(ref="situation", :situation="situations[situationIndex]")
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
      showGarbage: false,
      showSleepingCat: false,
      showNight: false,
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
            this.$refs.cat.setOs('媽媽在哪裡...？')
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
            this.$refs.street.hide()
          },
          duration: 1500
        },
        {
          fn: () => {
            this.showGarbage = true
          },
          duration: 1500
        },
        {
          fn: () => {
            this.$refs.cat.setOs('哀...找了那麼久，還是找不到媽媽')
            this.$refs.cat.toggleOs(true)
          },
          duration: 3000
        },
        {
          fn: () => {
            this.situationIndex = 1
            this.$refs.situation.show()
          }
        },
        {
          fn: () => {
            this.$refs.cat.toggleOs(false)
            this.$refs.situation.hide()
          },
          duration: 500
        },
        {
          fn: () => {
            this.$refs.cat.move('60%')
          },
          duration: 2000
        },
        {
          fn: () => {
            this.$refs.cat.hide()
            this.showSleepingCat = true
          },
          duration: 2000
        },
        {
          fn: () => {
            this.showNight = true
          },
          duration: 1500
        }
        // {
        //   fn: () => {
        //     this.$refs.cat.hide()
        //     this.showCatched = true
        //   },
        //   duration: 2000
        // },
        // {
        //   fn: () => {
        //     this.situationIndex = 1
        //     this.$refs.situation.show()
        //   }
        // }
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
          title: '此時已趨近黃昏',
          question: ' (主角)在周遭察看，確認沒什麼特別的危險訊號，決定在一個資源回收站度過今夜。',
          negative: '睡覺',
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

.stray-cat {
  position: fixed;
  left: 612px;
  bottom: 286px;
  transition: all 1s;
  opacity: 0;

  &.show {
    opacity: 1;
  }
}

.garbage {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  height: 100%;
  width: 100%;
  transition: transform 1s, opacity 3s;
  opacity: 0;
  transform: translateX(100%);

  &.show {
    opacity: 1;
    transform: translateX(0);
  }
}

.sleeping-cat {
  position: fixed;
  right: 80%;
  bottom: 0;
  left: 60%;
  transition: all 1s;
  opacity: 0;

  &.show {
    opacity: 1;
  }

  .cat {
    position: absolute;
    bottom: 0;
    left: 20px;
  }

  .box {
    position: absolute;
    bottom: 0;
  }

  .z {
    position: absolute;
    bottom: 100px;
    left: -20px;
  }
}

.night-overlay {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 4;
  background-color: black;
  opacity: 0;
  transition: all 1s;

  &.show {
    opacity: 1;
  }
}

#catched {
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
