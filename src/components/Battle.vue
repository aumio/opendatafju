<template lang="pug">
  #duel.full-screen
    .duel-dog
      img.dog(src="@/assets/battle-dog.png", @click="subHp(dog)")
      .dueler-info(@click="addHp(dog)")
        .row
          .dueler-name {{ dog.name }}
          .dueler-level Lv.{{ dog.level }}
        .dueler-hp
          span HP
          .hp-bar
            img.bone(src="@/assets/bone.svg", v-for="i in dog.hp")
    .duel-cat
      img.cat(src="@/assets/battle-cat.png", @click="subHp(cat)")
      .dueler-info(@click="addHp(cat)")
        .row
          .dueler-name {{ cat.name }}
          .dueler-level Lv.{{ cat.level }}
        .dueler-hp
          span HP
          .hp-bar
            img.fish(src="@/assets/fish.svg", v-for="i in cat.hp")
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
    }
  },
  mounted () {
    //
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
  }
}
</script>

<style lang="scss">
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

    &:before {
      bottom: 85px;
      right: 40px;
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

    &:before {
      bottom: 65px;
      right: 0;
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
}
</style>
