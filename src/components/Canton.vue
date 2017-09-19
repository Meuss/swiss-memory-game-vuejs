<template>
  <div class="wrapper">
    <div class="canton-wrapper">
      <div class="canton" v-for="canton in randomizeList(cantons)" :data-code="canton.code">
        <h4>{{canton.code}}</h4>
        <img :src="canton.img" :alt="canton.code" @click="checkGuess($event)">
      </div>
    </div>
    <!-- <div>Fails = {{fails}}</div>  this is not how i should do it-->
    <ul>
      <li>print out cantons -> change the array</li>
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
      fails: 0,
    }
  },
  methods: {
    randomizeList: function(array) {
      var currentIndex = array.length;
      var temporaryValue;
      var randomIndex;
      var myRandomizedList;
      myRandomizedList = array.slice(0)
      while (0 !== currentIndex) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;
        temporaryValue = myRandomizedList[currentIndex];
        myRandomizedList[currentIndex] = myRandomizedList[randomIndex];
        myRandomizedList[randomIndex] = temporaryValue;
      }
      return myRandomizedList;
    },
    checkGuess: function(event) {
      let el = event.target.parentElement;

      if ((this.count < 2) && (!el.classList.contains('faceUp'))) {
        this.count += 1;
        el.classList.add('faceUp');
        // first guess
        if (this.count === 1) {
          this.guess1 = el.dataset.code;
        }
        // second guess
        else {
          this.guess2 = el.dataset.code;
          // if match
          if (this.guess1 === this.guess2) {
            const matched = document.querySelectorAll(`[data-code="${el.dataset.code}"]`);
            for (let card of matched) {
              card.className += ' matched';
            }
            // checkGameFinished();
          }
          // else fail
          else {
            const facedUp = document.querySelectorAll('.faceUp:not(.matched)');
            setTimeout(() => {
              for (let card of facedUp) {
                card.className = 'canton';
              }
            }, 800);
            this.fails += 1;
            console.log(`fails: ${this.fails}`);
            // checkGameFinished();
          }

          // reset
          this.count = 0;
        }
      }
    },
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
  margin-bottom: 4px;
  box-shadow: 1px 1px 6px 0px rgba(107, 107, 107, 0.15);
  border-radius: 3px;
  background-image: url('../assets/switzerland.svg');
  background-size: cover;
  background-position: center center;
  background-repeat: no-repeat;
}

img {
  opacity: 0;
}

.faceUp img,
.matched img {
  opacity: 1;
}

.faceUp {
  background-color: #ddd;
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
}

img {
  width: 60%;
  cursor: pointer;
}
</style>