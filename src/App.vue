<template>
  <section class="hero">
      <div class="container hero__container">
        <h1 class="hero__title">
          Ты сегодня покормил кота?
        </h1>
        <div class="hero__cards">
          <div class="hero__card card" v-for="item in cards" :key="item.id">
            <!-- <div class="card__body" @click="changeBody(item)" :class="item.clicked ? 'isSelected' : ''" :style="item.disabled ? 'color: #b3b3b3; pointer-events: none;' : ''"> -->
            <div class="card__body" 
              @click="changeBody(item)" 
              :class="item.clicked && !item.disabled ? 'isSelected' : item.disabled ? 'isDisabled' : ''" 
              :style="item.disabled ? 'color: #b3b3b3; pointer-events: none;' : ''"
              @mouseleave="changePretitle(item)"
              @mouseenter="changePretitleBack(item)"
            >
              <p class="card__pretitle" :style="item.pretitle == 'Котэ не одобряет?' ? 'color: #E62E7A;' : ''">
                {{item.pretitle}}
              </p>
              <h2 class="card__title">
                Нямушка
                <span class="card__subtitle">с {{item.taste}}</span>
              </h2>
              <ul class="card__list">
                <li class="card__list-item">
                  {{item.portion}} порций
                </li>
                <li class="card__list-item" v-if="item.mouse > 0">
                  {{item.mouse}} {{word(item.mouse, words)}} в подарок
                </li>
                <li class="card__list-item" v-else>
                  мышь в подарок
                </li>
              </ul>
              <!-- <img src="/img/cat.png" alt="Котейка" class="card__img"> -->
              <div class="card__weight" :style="item.clicked && !item.disabled ? 'background: #E62E7A;' : item.disabled ? 'background: #979797' : '#1698d9'">
                <div class="card__circle">
                  <p class="card__count">
                    {{item.weight}}
                  </p>
                  <p class="card__measure">
                    кг
                  </p>
                </div>
              </div>
            </div>
            <div class="card__status">
              <p v-if="item.clicked && !item.disabled">
                {{item.footer}}
              </p>
              <p v-else-if="item.disabled" style="color: #ffff66;">
                Печалька, с {{item.taste}} закончился.
              </p>
              <p v-else>
                Чего сидишь? Порадуй котэ, <a href="#" class="card__buy" @click="changeBody(item)">купи</a>.
              </p>
            </div>
          </div>
        </div>
      </div>
  </section>
</template>

<script>
import { word } from '@/mixins/word.js';
export default {
  data() {
    return {
      cards: [
        {
          id: 1,
          clicked: false,
          disabled: false,
          pretitle: 'Сказочное заморское яство',
          taste: 'фуа-гра',
          portion: 10,
          mouse: 0,
          weight: '0,5',
          footer: 'Печень утки разварная с артишоками.',
        },
        {
          id: 2,
          clicked: false,
          disabled: false,
          pretitle: 'Сказочное заморское яство',
          taste: 'рыбой',
          portion: 40,
          mouse: 2,
          weight: '2',
          footer: 'Головы щучьи с чесноком да свежайшая сёмгушка.',
        },
        {
          id: 3,
          clicked: false,
          disabled: true,
          pretitle: 'Сказочное заморское яство',
          taste: 'курой',
          portion: 100,
          mouse: 5,
          weight: '5',
          footer: 'Филе из цыплят с трюфелями в бульоне.',
        }
      ],
      words: ['мышь', 'мыши', 'мышей']
    }
  },
  methods: {
    word,
    changeBody(val) {
      val.clicked = !val.clicked;
      // console.log(val)
      if (!val.clicked) {
        val.pretitle = 'Сказочное заморское яство'
      }
    },
    changePretitle(val) {
      if (val.clicked) {
        val.pretitle = 'Котэ не одобряет?';
        // console.log(val)
      } else {
        return
      }
    },
    changePretitleBack(val) {
      if (val.clicked) {
        val.pretitle = 'Сказочное заморское яство';
        // console.log(val)
      } else {
        return
      }
    },
  },
  computed: {
  }
}
</script>

<style lang="scss">
// @import '/src/assets/css/fonts.css';
@import url('https://fonts.googleapis.com/css2?family=Exo+2:wght@100&display=swap');

