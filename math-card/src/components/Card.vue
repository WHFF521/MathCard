<!-- src/components/Card.vue -->
<template>
    <div class="card" @click="handleClick">
      {{ number }}
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps({
    number: {
      type: Number,
      required: true
    }
  });
  
  const emits = defineEmits(['click']);
  
  const handleClick = () => {
    emits('click');
  };
  </script>
  
  <style scoped>
  .card {
    width: 150px; /* 卡片宽度 */
    height: 250px; /* 卡片高度 */
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    background-color: #fff;
    font-size: 24px;
    cursor: pointer;
  }
  </style>
  