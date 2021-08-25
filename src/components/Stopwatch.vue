<template>
  <span id="time" v-html="time"></span>
</template>

<style></style>

<script>
import { ref, computed, onMounted } from 'vue';

export default {
  setup() {
    // data
    const clockstate = ref('stopped');
    const startTime = ref(Date.now());
    const currentTime = ref(Date.now());
    let interval = ref(null);

    // computed
    const time = computed(() => `${minutes.value}:${seconds.value}`);
    const milliseconds = computed(() => currentTime.value - startTime.value);
    const minutes = computed(function () {
      const min = Math.floor((milliseconds.value / 1000 / 60) % 60);
      return min >= 10 ? min : '0' + min;
    });
    const seconds = computed(function () {
      const sec = Math.ceil((milliseconds.value / 1000) % 60);
      return sec >= 10 ? sec : '0' + sec;
    });

    // mounted
    onMounted(() => {
      interval.value = setInterval(updateCurrentTime, 1);
      clockstate.value = 'started';
    });

    // methods
    function updateCurrentTime() {
      if (clockstate.value == 'started') {
        currentTime.value = Date.now();
      }
    }
    function reset() {
      clockstate.value = 'started';
      startTime.value = Date.now();
      currentTime.value = Date.now();
    }

    return {
      clockstate,
      startTime,
      currentTime,
      interval,
      time,
      milliseconds,
      minutes,
      seconds,
      updateCurrentTime,
      reset,
    };
  },
};
</script>
