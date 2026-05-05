<template>
  <section class="player-section">
    <h2 class="player-heading">追番</h2>

    <div class="player-wrapper">
      <iframe
        :src="`https://player.bilibili.com/player.html?ep_id=${current}&autoplay=0`"
        scrolling="no"
        frameborder="0"
        allowfullscreen
        class="player-frame"
      ></iframe>
    </div>

    <div class="episode-bar">
      <button
        v-for="ep in episodes"
        :key="ep.id"
        :class="['ep-chip', { active: current === ep.id }]"
        @click="current = ep.id"
      >
        {{ ep.label }}
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const baseStart = 35595
const baseEnd = 35624
const special = 278737

const episodes = [
  ...Array.from({ length: baseEnd - baseStart + 1 }, (_, i) => ({
    id: baseStart + i,
    label: `第${i + 1}集`,
  })),
  { id: special, label: 'SP' },
]

const current = ref(baseStart)
</script>

<style scoped>
.player-section {
  width: 100%;
  max-width: 720px;
  margin-top: 40px;
}

.player-heading {
  font-size: 1.1rem;
  font-weight: 600;
  color: #3E001D;
  text-shadow: 0 1px 8px rgba(255, 255, 255, 0.5);
  margin-bottom: 14px;
  text-align: center;
}

.player-wrapper {
  position: relative;
  width: 100%;
  padding-top: 56.25%;
  border-radius: var(--md-shape-lg);
  overflow: hidden;
  box-shadow: var(--md-elevation-2);
  background: #000;
}

.player-frame {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  border: 0;
}

.episode-bar {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 12px;
  justify-content: center;
}

.ep-chip {
  padding: 5px 12px;
  border-radius: var(--md-shape-full);
  border: 1px solid var(--md-outline);
  background: var(--md-surface);
  color: var(--md-on-surface);
  font-size: 0.8rem;
  font-weight: 500;
  cursor: pointer;
  transition: background 150ms ease, color 150ms ease, border-color 150ms ease;
  font-family: inherit;
}

.ep-chip:hover {
  background: var(--md-primary-container);
  color: var(--md-on-primary-container);
  border-color: var(--md-primary);
}

.ep-chip.active {
  background: var(--md-primary);
  color: var(--md-on-primary);
  border-color: var(--md-primary);
}

@media (max-width: 600px) {
  .player-section {
    margin-top: 32px;
  }

  .ep-chip {
    padding: 4px 10px;
    font-size: 0.75rem;
  }
}
</style>
