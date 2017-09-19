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
export default {
  data() {
    return {
      cantons: [
        {
          code: 'AG',
          name: 'Aargau',
          img: 'src/assets/AG.svg'
        },
        {
          code: 'AI',
          name: 'Appenzell Innerrhoden',
          img: 'src/assets/AI.svg'
        },
        {
          code: 'AR',
          name: 'Appenzell Ausserrhoden',
          img: 'src/assets/AR.svg'
        },
        {
          code: 'BE',
          name: 'Bern',
          img: 'src/assets/BE.svg'
        },
        {
          code: 'BL',
          name: 'Basel-Landschaft',
          img: 'src/assets/BL.svg'
        },
        {
          code: 'BS',
          name: 'Basel-Stadt',
          img: 'src/assets/BS.svg'
        },
        {
          code: 'FR',
          name: 'Fribourg',
          img: 'src/assets/FR.svg'
        },
        {
          code: 'GE',
          name: 'Genève',
          img: 'src/assets/GE.svg'
        },
        {
          code: 'GL',
          name: 'Glarus',
          img: 'src/assets/GL.svg'
        },
        {
          code: 'GR',
          name: 'Grisons',
          img: 'src/assets/GR.svg'
        },
        {
          code: 'JU',
          name: 'Jura',
          img: 'src/assets/JU.svg'
        },
        {
          code: 'LU',
          name: 'Lucerne',
          img: 'src/assets/LU.svg'
        },
        {
          code: 'NE',
          name: 'Neuchâtel',
          img: 'src/assets/NE.svg'
        },
        {
          code: 'NW',
          name: 'Nidwalden',
          img: 'src/assets/NW.svg'
        },
        {
          code: 'OW',
          name: 'Obwalden',
          img: 'src/assets/OW.svg'
        },
        {
          code: 'SG',
          name: 'St. Gallen',
          img: 'src/assets/SG.svg'
        },
        {
          code: 'SH',
          name: 'Schaffhausen',
          img: 'src/assets/SH.svg'
        },
        {
          code: 'SO',
          name: 'Solothurn',
          img: 'src/assets/SO.svg'
        },
        {
          code: 'SZ',
          name: 'Schwyz',
          img: 'src/assets/SZ.svg'
        },
        {
          code: 'TG',
          name: 'Thurgau',
          img: 'src/assets/TG.svg'
        },
        {
          code: 'TI',
          name: 'Ticino',
          img: 'src/assets/TI.svg'
        },
        {
          code: 'UR',
          name: 'Uri',
          img: 'src/assets/UR.svg'
        },
        {
          code: 'VD',
          name: 'Vaud',
          img: 'src/assets/VD.svg'
        },
        {
          code: 'VS',
          name: 'Valais',
          img: 'src/assets/VS.svg'
        },
        {
          code: 'ZG',
          name: 'Zug',
          img: 'src/assets/ZG.svg'
        },
        {
          code: 'ZH',
          name: 'Zürich',
          img: 'src/assets/ZH.svg'
        },
        {
          code: 'AG',
          name: 'Aargau',
          img: 'src/assets/AG.svg'
        },
        {
          code: 'AI',
          name: 'Appenzell Innerrhoden',
          img: 'src/assets/AI.svg'
        },
        {
          code: 'AR',
          name: 'Appenzell Ausserrhoden',
          img: 'src/assets/AR.svg'
        },
        {
          code: 'BE',
          name: 'Bern',
          img: 'src/assets/BE.svg'
        },
        {
          code: 'BL',
          name: 'Basel-Landschaft',
          img: 'src/assets/BL.svg'
        },
        {
          code: 'BS',
          name: 'Basel-Stadt',
          img: 'src/assets/BS.svg'
        },
        {
          code: 'FR',
          name: 'Fribourg',
          img: 'src/assets/FR.svg'
        },
        {
          code: 'GE',
          name: 'Genève',
          img: 'src/assets/GE.svg'
        },
        {
          code: 'GL',
          name: 'Glarus',
          img: 'src/assets/GL.svg'
        },
        {
          code: 'GR',
          name: 'Grisons',
          img: 'src/assets/GR.svg'
        },
        {
          code: 'JU',
          name: 'Jura',
          img: 'src/assets/JU.svg'
        },
        {
          code: 'LU',
          name: 'Lucerne',
          img: 'src/assets/LU.svg'
        },
        {
          code: 'NE',
          name: 'Neuchâtel',
          img: 'src/assets/NE.svg'
        },
        {
          code: 'NW',
          name: 'Nidwalden',
          img: 'src/assets/NW.svg'
        },
        {
          code: 'OW',
          name: 'Obwalden',
          img: 'src/assets/OW.svg'
        },
        {
          code: 'SG',
          name: 'St. Gallen',
          img: 'src/assets/SG.svg'
        },
        {
          code: 'SH',
          name: 'Schaffhausen',
          img: 'src/assets/SH.svg'
        },
        {
          code: 'SO',
          name: 'Solothurn',
          img: 'src/assets/SO.svg'
        },
        {
          code: 'SZ',
          name: 'Schwyz',
          img: 'src/assets/SZ.svg'
        },
        {
          code: 'TG',
          name: 'Thurgau',
          img: 'src/assets/TG.svg'
        },
        {
          code: 'TI',
          name: 'Ticino',
          img: 'src/assets/TI.svg'
        },
        {
          code: 'UR',
          name: 'Uri',
          img: 'src/assets/UR.svg'
        },
        {
          code: 'VD',
          name: 'Vaud',
          img: 'src/assets/VD.svg'
        },
        {
          code: 'VS',
          name: 'Valais',
          img: 'src/assets/VS.svg'
        },
        {
          code: 'ZG',
          name: 'Zug',
          img: 'src/assets/ZG.svg'
        },
        {
          code: 'ZH',
          name: 'Zürich',
          img: 'src/assets/ZH.svg'
        }
      ],
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