<script setup>
import { ref } from "vue";
import Header from "./components/header.vue";
import Card from "./components/card.vue";
import Button from "./components/button.vue";
const date = new Date().toLocaleString("ru", { hour12: false });
const isFlipped = ref(false);

const card = ref({
	cardNumber: "06",
	word: "apple",
	translation: "яблоко",
	state: "closed",
	status: "pending",
});

const handleToggleFlip = () => {
	isFlipped.value = !isFlipped.value;
	card.value.state = "opened";
};

const changeStatus = (v) => {
	card.value.status = v;
};
</script>

<template>
  <Header />
  <Card
    v-bind="card"
    :is-flipped="isFlipped"
    @toggle-flip="handleToggleFlip"
    @change-status="changeStatus"
  />
  <div>{{ date }}</div>
  <Button>Начать игру</Button>
</template>

<style scoped></style>
