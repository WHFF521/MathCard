<!-- src/components/Card.vue -->
<template>
    <div class="card" @click="handleClick">
      {{ name }}
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps({
    name: {
      type: String,
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
    width: 100%; /* 确保卡片在网格系统中自适应宽度 */
    height: 250px; /* 卡片高度 */
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    background-color: #fff;
    font-size: 18px;
    cursor: pointer;
    text-align: center;
    padding: 10px;
    box-sizing: border-box; /* 确保内边距和边框在卡片内计算 */
  }
  </style>
  