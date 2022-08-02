<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter"></div>
    <div class="column is-three-quarter content">
      <div class="list"></div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ITask from "./interfaces/ITask";

export default defineComponent({
  name: "App",

  components: {},

  data() {
    return {
      tasks: [] as ITask[],
      activeDarkMode: false,
    };
  },

  computed: {
    listThisEmpty(): boolean {
      return this.tasks.length === 0;
    },
  },

  methods: {
    saveTask(task: ITask) {
      this.tasks.push(task);
    },
    swapTheme(activeDarkMode: boolean) {
      this.activeDarkMode = activeDarkMode;
    },
  },
});
</script>

<style>
.list {
  padding: 1.25rem;
}
main {
  --bg-primary: #fff;
  --primary-text: #000;
}
main.dark-mode {
  --bg-primary: #2b2d42;
  --primary-text: #ddd;
}

.content {
  background-color: var(--bg-primary);
}
</style>