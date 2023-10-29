<template>
  <div class="fab-container">
    <button 
      class="fab-button" 
      @click="toggleFab"
      :style="{ backgroundColor: computedColor }" 
    >
      <i class="material-icons">add</i>
    </button>
    <transition-group name="list" tag="div">
      <template v-for="action in fabActions" :key="action.name">
        <button 
          class="fab-action" 
          @click="handleClick(action)"
          v-if="showFab"
          :style="{ backgroundColor: computedColor }" 
        >
          <i class="material-icons">{{ action.icon }}</i>
        </button>
      </template>
    </transition-group>
  </div>
</template>

<script setup>
import { ref, computed, defineProps } from 'vue'

const props = defineProps({
  color: String,
  fabActions: Array, 
});

const showFab = ref(false);

const toggleFab = () => {
  console.log('toggleFab');
  showFab.value = !showFab.value;
};


const colors = {
  rainbow: '#00BF63', 
  red: '#FF0000',
  orange: '#FF7F00',
  yellow: '#FFFF00',
  green: '#00FF00',
  blue: '#0000FF',
  indigo: '#4B0082',
  violet: '#9400D3'
};

const computedColor = computed(() => {
  if (/^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/.test(props.color)) {
    return props.color;
  }
  return colors[props.color] || colors.rainbow;
});

const handleClick = (action) => {
  if (action && action.action && typeof action.action === 'function') {
    action.action();
  }
  
  console.log(`${action.name} clicked`);
  toggleFab();
};
</script>

<style>
.fab-container {
  position: fixed;
  bottom: 1em;
  right: 1em;
  display: flex;
  flex-direction: column-reverse;
  align-items: flex-end;
}
.fab-button,
.fab-action {
    border: none;
    width: 56px;
    height: 56px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 0px 2px 10px 0px rgba(0, 0, 0, 0.15);
    transition: transform 0.3s ease-in-out;
    color: white;
    font-size: 24px;
    margin-top: 10px;
    cursor: pointer;
  background: none;
}

.fab-button {
  transform: scale(1);
}

.fab-action {
  transition: transform 0.3s ease-in-out;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease-in-out;
}

.list-enter-from,
.list-leave-to {
  transform: translateY(20px);
  opacity: 0;
}

.list-enter-to,
.list-leave-from {
  transform: translateY(0);
  opacity: 1;
}

.bg {
  background-color: #00BF63;
  height: 50px; 
  position: sticky;
  top: 0;
  z-index: 999;
  width: 1000px;
}

@font-face {
  font-family: 'Material Icons';
  font-style: normal;
  font-weight: 400;
  src: url(https://fonts.gstatic.com/s/materialicons/v140/flUhRq6tzZclQEJ-Vdg-IuiaDsNZ.ttf) format('truetype');
}

.material-icons {
  font-family: 'Material Icons';
  font-weight: normal;
  font-style: normal;
  font-size: 24px;
  line-height: 1;
  letter-spacing: normal;
  text-transform: none;
  display: inline-block;
  white-space: nowrap;
  word-wrap: normal;
  direction: ltr;
}
</style>
