<script setup>
import { ref } from "vue";
import Header from "./components/header.vue";
import Card from "./components/card.vue";
import Button from "./components/button.vue";
const date = new Date().toLocaleString("ru", { hour12: false });
const activeId = ref(null);

const cards = ref([
	{
		cardNumber: "06",
		word: "apple",
		translation: "яблоко",
		state: "closed",
		status: "pending",
	},
	{
		cardNumber: "07",
		word: "banana",
		translation: "банан",
		state: "closed",
		status: "pending",
	},
	{
		cardNumber: "08",
		word: "orange",
		translation: "апельсин",
		state: "closed",
		status: "pending",
	},
	{
		cardNumber: "09",
		word: "lemon",
		translation: "лимон",
		state: "closed",
		status: "pending",
	},
]);

const handleToggleFlip = (cardNumber) => {
	if (activeId.value === cardNumber) {
		activeId.value = null;
	} else {
		activeId.value = cardNumber;
	}
};

const changeStatus = (cardNumber, v) => {
	cards.value.find((card) => card.cardNumber === cardNumber).status = v;
};
</script>

<template>
  <Header />
  <div class="cards-wrapper">
    <Card
      v-for="card in cards"
      :key="card.cardNumber"
      v-bind="card"
      :is-flipped="card.cardNumber === activeId"
      @toggle-flip="handleToggleFlip(card.cardNumber)"
      @change-status="changeStatus(card.cardNumber, $event)"
    />
  </div>
  <div>{{ date }}</div>
  <Button>Начать игру</Button>
</template>

<style scoped>
.cards-wrapper {
  display: flex;
  gap: 20px;
}
</style>
