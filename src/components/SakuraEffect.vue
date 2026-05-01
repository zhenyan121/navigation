<template>
  <div class="sakura-wrap" aria-hidden="true">
    <span
      v-for="p in petals"
      :key="p.id"
      class="petal"
      :style="{
        left: p.left,
        animationDuration: p.duration,
        animationDelay: p.delay,
        width: p.size,
        height: p.size,
      }"
    ></span>
  </div>
</template>

<script setup>
const petals = Array.from({ length: 25 }, (_, i) => ({
  id: i,
  left: Math.random() * 100 + '%',
  duration: Math.random() * 5 + 6 + 's',
  delay: Math.random() * 5 + 's',
  size: Math.random() * 15 + 10 + 'px',
}))
</script>

<style scoped>
.sakura-wrap {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
  overflow: hidden;
}

.petal {
  position: absolute;
  top: -10vh;
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Cpath fill='%23ffb7c5' d='M50 0 C55 20 80 20 90 40 C80 60 55 70 50 90 C45 70 20 60 10 40 C20 20 45 20 50 0Z'/%3E%3C/svg%3E") no-repeat center/contain;
  opacity: 0.75;
  animation: sakura-fall linear infinite;
}

@keyframes sakura-fall {
  from {
    transform: translateY(-10vh) rotate(0deg);
    opacity: 0.85;
  }
  to {
    transform: translateY(110vh) rotate(720deg);
    opacity: 0;
  }
}
</style>
