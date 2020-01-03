<template lang="pug">
  #duel.full-screen
    .shining-overlay(v-if="showOverlay")
    .duel-dog(:class="{ out: !showDog }")
      img.dog(src="@/assets/battle-dog.png", @click="subHp(dog)")
      .dueler-info(@click="addHp(dog)", :class="{ out: !showStatus }")
        .row
          .dueler-name {{ dog.name }}
          .dueler-level Lv.{{ dog.level }}
        .dueler-hp
          span HP
          .hp-bar
            img.bone(src="@/assets/bone.svg", v-for="i in dog.hp")
    .duel-cat(:class="{ out: !showCat }")
      img.cat(src="@/assets/battle-cat.png", @click="subHp(cat)")
      .dueler-info(@click="addHp(cat)", :class="{ out: !showStatus }")
        .row
          .dueler-name {{ cat.name }}
          .dueler-level Lv.{{ cat.level }}
        .dueler-hp
          span HP
          .hp-bar
            img.fish(src="@/assets/fish.svg", v-for="i in cat.hp")
    .narration-dialog(:class="{ out: !showNarration }")
      .narration-text.typewriter(v-if="showNarrationText") {{ narrationText }}
    .action-panel(v-if="showAction")
      ul.action-category(v-if="actionCategory === null")
        li(@click="actionCategory = 'skills'") 攻擊
        li(@click="actionCategory = 'items'") 道具
        li 逃跑
      ul.navigations-list(v-if="actionCategory !== null")
        li(@click="actionCategory = null") < 返回
      ul.skills-list(v-if="actionCategory === 'skills'")
        li 揮抓
        li 貓顫慄
        li 暴怒的鋼鐵尾巴
        li 裝可愛
      ul.items-list(v-if="actionCategory === 'items'")
        li(v-for="(item, index) in items", :key="index", @click="selectedItem = index; showItemDescription = true") {{ item.name }}
    .item-description(v-if="showItemDescription")
      .overlay
      .modal
        .modal-title {{ items[selectedItem].name }}
        .modal-content {{ items[selectedItem].description }}
        .modal-actions
          button.positive(@click="showItemDescription = false") 使用
          button.negative(@click="showItemDescription = false") 取消
</template>

<script>
export default {
  data () {
    return {
      dog: {
        name: 'Dog',
        level: 87,
        hp: 5,
      },
      cat: {
        name: 'Cat',
        level: 30,
        hp: 5,
      },
      showOverlay: true,
      showDog: false,
      showCat: false,
      showStatus: false,
      showNarration: false,
      showNarrationText: false,
      narrationText: '',
      showAction: false,
      actionCategory: null,
      selectedItem: null,
      showItemDescription: false,
      items: [
        {
          name: '阿忠的魚骨',
          description: '讓敵方人物嚇到暫停一回合',
        },
        {
          name: '貓罐頭',
          description: '回復 2 點 HP',
        },
        {
          name: '小玩偶',
          description: '分散敵方注意力，承受一次攻擊',
        },
      ],
      animatorIndex: 0,
      animators: [
        {
          fn: () => {
            //
          },
          duration: 1500
        },
        {
          fn: () => {
            this.showOverlay = false
            this.showDog = true
            this.showCat = true
          },
          duration: 1500
        },
        {
          fn: () => {
            this.showNarration = true
          },
          duration: 500
        },
        {
          fn: () => {
            this.narrationText = '狗狗發起了突襲！'
            this.showNarrationText = true
          },
          duration: 1500
        },
        {
          fn: () => {
            this.showNarrationText = false
            // this.showNarration = false
          },
          duration: 500
        },
        {
          fn: () => {
            this.showStatus = true
            this.showAction = true
          },
          duration: 500
        },
      ],
    }
  },
  mounted () {
    this.play()
  },
  methods: {
    addHp (dueler) {
      if (dueler.hp <= 4) {
        dueler.hp = dueler.hp + 1
      }
    },
    subHp (dueler) {
      if (dueler.hp >= 1) {
        dueler.hp = dueler.hp - 1
      }
    },
    play () {
      // this.show = true
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
    },
  }
}
</script>

<style lang="scss">
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

