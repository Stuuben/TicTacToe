<script setup lang="ts">
import TickTacToe from "./components/TickTacToe.vue";
</script>

<template>
  <TickTacToe></TickTacToe>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

#app {
  display: flex;
  justify-content: center;
  background-color: red;
}
</style>
