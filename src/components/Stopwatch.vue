<template>
  <span id="time" v-html="time">
  </span>
</template>

<style>

</style>

<script>
module.exports = {
  data: function() {
    return {
      clockstate: "paused",
      startTime: Date.now(),
      currentTime: Date.now(),
      interval: null
    }
  },
  mounted: function() {
    this.interval = setInterval(this.updateCurrentTime, 1);
  },
  destroyed: function() {
    clearInterval(this.interval)
  },
  computed: {
    time: function() {
      return this.minutes + ':' + this.seconds + ':' + Number(String((this.milliseconds % 1000)).charAt(0));
    },
    milliseconds: function() {
      return this.currentTime - this.$data.startTime;
    },
    minutes: function() {
      var lapsed = this.milliseconds;
      var min = Math.floor((lapsed / 1000 / 60) % 60);
      return min >= 10 ? min : '0' + min;
    },
    seconds: function() {
      var lapsed = this.milliseconds;
      var sec = Math.ceil((lapsed / 1000) % 60);
      return sec >= 10 ? sec : '0' + sec;
    }
  },
  methods: {
    reset: function() {
      this.$data.clockstate = "started";
      this.$data.startTime = Date.now();
      this.$data.currentTime = Date.now();
    },
    updateCurrentTime: function() {
      if (this.$data.clockstate == "started") {
        this.currentTime = Date.now();
      }
    }
  }
} 
</script>