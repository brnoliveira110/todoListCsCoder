<template>
  <main
    class="columns is-gapless is-multiline"
    :class="{ 'dark-mode': activeDarkMode }"
  >
    <div class="column is-one-quarter">
      <SideBar @toThemeChanged="swapTheme" />
    </div>
    <div class="column is-three-quarter content">
      <FormTodo @onSaveTask="saveTask" />
      <div class="list">
        <TaskTodo v-for="(task, index) in tasks" :key="index" :task="task" />
        <BoxTracker v-if="listThisEmpty"
          ><p>Você não está muito produtivo hoje :(</p></BoxTracker
        >
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ITask from "./interfaces/ITask";
import SideBar from "./components/SideBar.vue";
import FormTodo from "./components/FormTodo.vue";
import TaskTodo from "./components/TaskTodo.vue";
import BoxTracker from "./components/BoxTracker.vue";

export default defineComponent({
  name: "App",

  components: {
    SideBar,
    FormTodo,
    TaskTodo,
    BoxTracker,
  },

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
  --text-primary: #000;
}
main.dark-mode {
  --bg-primary: #2b2d42;
  --text-primary: #ddd;
}

.content {
  background-color: var(--bg-primary);
}
</style>