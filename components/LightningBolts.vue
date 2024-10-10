<template>
  <div class="lightning-container">
    <div v-for="i in 3" :key="i" class="lightning" :class="`bolt-${i}`"></div>
  </div>
</template>

<style scoped>
.lightning-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.lightning {
  position: absolute;
  background: #fff;
  width: 2px;
  height: 0;
  top: 0;
  opacity: 0;
  transform: translateX(-50%);
}

@keyframes lightning {
  0% { opacity: 0; height: 0; }
  20% { opacity: 1; height: 20%; }
  25% { opacity: 0; height: 20%; }
  30% { opacity: 1; height: 40%; }
  35% { opacity: 0; height: 40%; }
  40% { opacity: 1; height: 60%; }
  45% { opacity: 0; height: 60%; }
  50% { opacity: 1; height: 80%; }
  55% { opacity: 0; height: 80%; }
  60% { opacity: 1; height: 100%; }
  100% { opacity: 0; height: 100%; }
}

.bolt-1 {
  left: 20%;
  animation: lightning 3s infinite;
}

.bolt-2 {
  left: 50%;
  animation: lightning 2.5s 0.5s infinite;
}

.bolt-3 {
  left: 80%;
  animation: lightning 3.5s 0.7s infinite;
}
</style>