<script setup>
import { ref, computed, onMounted } from "vue";
import Header from "./components/header.vue";
import Card from "./components/card.vue";
import Button from "./components/button.vue";
const date = new Date().toLocaleString("ru", { hour12: false });
const activeId = ref(null);

const API_URL = "http://localhost:8080/api/random-words";
const cards = ref([]);

onMounted(async () => {
	const response = await fetch(API_URL);
	const data = await response.json();
	cards.value = data.map((card, index) => ({
		...card,
		status: "pending",
		state: "closed",
		cardNumber: String(index + 1).padStart(2, "0"),
	}));
});

const handleToggleFlip = (cardNumber) => {
	if (activeId.value === cardNumber) {
		activeId.value = null;
	} else {
		activeId.value = cardNumber;
	}
};

const changeStatus = (cardNumber, v) => {
	const item = cards.value.find((card) => card.cardNumber === cardNumber);
	if (item) item.status = v;
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
  display: grid;
  grid-template-columns: repeat(4, minmax(250px, 1fr));
  gap: 107px;
  padding: 0 62px;
}
</style>
