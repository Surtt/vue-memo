<script setup>
import IconHeart from "../icons/icon-heart.vue";
const { score } = defineProps({
	score: String,
});
</script>

<template>
  <div class="score">{{ score }}<IconHeart /></div>
</template>

<style scoped>
.score {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  width: 110px;
  padding: 12px 24px;
  color: var(--primary-color);
  font-weight: 700;
  line-height: 24px;
  background-color: var(--secondary-color);
  border-radius: 36px;
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
}
</style>
