<template lang="pug">
  #city(:class="{ show }")
    cat(ref="cat")
    street(ref="street")
    img#catched(src="@/assets/womancat.png", :class="{ show: showCatched }")
    .dialog
    .situation-modal(:class="{ show: showSituation }")
      .situation-title 「可惡，被抓住了，該怎麼辦...」
      .situation-question (主角)很努力的想掙脫，但仍徒勞無功。
      .situation-actions
        .action-negative 放棄掙扎
        .action-positive 張口咬Shelly
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
      expanded: false,
      showCatched: false,
      showSituation: false,
      animatorIndex: 0,
      animators: [
        {
          fn: () => {
            this.$refs.street.show()
            this.$refs.cat.play()
          },
          duration: 3000
        },
        {
          fn: () => {
            this.$refs.street.forward()
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
            this.showSituation = true
          }
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

.circle-mask {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 50%;
  width: 200px;
  height: 200px;
  overflow: hidden;
  // background-color: white;
  // background-image: url("assets/street.jpg");
  transition: all 2s;

  &.expanded {
    width: 100vw;
    height: 100vh;
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
