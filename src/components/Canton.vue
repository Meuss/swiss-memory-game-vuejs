<template>
  <div class="canton-wrapper">
    <div class="canton" v-for="canton in randomizeList(cantons)" :class="canton.code">
      <h4>{{canton.code}}</h4>
      <img :src="canton.img" :alt="canton.code" @click="select($event)">
    </div>
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
          img: 'src/assets/AG.png'
        },
        {
          code: 'AI',
          name: 'Appenzell Innerrhoden',
          img: 'src/assets/AI.png'
        },
        {
          code: 'AR',
          name: 'Appenzell Ausserrhoden',
          img: 'src/assets/AR.png'
        },
        {
          code: 'BE',
          name: 'Bern',
          img: 'src/assets/BE.png'
        },
        {
          code: 'BL',
          name: 'Basel-Landschaft',
          img: 'src/assets/BL.png'
        },
        {
          code: 'BS',
          name: 'Basel-Stadt',
          img: 'src/assets/BS.png'
        },
        {
          code: 'FR',
          name: 'Fribourg',
          img: 'src/assets/FR.png'
        },
        {
          code: 'GE',
          name: 'Genève',
          img: 'src/assets/GE.png'
        },
        {
          code: 'GL',
          name: 'Glarus',
          img: 'src/assets/GL.png'
        },
        {
          code: 'GR',
          name: 'Grisons',
          img: 'src/assets/GR.png'
        },
        {
          code: 'JU',
          name: 'Jura',
          img: 'src/assets/JU.png'
        },
        {
          code: 'LU',
          name: 'Lucerne',
          img: 'src/assets/LU.png'
        },
        {
          code: 'NE',
          name: 'Neuchâtel',
          img: 'src/assets/NE.png'
        },
        {
          code: 'NW',
          name: 'Nidwalden',
          img: 'src/assets/NW.png'
        },
        {
          code: 'OW',
          name: 'Obwalden',
          img: 'src/assets/OW.png'
        },
        {
          code: 'SG',
          name: 'St. Gallen',
          img: 'src/assets/SG.png'
        },
        {
          code: 'SH',
          name: 'Schaffhausen',
          img: 'src/assets/SH.png'
        },
        {
          code: 'SO',
          name: 'Solothurn',
          img: 'src/assets/SO.png'
        },
        {
          code: 'SZ',
          name: 'Schwyz',
          img: 'src/assets/SZ.png'
        },
        {
          code: 'TG',
          name: 'Thurgau',
          img: 'src/assets/TG.png'
        },
        {
          code: 'TI',
          name: 'Ticino',
          img: 'src/assets/TI.png'
        },
        {
          code: 'UR',
          name: 'Uri',
          img: 'src/assets/UR.png'
        },
        {
          code: 'VD',
          name: 'Vaud',
          img: 'src/assets/VD.png'
        },
        {
          code: 'VS',
          name: 'Valais',
          img: 'src/assets/VS.png'
        },
        {
          code: 'ZG',
          name: 'Zug',
          img: 'src/assets/ZG.png'
        },
        {
          code: 'ZH',
          name: 'Zürich',
          img: 'src/assets/ZG.png'
        },
        {
          code: 'AG',
          name: 'Aargau',
          img: 'src/assets/AG.png'
        },
        {
          code: 'AI',
          name: 'Appenzell Innerrhoden',
          img: 'src/assets/AI.png'
        },
        {
          code: 'AR',
          name: 'Appenzell Ausserrhoden',
          img: 'src/assets/AR.png'
        },
        {
          code: 'BE',
          name: 'Bern',
          img: 'src/assets/BE.png'
        },
        {
          code: 'BL',
          name: 'Basel-Landschaft',
          img: 'src/assets/BL.png'
        },
        {
          code: 'BS',
          name: 'Basel-Stadt',
          img: 'src/assets/BS.png'
        },
        {
          code: 'FR',
          name: 'Fribourg',
          img: 'src/assets/FR.png'
        },
        {
          code: 'GE',
          name: 'Genève',
          img: 'src/assets/GE.png'
        },
        {
          code: 'GL',
          name: 'Glarus',
          img: 'src/assets/GL.png'
        },
        {
          code: 'GR',
          name: 'Grisons',
          img: 'src/assets/GR.png'
        },
        {
          code: 'JU',
          name: 'Jura',
          img: 'src/assets/JU.png'
        },
        {
          code: 'LU',
          name: 'Lucerne',
          img: 'src/assets/LU.png'
        },
        {
          code: 'NE',
          name: 'Neuchâtel',
          img: 'src/assets/NE.png'
        },
        {
          code: 'NW',
          name: 'Nidwalden',
          img: 'src/assets/NW.png'
        },
        {
          code: 'OW',
          name: 'Obwalden',
          img: 'src/assets/OW.png'
        },
        {
          code: 'SG',
          name: 'St. Gallen',
          img: 'src/assets/SG.png'
        },
        {
          code: 'SH',
          name: 'Schaffhausen',
          img: 'src/assets/SH.png'
        },
        {
          code: 'SO',
          name: 'Solothurn',
          img: 'src/assets/SO.png'
        },
        {
          code: 'SZ',
          name: 'Schwyz',
          img: 'src/assets/SZ.png'
        },
        {
          code: 'TG',
          name: 'Thurgau',
          img: 'src/assets/TG.png'
        },
        {
          code: 'TI',
          name: 'Ticino',
          img: 'src/assets/TI.png'
        },
        {
          code: 'UR',
          name: 'Uri',
          img: 'src/assets/UR.png'
        },
        {
          code: 'VD',
          name: 'Vaud',
          img: 'src/assets/VD.png'
        },
        {
          code: 'VS',
          name: 'Valais',
          img: 'src/assets/VS.png'
        },
        {
          code: 'ZG',
          name: 'Zug',
          img: 'src/assets/ZG.png'
        },
        {
          code: 'ZH',
          name: 'Zürich',
          img: 'src/assets/ZG.png'
        }
      ]
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
    select: function(event) {
      event.target.parentElement.classList.add('shown');
    },
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
}

.canton {
  width: 130px;
  height: 130px;
  margin-bottom: 4px;
  background-color: #FFF;
  box-shadow: 1px 1px 6px 0px rgba(107, 107, 107, 0.15);
  border-radius: 3px;
}

.shown {
  background-color: #ddd;
}

img {
  width: 60%;
  cursor: pointer;
}
</style>