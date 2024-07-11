<!-- src/components/CardModal.vue -->
<template>
    <div v-if="show" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content">
        <button class="close-button" @click="closeModal">X</button>
        <button class="arrow left" @click="prevCard">‹</button>
        <div class="card">
          {{ currentCard }}
        </div>
        <button class="arrow right" @click="nextCard">›</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed, defineProps, defineEmits, watch } from 'vue';
  
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
  
  const currentCard = computed(() => props.cards[currentIndex.value]);
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
    align-items: center;
    justify-content: center;
  }
  
  .card {
    max-width: 80vw; /* 卡片最大宽度占80%视口宽度 */
    max-height: 80vh; /* 卡片最大高度占80%视口高度 */
    width: 80vw;
    height: calc(80vw * 5 / 3); /* 保持长宽比 150:250 = 3:5 */
    max-height: 80vh;
    max-width: calc(80vh * 3 / 5); /* 保持长宽比 */
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    background-color: #fff;
    font-size: 48px;
  }
  
  .close-button, .arrow {
    position: absolute;
    background: none;
    border: none;
    font-size: 24px;
    cursor: pointer;
    z-index: 1;
  }
  
  .close-button {
    top: 0px;
    right: 0px;
  }
  
  .arrow.left {
    left: -40px; /* 确保箭头与卡片有一定的距离 */
    top: 50%;
    transform: translateY(-50%);
    font-size: 48px; /* 增大箭头按钮的字体大小 */
  }
  
  .arrow.right {
    right: -40px; /* 确保箭头与卡片有一定的距离 */
    top: 50%;
    transform: translateY(-50%);
    font-size: 48px; /* 增大箭头按钮的字体大小 */
  }
  </style>
  