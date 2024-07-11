<!-- src/App.vue -->
<template>
  <div class="outer-container">
    <div class="card-container">
      <Card v-for="(number, index) in cards" :key="number" :number="number" @click="openModal(index)" />
    </div>
    <CardModal v-if="showModal" :show="showModal" :cards="cards" :initialIndex="currentCardIndex" @close="closeModal" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';
import CardModal from './components/CardModal.vue';

const cards = ref(Array.from({ length: 30 }, (_, i) => i + 1));
const showModal = ref(false);
const currentCardIndex = ref(0);

const openModal = (index) => {
  currentCardIndex.value = index;
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
};
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
  width: max-content;
}
</style>
