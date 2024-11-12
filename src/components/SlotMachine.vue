<script setup lang="ts">
import { ref } from 'vue';

const symbols = ['🍀', '⭐', '💎', '🎰', '7️⃣'];
const slots = ref(['🍀', '🍀', '🍀']);
const isSpinning = ref(false);
const handlePosition = ref(0);

const spin = () => {
  if (isSpinning.value) return;
  
  handlePosition.value = 30;
  isSpinning.value = true;
  
  // Simulate spinning animation
  const duration = 2000;
  const intervals = 100;
  const spinInterval = setInterval(() => {
    slots.value = slots.value.map(() => symbols[Math.floor(Math.random() * symbols.length)]);
  }, 100);

  // Stop spinning after duration
  setTimeout(() => {
    clearInterval(spinInterval);
    isSpinning.value = false;
    handlePosition.value = 0;
    
    // Generate final result
    slots.value = slots.value.map(() => symbols[Math.floor(Math.random() * symbols.length)]);
  }, duration);
};
</script>

<template>
  <div class="slot-machine">
    <div class="machine-frame">
      <div class="slot-display" :class="{ spinning: isSpinning }">
        <div v-for="(symbol, index) in slots" :key="index" class="slot">
          {{ symbol }}
        </div>
      </div>
      <div 
        class="handle" 
        :style="{ transform: `translateY(${handlePosition}px)` }"
        @click="spin"
      >
        🎮
      </div>
    </div>
  </div>
</template>

<style scoped>
.slot-machine {
  background: linear-gradient(45deg, #2a0e37, #440e37);
  border-radius: 20px;
  padding: 2rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.machine-frame {
  background: #gold;
  border: 8px solid #ffd700;
  border-radius: 15px;
  padding: 2rem;
  position: relative;
  display: flex;
  align-items: center;
}

.slot-display {
  display: flex;
  gap: 1rem;
  background: white;
  padding: 2rem;
  border-radius: 10px;
  margin-right: 4rem;
}

.slot {
  font-size: 3rem;
  width: 80px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f0f0f0;
  border-radius: 8px;
  border: 2px solid #ddd;
}

.spinning .slot {
  animation: blur 0.2s infinite;
}

.handle {
  position: absolute;
  right: 1rem;
  font-size: 3rem;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.handle:hover {
  transform: translateY(5px);
}

@keyframes blur {
  0% { filter: blur(0); }
  50% { filter: blur(2px); }
  100% { filter: blur(0); }
}
</style>