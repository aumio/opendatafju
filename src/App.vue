<template lang="pug">
  #app
    intro(@done="showStartScreen")
    cat(ref="cat")
    street(ref="street")
    img#catched(src="@/assets/womancat.png", :class="{ show: showCatched }")
    .dialog
    .situation-modal(:class="{ show: showSituation }")
      .situation-title 野生的獸醫出現了！
      .situation-question 要不要逃跑呢？
      .situation-actions
        .action-negative 放棄掙扎
        .action-positive 用力咬一口然後逃跑
</template>

<script>
import Cat from '@/components/Cat'
import Street from '@/components/Street'
import Intro from '@/components/Intro'
import Start from '@/components/Start'

export default {
  name: 'app',
  components: {
    Cat, Street, Intro, Start
  },
  data () {
    return {
      expanded: false,
      showCatched: false,
      showSituation: false
    }
  },
  methods: {
    showStartScreen () {
      this.$refs.street.show()
      this.$refs.cat.play()
      let self = this

      setTimeout(function () {
        self.$refs.street.forward()
      }, 3000)

      setTimeout(function () {
        self.$refs.cat.hide()
        self.showCatched = true
      }, 6000)

      setTimeout(function () {
        self.showSituation = true
      }, 8000)
    }
  }
}
</script>

<style lang="scss">
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

img#catched {
  transition: all 1s;
  opacity: 0;
  position: fixed;
  width: 400px;
  bottom: 0;
  right: 200px;

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
  background-color: rgba(255, 255, 255, .8);
  border-radius: 20px;
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
    margin-top: 20px;
    display: flex;

    .action-positive, .action-negative {
      width: 100%;
      border-radius: 10px;
      padding: 10px;
      text-align: center;
      font-size: 18px;
      margin: 0 20px;
      transition: all .3s;
      border: 1px solid transparent;

      &:hover {
        background-color: white;
        border: 1px solid black;
        color: black;
        cursor: pointer;
      }
    }

    .action-positive {
      background-color: orange;
    }

    .action-negative {
      background-color: gray;
      color: white;
    }
  }
}
</style>
