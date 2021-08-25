<template>
  <div class="wrapper">
    <div class="canton-wrapper">
      <div
        class="canton"
        v-for="(canton, index) in shuffleArrayTwice(cantons)"
        :key="`canton-${index}`"
        :data-code="canton.code"
        :data-matched="canton.matched"
        :data-faceup="canton.faceUp"
        @click="handleClick($event)"
      >
        <div>
          <div class="swissflag" key="1"></div>
          <img :src="canton.img" :alt="canton.code" key="2" />
        </div>
      </div>
    </div>
    <ul>
      <li v-for="(canton, key) in cantonsOnce(cantons)" :key="`canton-${key}`" :data-code="canton.code" :data-matched="canton.matched">
        {{ canton.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import cantonsData from '../assets/cantons.json';
import { ref, inject } from 'vue';

export default {
  setup() {
    // data
    const cantons = ref(cantonsData);
    const guess1 = ref('');
    const guess2 = ref('');
    const count = ref(0);
    const wait = ref(false);
    const started = ref(false);

    // bus
    const emitter = inject('emitter');

    // methods
    function handleClick(event) {
      if (started.value === false) {
        started.value = true;
        startGame();
      }
      checkGuess(event);
    }
    function startGame() {
      emitter.emit('startGame');
    }
    function cantonsOnce() {
      return cantons.value.filter((canton, key) => key < 26);
    }
    function shuffleArrayTwice(array) {
      let newArray = array.slice();
      for (var i = newArray.length - 1; i > 0; i--) {
        var rand = Math.floor(Math.random() * (i + 1));
        [newArray[i], newArray[rand]] = [newArray[rand], newArray[i]];
      }
      return newArray;
    }
    function checkGuess(event) {
      let el = event.target;
      if (el.dataset.faceup == 0 && wait.value === false) {
        if (count.value < 2) {
          if (count.value == 0) {
          }
          count.value += 1;
          // first guess
          if (count.value === 1) {
            guess1.value = el.dataset.code;
            el.dataset.faceup = 1;
          }
          // second guess
          else {
            wait.value = true;
            guess2.value = el.dataset.code;
            el.dataset.faceup = 1;
            // if match
            if (guess1.value === guess2.value) {
              wait.value = false;
              const matchedGuess = document.querySelectorAll(`.canton[data-faceup='1']`);
              for (let card of matchedGuess) {
                card.dataset.faceup = 0;
                card.dataset.matched = 1;
                document.querySelector(`ul li[data-code='${card.dataset.code}']`).dataset.matched = 1;
              }
              // check if game finished
              const unmatchedCantons = document.querySelectorAll(`.canton[data-matched='0']`);
              if (unmatchedCantons.length == 0) {
                finishGame();
              }
            }
            // else fail
            else {
              const failedGuess = document.querySelectorAll(`.canton[data-faceup='1']`);
              setTimeout(() => {
                for (let card of failedGuess) {
                  card.dataset.faceup = 0;
                }
                wait.value = false;
              }, 800);
            }
            // reset checks
            count.value = 0;
            guess1.value = '';
            guess2.value = '';
          }
        }
      }
    }
    function finishGame() {
      console.log('ggwp! TODO');
    }

    return {
      cantons,
      guess1,
      guess2,
      count,
      wait,
      started,
      handleClick,
      startGame,
      cantonsOnce,
      shuffleArrayTwice,
      checkGuess,
      finishGame,
    };
  },
};
</script>

<style scoped lang="scss">
.wrapper {
  display: flex;
  justify-content: center;
}
.canton-wrapper {
  display: grid;
  grid-template-columns: repeat(8, 100px);
  grid-template-rows: repeat(7, 100px);
  grid-gap: 10px;
  margin-right: 20px;
}

h3,
h4 {
  margin: 0px;
  opacity: 0;
}

.canton {
  width: 100px;
  height: 100px;
  position: relative;
  margin-bottom: 4px;
  box-shadow: 1px 1px 6px 0px rgba(107, 107, 107, 0.15);
  background-color: white;
  border-radius: 3px;
  cursor: pointer;
}
[data-matched='1'] {
  background-color: rgba(0, 97, 80, 0.6);
}

.canton > div {
  height: 100%;
  pointer-events: none;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  img {
    pointer-events: none;
  }
}

.swissflag {
  pointer-events: none;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-image: url('../../switzerland.svg');
  background-size: cover;
  background-position: center center;
  background-repeat: no-repeat;
}

[data-faceup='1'] .swissflag,
[data-matched='1'] .swissflag {
  opacity: 0;
  pointer-events: none;
}

img {
  pointer-events: none;
  width: 60%;
}

ul {
  margin-top: 0px;
  padding-left: 0;
  list-style-type: none;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  flex-wrap: wrap;
}

li[data-matched='1'] {
  text-decoration: line-through;
  opacity: 1;
  background-color: transparent;
}
</style>
