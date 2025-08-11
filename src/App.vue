<script setup>
const date = new Date().toLocaleString("ru", { hour12: false });
</script>

<template>
  <div>{{ date }}</div>
</template>

<style scoped></style>
