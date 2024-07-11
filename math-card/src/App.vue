<!-- src/App.vue -->
<template>
  <div class="outer-container">
    <div class="card-container">
      <Card v-for="(card, index) in cards" :key="index" :name="card.name" @click="openModal(index)" />
    </div>
    <CardModal v-if="showModal" :show="showModal" :cards="cards" :initialIndex="currentCardIndex" @close="closeModal" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Card from './components/Card.vue';
import CardModal from './components/CardModal.vue';

const cards = ref([]);
const showModal = ref(false);
const currentCardIndex = ref(0);

const fetchCards = async () => {
  try {
    const response = await fetch('/src/assets/formulas.json');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    cards.value = await response.json();
  } catch (error) {
    console.error('Error loading cards:', error);
  }
};

const openModal = (index) => {
  currentCardIndex.value = index;
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
};

onMounted(() => {
  fetchCards();
});
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
  grid-template-columns: repeat(6, 1fr);
  gap: 20px;
  justify-content: center;
  width: 100%;
  max-width: 1200px; /* 你可以根据需要调整 */
  margin: 0 auto; /* 使卡片容器在父容器中居中 */
}
</style>
