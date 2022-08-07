<template>
  <header>
    <h1>
      <img src="" alt="" />
    </h1>
    <button class="button" @click="changeTheme">{{ textButton }}</button>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "SideBar",
  emits: ["toThemeChanged"],
  data() {
    return {
      activeDarkMode: false,
    };
  },

  computed: {
    textButton() {
      if (this.activeDarkMode) {
        return "Desativar modo escuro";
      }
      return "Ativar modo escuro";
    },
  },

  methods: {
    changeTheme() {
      this.activeDarkMode = !this.activeDarkMode;
      this.$emit("toThemeChanged", this.activeDarkMode);
    },
  },
});
</script>

<style>
header {
  padding: 1rem;
  background: #0d3b66;
  width: 100%;
  height: 100vh;
  text-align: center;
}
@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>