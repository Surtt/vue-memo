<script setup>
import { ref } from "vue";
import Header from "./components/header.vue";
import Card from "./components/card.vue";
import Button from "./components/button.vue";
const date = new Date().toLocaleString("ru", { hour12: false });
const isFlipped = ref(false);

const handleToggleFlip = () => {
	isFlipped.value = !isFlipped.value;
};

const changeStatus = (v) => {
	console.log("Статус изменился", v);
};
</script>

<template>
  <Header />
  <Card
    card-number="06"
    front-word="apple"
    back-word="яблоко"
    :is-flipped="isFlipped"
    @toggle-flip="handleToggleFlip"
    @change-status="changeStatus"
  />
  <div>{{ date }}</div>
  <Button>Начать игру</Button>
</template>

<style scoped></style>
