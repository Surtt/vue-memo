<script setup></script>

<template>
  <button class="btn"><slot /></button>
</template>

<style scoped>
.btn {
  border: none;
  font-family: var(--font);
  color: var(--inverted-main-text-color);
  font-size: 24px;
  fonte-weight: 400;
  line-height: 36px;
  padding: 16px 10px;
  border-radius: 100px;
  background-color: var(--primary-color);
  min-width: 315px;
  cursor: pointer;
}

.btn:hover {
  background-color: var(--primary-color-hover);
}
</style>
