<template lang="pug">
  .situation-modal(:class="{ show: showSituation }")
    .situation-title {{ situation.title }}
    .situation-question {{ situation.question }}
    .situation-actions
      .action-negative(v-if="situation.negative", @click="situation.negativeCallback") {{ situation.negative }}
      .action-positive(v-if="situation.positive", @click="situation.positiveCallback") {{ situation.positive }}
</template>

<script>
export default {
  props: {
    situation: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      showSituation: false
    }
  },
  methods: {
    show () {
      this.showSituation = true
    },
    hide () {
      this.showSituation = false
    }
  }
}
</script>

<style lang="scss">
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
