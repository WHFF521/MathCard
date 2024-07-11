<template>
  <div class="card" @click="handleClick">
    <div class="type-label" :style="{ backgroundColor: props.color }">{{ props.type }}</div>
    <div>{{ englishName }}</div>
    <div>{{ chineseName }}</div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, computed } from 'vue';

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  type: {
    type: String,
    required: true
  },
  color: {
    type: String,
    required: true,
    default: '#4789f5' // 默认颜色值
  }
});

const emits = defineEmits(['click']);

const handleClick = () => {
  emits('click');
};

// 使用计算属性来分割传入的名称字符串
const englishName = computed(() => props.name.split(' | ')[0]);
const chineseName = computed(() => props.name.split(' | ')[1]);
</script>

<style scoped>
.card {
  width: 100%; /* 确保卡片在网格系统中自适应宽度 */
  height: 250px; /* 卡片高度 */
  display: flex;
  flex-direction: column; /* 垂直布局 */
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
  position: relative; /* 为标签定位 */
}

.type-label {
  position: absolute; /* 绝对定位 */
  top: 10px; /* 距离顶部 */
  left: 10px; /* 距离左侧 */
  color: #fff; /* 标签文字颜色 */
  padding: 5px 10px; /* 标签内边距 */
  border-radius: 4px; /* 标签圆角 */
  font-size: 14px; /* 标签文字大小 */
}
</style>
