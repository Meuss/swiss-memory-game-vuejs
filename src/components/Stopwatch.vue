<template>
  <span id="time" v-html="time" @click="startFFS"> </span>
</template>

<style></style>

<script>
import bus from '../bus.js';

export default {
  data() {
    return {
      clockstate: 'stopped',
      startTime: Date.now(),
      currentTime: Date.now(),
      interval: null,
    };
  },
  mounted: function () {
    this.interval = setInterval(this.updateCurrentTime, 1);
    bus.$on('startTimer', function () {
      // wtf is wrong here, I can't access any data. Oh well,..
      ffs();
    });
  },
  destroyed: function () {
    clearInterval(this.interval);
  },
  computed: {
    time: function () {
      return this.minutes + ':' + this.seconds;
    },
    milliseconds: function () {
      return this.currentTime - this.$data.startTime;
    },
    minutes: function () {
      var lapsed = this.milliseconds;
      var min = Math.floor((lapsed / 1000 / 60) % 60);
      return min >= 10 ? min : '0' + min;
    },
    seconds: function () {
      var lapsed = this.milliseconds;
      var sec = Math.ceil((lapsed / 1000) % 60);
      return sec >= 10 ? sec : '0' + sec;
    },
  },
  methods: {
    startFFS: function () {
      this.clockstate = 'started';
    },
    reset: function () {
      this.$data.clockstate = 'started';
      this.$data.startTime = Date.now();
      this.$data.currentTime = Date.now();
    },
    updateCurrentTime: function () {
      if (this.$data.clockstate == 'started') {
        this.currentTime = Date.now();
      }
    },
  },
};
function ffs() {
  document.querySelector('#time').click();
}
</script>
