<script setup>
import { ref } from "vue";
import Score from "./score.vue";
const score = ref(100);
</script>

<template>
  <header class="header">
    <a class="logo">Запомни слово</a>
    <Score :score />
  </header>
</template>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 1440px;
  height: 121px;
  padding: 37px 62px;
  background-color: transparent;
}

.logo {
  font-weight: 700;
  line-height: 24px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}
</style>
