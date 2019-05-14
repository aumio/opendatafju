<template lang="pug">
  #app
    //- #cat: img(src="@/assets/cat-walking.gif")
    //- #street.full-screen
    //-   img.bg-image(src="@/assets/street.jpg")
    #intro.full-screen
      .loading
        img(src="@/assets/cat-walking-empty.gif")
      h1 STRAY LAB
      p 這是一段流浪貓尋找自我歸處的故事
      p 有些貓、有些狗，甚至是很多人很幸運，從一出生都有著溫暖的家
      p
        | 但願未來，每一隻浪浪，甚至是所有的生物，
        br
        | 有一日都能找到自己的家，與家人相伴
</template>

<script>
export default {
  name: 'app',
  components: {
    // HelloWorld
  }
}
</script>

<style lang="scss">
#intro {
  background: rgb(28, 35, 70);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;

  .loading {
    display: inline-block;
    background: purple;
    position: relative;

    &:before {
      content: '';
      display: block;
      width: 100%;
      position: absolute;
      bottom: 0;
      height: 50%;
      transition: all .3s;
      background: white;
    }

    img {
      height: 150px;
      margin: -25px -51px -34px -23px;
      transform: rotateY(180deg);
    }
  }

  p {
    width: 500px;
    max-width: 100%;
    padding: 0 30px;
    text-align: center;
    margin: 5px 0;
  }
}

#cat {
  position: fixed;
  bottom: 0px;
  left: 100px;

  img {
    height: 250px;
    margin: -43px -84px -54px -41px;
    transform: rotateY(180deg);
  }
}

#street {
  overflow: scroll;

  .bg-image {
    height: 100%;
  }
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #eee;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;

  > .full-screen {
    height: 100%;
    width: 100%;
  }
}

body {
  background: rgb(19, 65, 91);
}
</style>
