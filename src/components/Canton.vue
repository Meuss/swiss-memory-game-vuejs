<template>
  <div class="wrapper">
    <div class="canton-wrapper">
      <div class="canton" v-for="(canton, index) in shuffleArrayTwice(cantons)" :data-code="canton.code" :data-matched="canton.matched" :data-faceup="canton.faceUp" @click="checkGuess($event)">
        <transition-group name="fade" mode="out-in">
          <div class="swissflag" key="1"></div>
          <img :src="canton.img" :alt="canton.code" key="2">
        </transition-group>
      </div>
    </div>
    <ul>
      <li v-for="canton in cantons" :data-code="canton.code" :data-matched="canton.matched">{{canton.name}}</li>
    </ul>
  </div>
</template>

<script>
import cantons from '../assets/cantons.json';
export default {
  data() {
    return {
      cantons: cantons,
      guess1: '',
      guess2: '',
      count: 0,
      wait: false,
    }
  },
  methods: {
    shuffleArrayTwice: function(array) {
      let newArray = array.slice();
      // let newArray2 = array.slice()
      for (var i = newArray.length - 1; i > 0; i--) {
        var rand = Math.floor(Math.random() * (i + 1));
        [newArray[i], newArray[rand]] = [newArray[rand], newArray[i]];
      }
      return newArray;
      // for (var i = newArray2.length - 1; i > 0; i--) {
      //   var rand = Math.floor(Math.random() * (i + 1));
      //   [newArray2[i], newArray2[rand]] = [newArray2[rand], newArray2[i]];
      // }
      // let bothArrays = newArray.concat(newArray2);
      // for (var i = bothArrays.length - 1; i > 0; i--) {
      //   var rand = Math.floor(Math.random() * (i + 1));
      //   [bothArrays[i], bothArrays[rand]] = [bothArrays[rand], bothArrays[i]];
      // }
      // return bothArrays;
    },
    finishGame: function() {
      console.log('ggwp!');
    },
    checkGuess: function(event) {
      let el = event.target;
      // console.log(this.data);
      // console.log(this.faceUp);

      // dont execute code if canton is faceup or waiting to turn back over
      if ((el.dataset.faceup == 0) && (this.wait === false)) {
        if ((this.count < 2)) {
          if (this.count == 0) {
            // console.log('turn back over');
          }
          this.count += 1;
          // first guess
          if (this.count === 1) {
            this.guess1 = el.dataset.code;
            el.dataset.faceup = 1;
          }
          // second guess
          else {
            this.wait = true;
            this.guess2 = el.dataset.code;
            el.dataset.faceup = 1;
            // if match
            if (this.guess1 === this.guess2) {
              this.wait = false;
              const matchedGuess = document.querySelectorAll(`.canton[data-faceup='1']`);
              // console.log(matchedGuess);

              for (let card of matchedGuess) {
                card.dataset.faceup = 0;
                card.dataset.matched = 1;
                document.querySelector(`ul li[data-code='${card.dataset.code}']`).dataset.matched = 1;
              }
              // check if game finished
              const unmatchedCantons = document.querySelectorAll(`.canton[data-matched='0']`);
              console.log('cantons left: ' + unmatchedCantons.length);
              if (unmatchedCantons.length == 0) {
                this.finishGame();
              }
            }
            // else fail
            else {
              const failedGuess = document.querySelectorAll(`.canton[data-faceup='1']`);
              setTimeout(() => {
                for (let card of failedGuess) {
                  card.dataset.faceup = 0;
                }
                this.wait = false;
              }, 800);
            }
            // reset checks
            this.count = 0;
            this.guess1 = '';
            this.guess2 = '';
          }
        }
      }
    },
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
}
.canton-wrapper {
  /* display: flex; */
  /* flex-wrap: wrap; */
  /* justify-content: space-between; */
  /* width: 90%; */
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(8, 100px);
  grid-template-rows: repeat(7, 100px);
  grid-gap: 10px;
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
[data-matched="1"] {
  background-color: rgba(0,97,80,0.6);
}

.canton span {
  height: 100%;
  pointer-events: none;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.swissflag {
  /* opacity: 0.3; */
  pointer-events: none;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-image: url('../assets/switzerland.svg');
  background-size: cover;
  background-position: center center;
  background-repeat: no-repeat;
}

[data-faceup="1"] .swissflag,
[data-matched="1"] .swissflag {
  opacity: 0;
  pointer-events: none;
}

img {
  pointer-events: none;
  width: 60%;
}

ul {
  padding-left: 0;
  list-style-type: none;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  flex-wrap: wrap;
  width: 90%;
  margin: 40px auto;
  max-height: 150px;
}

li[data-matched="1"] {
  text-decoration: line-through;
  opacity: 1;
  background-color: transparent;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>