// colors
$gray: #F2F2F2;
$dark-grey: #666666;
$blue: #1698D9;
$hover-blue: #2EA8E6;
$white: #ffffff;

// fonts
$first-ff: "Trebuchet MS", Tahoma, sans-serif;
$second-ff: "Exo 2", Tahoma, sans-serif;
$second-ff-alt: Exo\ 2, Tahoma, sans-serif;

//general
h1, h2, h3, ul {
  margin: 0;
}
  
p {
  padding: 0;
  margin: 0;
}

body {
  height: inherit;
  margin: 0;
  background: linear-gradient(180deg, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 5e-05) 49.88%, rgba(0, 0, 0, 0.5) 100%), url('./assets/img/background.png');
}

.hero {
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translate(0, -50%);
  &__container {
    margin: 0 auto;
    width: 1280px;
  }
  &__title {
    margin-top: 36px;
    font-family: 'Exo 2', Tahoma, sans-serif;
    font-size: 36px;
    font-weight: 200;
    color: #fff;
    text-align: center;
    text-shadow: 0px 1px 1px #000000;
  }
  &__cards {
    display: flex;
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
    font-family: $first-ff;
  }
}

.card {
  margin: 25px 40px;
  width: 320px;
  // height: 480px;
  &__pretitle {
    margin-bottom: 5px;
    font-size: 16px;
    line-height: 19px;
    color: #666666;
    pointer-events: none;
  }
  &__title {
    margin-bottom: 15px;
    font-weight: 700;
    font-size: 48px;
    line-height: 56px;
    pointer-events: none;
  }
  &__subtitle {
    display: block;
    font-weight: 700;
    font-size: 24px;
    line-height: 28px;
    pointer-events: none;
  }
  &__body {
    padding-left: 51px;
    padding-top: 21px;
    padding-bottom: 300px;
    position: relative;
    // overflow: hidden;
    background: $gray;
    background: url('./assets/img/cat.png') no-repeat left -25px bottom -95px,linear-gradient(135deg, transparent 24px, #fff 24px);
    border-radius: 12px;
    cursor: pointer;
  }
  .isDisabled {
    background: url('./assets/img/cat-negative.png') no-repeat left -33px bottom -97px, linear-gradient(135deg, transparent 24px, #fff 24px) !important;
    &::before {
      background-color: gray;
      background: linear-gradient(135deg, transparent 25px, gray 25px);
    }
  }
  &__body::before {
    content: "";
    position: absolute;
    top: -4px;
    right: -4px;
    bottom: -4px;
    left: -4px;
    z-index: -1;
    background-color: $blue;
    background: linear-gradient(135deg, transparent 25px, $blue 25px);
    border-radius: 12px;
  }
  &__body:hover::before {
    background: linear-gradient(135deg, transparent 25px, $hover-blue 25px);
  }
  .isSelected {
    &::before {
      background-color: #E62E7A !important;
      background: linear-gradient(135deg, transparent 25px, #E62E7A 25px) !important;
    }
  }
  &__list {
    padding-left: 0px;
    font-weight: 400;
    font-size: 14px;
    line-height: 16px;
    color: $dark-grey;
    list-style: none;
    pointer-events: none;
  }
  &__img {
    position: absolute;
    bottom: -95px;
    left: -25px;
    z-index: 0;
    width: 370px;
  }
  &__weight {
    position: absolute;
    bottom: 15px;
    right: 15px;
    width: 81px;
    height: 81px;
    border-radius: 50%;
    background: #1698d9;
    color: #fff;
    text-align: center;
    pointer-events: none;
  }
  &__circle {
    position: relative;
    top: 20px;
  }
  &__count {
    font-weight: 400;
    font-size: 42px;
    line-height: 33px;
    color: $white;
  }

  &__measure {
    font-weight: 400;
    font-size: 21px;
    line-height: 22px;
    color: $white;
  }

  &__status {
    margin-top: 14px;
    text-align: center;
    font-weight: 400;
    font-size: 13px;
    line-height: 15px;
    color: $white;
  }

  &__buy {
    text-decoration: dotted;
    color: $blue;
  }

}

@media (max-width:1279px){
  .hero {
    &__container {
      width: auto;
    }
  }
  .card {
    margin: 25px 20px;
  }
}

@media (max-width:1080px){
  .hero {
    position: relative;
    transform: none;
  }
  .card {
      margin: 25px 20px;
    }
}

</style>
