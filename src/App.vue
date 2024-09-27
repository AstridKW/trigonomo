<template>
  <div id="menu-container" @click="showMenu($event)">
    <button
      v-for="(item, index) in menuItems"
      :key="index"
      v-if="isMenuActive"
      class="menu-item"
      :style="getItemPosition(index)"
      @click.stop="action(item)"
    >
      {{ item }}
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const radius = 200; // Radius from the click position

// State for menu activation and position
const isMenuActive = ref(false);
const position = ref({ x: 0, y: 0 });

// Menu items list (can be updated dynamically)
const menuItems = ref(['Apple', 'Banana', 'Kiwi', 'Grape', 'Papaya', 'Orange']); // Add or remove items here

// Function to show the menu and set position
const showMenu = (event) => {
  position.value = { x: event.clientX, y: event.clientY };
  isMenuActive.value = !isMenuActive.value;
};

// Function to get the style of each item based on its index
const getItemPosition = (index) => {
  const angle = (2 * Math.PI * index) / menuItems.value.length; // Calculate angle based on item count

  const xOffset = Math.cos(angle) * radius;
  const yOffset = Math.sin(angle) * radius;

  return {
    top: `${position.value.y + yOffset - 20}px`, // Adjust to center the button
    left: `${position.value.x + xOffset - 40}px`, // Adjust to center the button
  };
};

// Action function when a menu item is clicked
const action = (item) => {
  alert(`Selected: ${item}`);
  isMenuActive.value = false; // Close the menu after selection
};
</script>

<style scoped>
#menu-container {
  width: 100vw;
  height: 100vh;
  position: relative;
  overflow: hidden;
}

.menu-item {
  position: absolute;
  width: 80px;
  height: 40px;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  background-color: #000000;
  border: 1px solid #ccc;
  transition: transform 0.2s;
}

.menu-item:hover {
  transform: scale(1.1);
}
</style>
