<!-- src/components/CardModal.vue -->
<template>
  <div v-if="show" class="modal-overlay" @click.self="closeModal">
    <div class="modal-content">
      <button class="close-button" @click="closeModal">X</button>
      <div class="navigation">
        <button class="arrow left" @click="prevCard">‹</button>
        <div class="card" v-html="currentCardContent"></div>
        <button class="arrow right" @click="nextCard">›</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue';
import katex from 'katex';
import 'katex/dist/katex.min.css';

const props = defineProps({
  show: Boolean,
  cards: Array,
  initialIndex: Number,
});

const emits = defineEmits(['close']);

const currentIndex = ref(props.initialIndex);

const closeModal = () => {
  emits('close');
};

const prevCard = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--;
  }
};

const nextCard = () => {
  if (currentIndex.value < props.cards.length - 1) {
    currentIndex.value++;
  }
};

watch(() => props.initialIndex, (newIndex) => {
  currentIndex.value = newIndex;
});

const renderFormula = (formula) => {
  return katex.renderToString(formula, {
    throwOnError: false,
  });
};

const currentCardContent = computed(() => {
  if (props.cards.length > 0) {
    return renderFormula(props.cards[currentIndex.value].formula);
  }
  return '';
});
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  position: relative;
  background: white;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.card {
  width: calc(80vh * 5 / 3); /* 固定宽度 */
  height: 80vh; /* 固定高度 */
  max-width: 80vw;
  max-height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  background-color: #fff;
  font-size: 48px;
}

/* 响应式设计 */
@media (max-width: 767px) {
  .card {
    width: 90vw; /* 调整手机上的卡片宽度 */
    height: 60vh; /* 调整手机上的卡片高度 */
    font-size: 24px; /* 调整手机上的字体大小 */
  }
}

.close-button {
  align-self: flex-end;
  background: none;
  border: none;
  cursor: pointer;
  font-size: 24px;
  margin-bottom: 10px;
}

.navigation {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.arrow {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 48px;
  margin: 0 20px;
}

/* 响应式设计 */
@media (max-width: 767px) {
  .arrow {
    font-size: 24px; /* 调整手机上的箭头大小 */
    margin: 0 10px; /* 调整箭头位置 */
  }
}
</style>
