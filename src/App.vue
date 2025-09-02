<script setup>
import { ref, provide } from "vue";
import { scoreProvide } from "./constants.js";
import Header from "./components/header.vue";
import Card from "./components/card.vue";
import Button from "./components/button.vue";

const gameStarted = ref(false);
const score = ref(0);
provide(scoreProvide, score);
const activeId = ref(null);

const API_URL = "http://localhost:8080/api/random-words";
const cards = ref([]);

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

const startGame = async () => {
	const response = await fetch(API_URL);
	const data = await response.json();
	cards.value = data.map((card, index) => ({
		...card,
		status: "pending",
		state: "closed",
		cardNumber: String(index + 1).padStart(2, "0"),
	}));
	gameStarted.value = true;
	activeId.value = null;
};
</script>

<template>
  <Header />
  <div v-if="gameStarted" class="gameWrapper">
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
    <Button @click="startGame">Начать заново</Button>
  </div>
  <div v-else class="button-wrapper">
    <Button @click="startGame">Начать игру</Button>
  </div>
</template>

<style scoped>
.cards-wrapper {
  display: grid;
  grid-template-columns: repeat(4, minmax(250px, 1fr));
  gap: 107px;
  padding: 0 62px;
}

.button-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.gameWrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 100px;
}
</style>
