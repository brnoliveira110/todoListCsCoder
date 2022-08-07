<template>
  <BoxTracker>
    <div class="columns">
      <div class="column is-7">
        {{ task.description || "Tarefa sem descrição" }}
      </div>
      <div class="column">
        <TimerTodo :timeInSeconds="task.durationInSeconds" />
      </div>
    </div>
  </BoxTracker>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import TimerTodo from "./TimerTodo.vue";
import ITask from "../interfaces/ITask";
import BoxTracker from "./BoxTracker.vue";

export default defineComponent({
  name: "TaskTodo",
  components: {
    TimerTodo,
    BoxTracker,
  },
  props: {
    task: {
      type: Object as PropType<ITask>,
      required: true,
    },
  },
});
</script>