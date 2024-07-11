<!-- src/App.vue -->
<template>
  <div class="outer-container">
    <div class="card-container">
      <Card v-for="number in cards" :key="number" :number="number" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';

const cards = ref(Array.from({ length: 30 }, (_, i) => i + 1));
</script>

<style>
.outer-container {
  display: flex;
  justify-content: center;
  padding: 20px;
  width: 100%;
}

.card-container {
  display: grid;
  grid-template-columns: repeat(6, 150px);
  gap: 20px;
  justify-content: center;
  width: max-content; /* 确保卡片容器根据内容宽度动态调整 */
}
</style>
