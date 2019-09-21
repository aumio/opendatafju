<template lang="pug">
  .data-modal(:class="{ show: showSelf }")
    .data-title 資料標題
    .data-question 資料內容
    .data-actions
      .action-ok(@click="hide(); $emit('ended')") 我知道了
</template>

<script>
export default {
  // props: {
  //   situation: {
  //     type: Object,
  //     required: true
  //   }
  // },
  data () {
    return {
      showSelf: false
    }
  },
  methods: {
    show () {
      this.showSelf = true
    },
    hide () {
      this.showSelf = false
    }
  }
}
</script>

<style lang="scss">
.data-modal {
  position: fixed;
  top: 50px;
  left: 100px;
  right: 100px;
  bottom: 50px;
  padding: 30px;
  background-color: rgba(255, 255, 255, 0.8);
  color: white;
  border-radius: 10px;
  transition: all 1s;
  opacity: 0;
  pointer-events: none;
  z-index: 5 !important;
  display: flex;
  flex-direction: column;
  color: black;

  &.show {
    opacity: 1;
    pointer-events: auto;
  }

  .data-title {
    font-size: 24px;
    margin-bottom: 20px;
  }

  .data-question {
    font-size: 18px;
  }

  .data-actions {
    margin-top: auto;
    display: flex;

    .action-ok {
      width: 100%;
      border-radius: 4px;
      padding: 10px;
      text-align: center;
      font-size: 18px;
      margin: 0 20px;
      transition: all .3s;

      &:hover {
        background-color: black;
        border: 1px solid white;
        color: white;
        cursor: pointer;
      }
    }

    .action-ok {
      background-color: transparent;
      border: 1px solid black;
      color: black;
    }
  }
}
</style>
