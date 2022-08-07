<template>
  <div class="box form">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        aria-label="Formulário para a criação de uma nova tarefa."
      >
        <input
          type="text"
          class="input"
          placeholder="Qual tarefa você deseja iniciar ?"
          v-model="description"
        />
      </div>
      <div class="column">
        <DelayerTodo @toTimerEnded="finishTask" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import DelayerTodo from "@/components/DelayerTodo.vue";

export default defineComponent({
  name: "FormTodo",
  emits: ["onSaveTask"],
  components: {
    DelayerTodo,
  },

  data() {
    return {
      description: "",
    };
  },

  methods: {
    finishTask(elapsedTime: number): void {
      this.$emit("onSaveTask", {
        durationInSeconds: elapsedTime,
        description: this.description,
      });
      this.description = "";
    },
  },
});
</script>

<style>
.form {
  color: var(--text-primary);
  background-color: var(--bg-primary);
}
</style>