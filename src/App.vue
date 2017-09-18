<template>
  <div id="app">
    <div class="header">
      <img class="logo" src="./assets/logo.png">
      <h1>{{ msg }}</h1>
      <img class="switzerland" src="./assets/switzerland.svg">
    </div>
    <canton></canton>
  </div>
</template>

<script>
import Canton from './components/Canton.vue';
export default {
  components: {
    Canton
  },
  name: 'app',
  data() {
    return {
      msg: 'Learning Vue.js - Swiss cantons memory game'
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #ddd;
  height: 100%;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100px;
  width: 90%;
  margin: 0 auto;
  img {
    width: auto;
    height: 30px;
  }
  .logo {
    padding-right: 20px;
  }
  .switzerland {
    padding-left: 20px;
  }
}

h1,
h2 {
  font-weight: normal;
  margin: 0px;
}

a {
  color: #42b983;
}

html,
body {
  margin: 0;
  height: 100%;
}
</style>
