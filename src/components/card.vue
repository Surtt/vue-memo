<script setup>
import IconWrong from "../icons/icon-wrong.vue";
import IconSuccess from "../icons/icon-success.vue";

const props = defineProps({
	cardNumber: String,
	word: String,
	translation: String,
	state: String,
	status: String,
	isFlipped: Boolean,
});
const emit = defineEmits({
	toggleFlip: null,
	changeStatus: (v) => v === "success" || v === "fail",
});

const toggleFlip = () => emit("toggleFlip");

const markRight = () => emit("changeStatus", "success");

const markWrong = () => emit("changeStatus", "fail");
</script>

<template>
  <div
    class="card"
    :class="[
      { 'is-flipped': props.isFlipped },
      props.status === 'success'
        ? 'is-success'
        : props.status === 'fail'
          ? 'is-fail'
          : '',
    ]"
  >
    <div class="card-inner">
      <div class="face front">
        <div class="card-number">{{ props.cardNumber }}</div>
        <div class="word">{{ props.word }}</div>
        <button class="flip-btn" type="button" @click="toggleFlip">
          Перевернуть
        </button>
      </div>

      <div class="face back">
        <div class="card-number">{{ props.cardNumber }}</div>
        <div class="answer">
          <IconWrong v-if="props.status === 'fail'" width="39" height="39" />
          <IconSuccess
            v-else-if="props.status === 'success'"
            width="39"
            height="39"
          />
        </div>
        <div class="word">{{ props.translation }}</div>
        <div class="btns">
          <button class="wrong-btn" type="button" @click="markWrong">
            <IconWrong />
          </button>
          <button class="success-btn" type="button" @click="markRight">
            <IconSuccess />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  perspective: 1000px;
  position: relative;
  width: 250px;
  height: 376px;
  border-radius: 16px;
  box-shadow: 0 0 16px 0 rgba(0, 0, 0, 0.1);
  background-color: var(--inverted-main-text-color);
  padding: 28px 19px;
}

.card-inner {
  transform-style: preserve-3d;
  transition: transform 0.8s;
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: 12px;
  border: 1px solid var(--secondary-color);
}

.card.is-flipped .card-inner {
  transform: rotateY(180deg);
}

.face {
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  backface-visibility: hidden;
}

.back {
  transform: rotateY(180deg);
}

.card-number {
  position: absolute;
  font-size: 14px;
  padding: 2px;
  background-color: var(--inverted-main-text-color);
  top: -10px;
  left: 10px;
}

.flip-btn {
  position: absolute;
  font-weight: 700;
  font-size: 12px;
  text-transform: uppercase;
  line-height: 18px;
  letter-spacing: 0.12em;
  padding: 4px;
  background-color: var(--inverted-main-text-color);
  bottom: -12px;
  left: 50%;
  transform: translateX(-50%);
  border: none;
}

.btns {
  position: absolute;
  bottom: -12px;
  display: flex;
  justify-content: space-between;
  gap: 32px;
  background-color: var(--inverted-main-text-color);
  padding: 0 10px;
}

.wrong-btn,
.success-btn {
  border: none;
  background-color: transparent;
  cursor: pointer;
}

.answer {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
