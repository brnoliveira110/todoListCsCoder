<template>
  <section
    class="is-flex is-align-items-center is-justify-content-space-between"
  >
    <TimerTodo :timeInSeconds="timeInSeconds" />

    <ButtonTracker
      @clicked="start"
      icon="fas fa-play"
      text="play"
      :disabled="runningStopwatch"
    />

    <ButtonTracker
      @clicked="finish"
      icon="fas fa-stop"
      text="stop"
      :disabled="!runningStopwatch"
    />
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TimerTodo from "./TimerTodo.vue";
import ButtonTracker from "./ButtonTracker.vue";

export default defineComponent({
  name: "DelayerTodo",
  emits: ["toTimerEnded"],

  components: {
    TimerTodo,
    ButtonTracker,
  },

  data() {
    return {
      timeInSeconds: 0,
      timer: 0,
      runningStopwatch: false,
    };
  },

  methods: {
    start() {
      this.runningStopwatch = true;
      this.timer = setInterval(() => {
        this.timeInSeconds += 1;
      }, 1000);
    },
    finish() {
      this.runningStopwatch = false;
      clearInterval(this.timer);
      this.$emit("toTimerEnded", this.timeInSeconds);
      this.timeInSeconds = 0;
    },
  },
});
</script>