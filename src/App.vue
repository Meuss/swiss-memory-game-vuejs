<template>
  <div>
    <div class="header">
      <img class="logo" src="/logo.png" />
      <h1>Swiss cantons memory game</h1>
      <img class="switzerland" src="/switzerland.svg" />
    </div>
    <Stopwatch />
    <Canton />
    <a href="https://github.com/Meuss/swiss-memory-game-vuejs" target="_blank" class="github">
      <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"
        />
      </svg>
    </a>
  </div>
</template>

<script>
import { inject } from 'vue';
import Stopwatch from './components/Stopwatch.vue';
import Canton from './components/Canton.vue';

export default {
  name: 'App',
  setup() {
    const emitter = inject('emitter');

    emitter.on('startGame', function () {
      startAppToCanton();
    });

    const startAppToCanton = () => {
      emitter.emit('startAppToCanton');
    };

    return {
      startAppToCanton,
    };
  },
  components: {
    Stopwatch,
    Canton,
  },
};
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
  position: relative;
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
#time {
  margin-bottom: 10px;
  display: block;
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
  overflow: hidden;
}
.github {
  padding: 10px 0px;
  bottom: -40px;
  right: -60px;
  position: absolute;
  background: black;
  color: black;
  box-shadow: -1px -1px 20px 0px rgba(0, 0, 0, 0.3);
  display: inline-block;
  width: 150px;
  height: 80px;
  transform: rotate(-45deg);
  transform-origin: 50% 50%;
  transition: 0.15s ease-out;
  svg {
    transform: rotate(45deg);
    fill: white;
    height: 25px;
  }
}
</style>
