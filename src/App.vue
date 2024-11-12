<script setup lang="ts">
import SlotMachine from './components/SlotMachine.vue'
</script>

<template>
  <div class="container">
    <h1>Lucky Slots! 🎰</h1>
    <SlotMachine />
  </div>
</template>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  padding: 2rem;
}

h1 {
  color: #ffd700;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}
</style>