#duel {
  background-color: #14425c;
  position: relative;

  .duel-dog, .duel-cat {
    position: relative;
    display: inline-block;

    .dueler-info {
      position: absolute;
    }
  }

  .duel-dog:before, .duel-cat:before {
    content: '';
    position: absolute;
    display: block;
    width: 250px;
    height: 70px;
    border-radius: 50%;
    background-color: #bdd9ec;
    border: 4px solid #97aeb8;
  }

  .dueler-info {
    position: absolute;
    background-color: #bdd9ec;
    border: 5px solid #78b9d3;
    border-radius: 10px;
    color: #13415d;
    padding: 15px 40px;
    transition: all 1s;

    &:after {
      content: '';
      display: block;
      margin: 0 -30px;
      height: 20px;
      width: 350px;
      background-color: #78b9d3;
      position: absolute;
      bottom: -22px;
    }

    &.out {
      opacity: 0;
    }

    .row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 20px;
    }

    .dueler-name {
      font-size: 40px;
    }

    .dueler-level {
      font-size: 40px;
    }

    .dueler-hp {
      display: flex;
      align-items: center;
      background-color: #14425c;
      height: 50px;
      border-radius: 25px;
      margin-top: 20px;
      padding: 0 20px;

      span {
        color: white;
        font-size: 36px;
        font-weight: 900;
      }

      .hp-bar {
        display: flex;
        margin-left: 20px;
        width: 180px;

        img {
          transform: rotate(315deg);
          width: 35px;
        }
      }
    }
  }

  .duel-dog {
    position: absolute;
    right: 0;
    transition: all 1s;

    &:before {
      bottom: 85px;
      right: 40px;
    }

    &.out {
      right: 100vw;
    }

    img.dog {
      width: 400px;
      position: relative;
    }

    .dueler-info {
      top: 50px;
      left: 0;
      transform: translateX(-100%);

      &:after {
        transform: skewX(30deg);
        right: 25px;
      }
    }
  }

  .duel-cat {
    position: absolute;
    top: 400px;
    left: 0;
    transition: all 1s;

    &:before {
      bottom: 65px;
      right: 0;
    }

    &.out {
      left: 100vw;
    }

    img.cat {
      width: 400px;
      position: relative;
    }

    .dueler-info {
      bottom: 100px;
      right: -100px;
      transform: translateX(100%);

      &:after {
        transform: skewX(-30deg);
        left: 25px;
      }
    }
  }

  .bone {
    width: 60px;
  }

  .fish {
    width: 60px;
  }

  .narration-dialog {
    transition: all 1s;
    background-color: black;
    color: white;
    position: fixed;
    right: 0;
    bottom: 0;
    left: 0;
    height: 200px;
    padding: 30px 50px;
    font-size: 36px;

    &.out {
      opacity: 0;
    }

    .narration-text {
      //
    }
  }

  .typewriter {
    overflow: hidden; /* Ensures the content is not revealed until the animation */
    // border-right: .15em solid orange; /* The typwriter cursor */
    white-space: nowrap; /* Keeps the content on a single line */
    margin: 0 auto; /* Gives that scrolling effect as the typing happens */
    letter-spacing: .15em; /* Adjust as needed */
    text-align: left;
    display: inline-block;
    // animation:
    //   typing 3.5s steps(40, end),
    //   blink-caret .75s step-end infinite;
    animation:
      typing 3.5s steps(40, end);
  }

  /* The typing effect */
  @keyframes typing {
    from { width: 0 }
    to { width: 100% }
  }

  /* The typewriter cursor effect */
  @keyframes blink-caret {
    from, to { border-color: transparent }
    50% { border-color: orange; }
  }

  .shining-overlay {
    transition: all .5s;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    animation: shining .5s infinite;
  }

  @keyframes shining {
    0% { background-color: transparent }
    50% { background-color: black }
    100% { background-color: transparent }
  }

  .action-panel {
    position: fixed;
    right: 0;
    bottom: 0;
    left: 0;
    height: 200px;
    padding: 30px 50px;
    display: flex;

    ul.action-category {
      display: flex;
      height: 100%;
      flex: 1 1 auto;

      li {
        cursor: pointer;
        flex: 1 1 auto;
        color: white;
        margin: 0 10px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        border-radius: 20px;
        background-color: gray;
        height: 100%;
        font-size: 36px;
      }
    }

    ul.navigations-list {
      display: flex;
      flex-direction: column;
      height: 100%;
      flex: 0 0 120px;

      li {
        cursor: pointer;
        color: white;
        margin: 10px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        border-radius: 20px;
        background-color: gray;
        height: 100%;
        font-size: 24px;
      }
    }

    ul.skills-list {
      display: flex;
      flex-wrap: wrap;
      height: 100%;
      flex: 1 1 auto;

      li {
        cursor: pointer;
        flex: 0 0 calc(50% - 20px);
        color: white;
        margin: 10px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        border-radius: 20px;
        background-color: gray;
        height: calc(50% - 20px);
        font-size: 36px;
      }
    }

    ul.items-list {
      display: flex;
      height: 100%;
      flex: 1 1 auto;

      li {
        cursor: pointer;
        flex: 0 0 30%;
        color: white;
        margin: 0 10px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        border-radius: 20px;
        background-color: gray;
        height: 100%;
        font-size: 36px;
      }
    }
  }

  .item-description {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 5;
    background-color: rgba(0, 0, 0, .3);
    display: flex;
    align-items: center;
    justify-content: center;

    .modal {
      background-color: #444;
      padding: 20px;
      width: 360px;

      .modal-title {
        font-size: 24px;
        color: white;
        text-align: center;
      }

      .modal-content {
        color: white;
        text-align: center;
        margin: 20px 0 40px;
      }

      .modal-actions {
        display: flex;

        button {
          cursor: pointer;
          color: white;
          border: none;
          flex: 1 1 auto;
          height: 50px;
          border-radius: 5px;
          margin: 0 5px;
          font-size: 24px;

          &.positive {
            background-color: #0a0;
          }

          &.negative {
            background-color: #c00;
          }
        }
      }
    }
  }
}
</style>
