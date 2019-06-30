<template lang="pug">
  #intro.full-screen(:class="{ hide: hideAll }")
    .loading
      .loading-mask(:style="{ height: steps[percentage] + '%' }")
      img(src="@/assets/cat-walking-empty.gif")
    h1 STRAY LAB
    p 這是一段流浪貓尋找自我歸處的故事
    p 有些貓、有些狗，甚至是很多人很幸運，從一出生都有著溫暖的家
    p
      | 但願未來，每一隻浪浪，甚至是所有的生物，
      br
      | 有一日都能找到自己的家，與家人相伴
    button(:class="{ hide: hideButton }", @click="hideAll = true;$emit('done')") START
</template>

<script>
export default {
  data () {
    return {
      percentage: 0,
      steps: [10, 30, 50, 80, 100],
      hideAll: false,
      hideButton: true
    }
  },
  mounted () {
    let self = this
    let timer = setInterval(() => {
      if (self.percentage < self.steps.length) {
        self.percentage++
      }
      if (self.percentage === self.steps.length) {
        // self.$emit('done')
        clearInterval(timer)
        self.hideButton = false
      }
    }, 1000)
  }
}
</script>

<style lang="scss">
#intro {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
  transition: all .5s;

  &.hide {
    opacity: 0;
  }

  .loading {
    display: inline-block;
    background: purple;
    position: relative;

    .loading-mask {
      width: 100%;
      position: absolute;
      bottom: 0;
      transition: all .5s;
      background: white;
    }

    img {
      height: 150px;
      margin: -25px -51px -34px -23px;
      transform: rotateY(180deg);
    }
  }

  h1 {
    margin-top: 50px;
  }

  p {
    width: 500px;
    max-width: 100%;
    padding: 0 30px;
    text-align: center;
    margin: 5px 0;
  }

  button {
    padding: 15px 70px;
    border: 1px solid white;
    background: transparent;
    color: white;
    margin-top: 50px;
    font-size: 20px;
    cursor: pointer;
    opacity: 1;
    transition: all .5s;

    &.hide {
      opacity: 0;
    }

    &:hover {
      background: white;
      color: black;
    }
  }
}
</style>
