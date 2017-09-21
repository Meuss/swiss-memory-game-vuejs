<template>
  <div class="wrapper">
    <div class="canton-wrapper">
      <div class="canton" v-for="(canton, index) in shuffleArrayTwice(cantons)" :data-code="canton.code" :data-matched="canton.matched" :data-faceup="canton.faceUp" @click="checkGuess($event)">
        <transition name="fade" mode="out-in">
          <div v-if="!canton.faceUp" class="swissflag"></div>
          <img v-else :src="canton.img" :alt="canton.code">
        </transition>
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
    }
  },
  methods: {
    shuffleArrayTwice: function(array) {
      let newArray = array.slice();
      let newArray2 = array.slice()
      for (var i = newArray.length - 1; i > 0; i--) {
        var rand = Math.floor(Math.random() * (i + 1));
        [newArray[i], newArray[rand]] = [newArray[rand], newArray[i]];
      }
      for (var i = newArray2.length - 1; i > 0; i--) {
        var rand = Math.floor(Math.random() * (i + 1));
        [newArray2[i], newArray2[rand]] = [newArray2[rand], newArray2[i]];
      }
      let bothArrays = newArray.concat(newArray2);
      for (var i = bothArrays.length - 1; i > 0; i--) {
        var rand = Math.floor(Math.random() * (i + 1));
        [bothArrays[i], bothArrays[rand]] = [bothArrays[rand], bothArrays[i]];
      }
      return bothArrays;
    },
    checkGuess: function(event) {
      let el = event.target;
      console.log(this);
      if ((this.count < 2)) { // TODO: make sure we dont click same canton twice
        if (this.count == 0) {
          // console.log('turn back over');
        }
        this.count += 1;
        // first guess
        if (this.count === 1) {
          this.guess1 = el.dataset.code;
          console.log('first guess - turn face up');
          el.dataset.faceup = 1;
        }
        // second guess
        else {
          this.guess2 = el.dataset.code;
          console.log('second guess - turn face up');
          el.dataset.faceup = 1;
          // if match
          if (this.guess1 === this.guess2) {
            const matchedGuess = document.querySelectorAll(`.canton[data-faceup='1']`);
            setTimeout(() => {
              for (let card of matchedGuess) {
                card.dataset.faceup = 0;
                card.dataset.matched = 1;
              }
            }, 800);
          }
          // else fail
          else {
            const failedGuess = document.querySelectorAll(`.canton[data-faceup='1']`);
            setTimeout(() => {
              for (let card of failedGuess) {
                card.dataset.faceup = 0;
              }
            }, 800);
          }
          // reset checks
          this.count = 0;
          this.guess1 = '';
          this.guess2 = '';
        }
      }
    },
    // checkGuess: function(event) {
    //   console.log(this);
    //   // console.log(this.$el); // renders the html canton div clicked!
    //   let el = event.target;
    //   // console.log
    //   el.dataset.faceUp = 1;
    //   if ((this.count < 2) && (!el.classList.contains('faceUp'))) {
    //     if (this.count == 0) {
    //       const facedUp = document.querySelectorAll('.faceUp:not(.matched)');
    //       for (let card of facedUp) {
    //         card.className = 'canton';
    //       }
    //     }
    //     this.count += 1;
    //     el.classList.add('faceUp');
    //     // first guess
    //     if (this.count === 1) {
    //       this.guess1 = el.dataset.code;
    //     }
    //     // second guess
    //     else {
    //       this.guess2 = el.dataset.code;
    //       // if match
    //       if (this.guess1 === this.guess2) {
    //         console.log(el.dataset.code);
    //         // const matched = document.querySelectorAll(`[data-code="${el.dataset.code}"]`);
    //         // for (let card of matched) {
    //         // card.className += ' matched';
    //         // card.dataset.matched = 1;
    //         // }
    //       }
    //       // else fail
    //       else {
    //         const facedUp = document.querySelectorAll('.faceUp:not(.matched)');
    //         setTimeout(() => {
    //           for (let card of facedUp) {
    //             card.className = 'canton';
    //           }
    //         }, 800);
    //         this.fails += 1;
    //       }
    //       // reset checks
    //       this.count = 0;
    //     }
    //   }
    // },
    checkGameFinished: function() {
      console.log('game not finished!');
    }
  }
}
</script>

<style scoped>
.canton-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 90%;
  margin: 0 auto;
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
  border-radius: 3px;
}

.swissflag {
  /* pointer-events: none; */
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

img {
  /* opacity: 0.1; */
  /* transition: all 0.1s ease-out; */
}







































































/* .faceUp img,
.matched img {
  opacity: 1;
}

.faceUp {
  background-color: #ddd;
  transition: all 0.1s ease-in;
}

.matched {
  opacity: 0.5;
  background-color: #ddd;
}

.faceUp,
.matched {
  background-image: none;
  background-color: #FFF;
}

.matched h4 {
  opacity: 1;
}

.matched img {
  filter: grayscale(1);
} */

img {
  width: 60%;
  cursor: pointer;
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

li.matched {
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