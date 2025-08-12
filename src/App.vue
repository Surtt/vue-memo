<script setup>
import Button from "./components/button.vue";
const date = new Date().toLocaleString("ru", { hour12: false });
</script>

<template>
  <div>{{ date }}</div>
  <Button>Начать игру</Button>
</template>

<style scoped></style>
