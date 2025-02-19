<!-- src/App.vue -->
<template>
  <div>
    <header class="header">
      <h1>数学公式展示</h1>
    </header>
    <div class="outer-container">
      <div class="card-container">
        <Card 
        v-for="(card, index) in cards" 
        :key="index" 
        :name="card.name" 
        :type="card.type" 
        :color="card.color"
        @click="openModal(index)" />
      </div>
      <CardModal v-if="showModal" :show="showModal" :cards="cards" :initialIndex="currentCardIndex" @close="closeModal" />
    </div>
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
    const response = await fetch('/formulas.json');
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
.header {
  background-color: #f8f9fa;
  padding: 20px;
  text-align: center;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

.header h1 {
  margin: 0;
  font-size: 24px;
  font-weight: 600;
}

.outer-container {
  display: flex;
  justify-content: center;
  padding: 20px;
  width: 100%;
}

.card-container {
  display: grid;
  gap: 20px;
  justify-content: center;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

/* 响应式设计 */
@media (min-width: 1200px) {
  .card-container {
    grid-template-columns: repeat(6, 1fr);
  }
}

@media (max-width: 1199px) and (min-width: 992px) {
  .card-container {
    grid-template-columns: repeat(4, 1fr);
  }
}

@media (max-width: 991px) and (min-width: 768px) {
  .card-container {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 767px) and (min-width: 576px) {
  .card-container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 575px) {
  .card-container {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
