<template>
  <section class="player-section">
    <h2 class="player-heading">追番 · 幸运星</h2>

    <div class="player-wrapper">
      <iframe
        v-if="playerUrl"
        :key="playerUrl"
        :src="playerUrl"
        allowfullscreen
        class="player-frame"
      ></iframe>
    </div>

    <div class="episode-bar">
      <button
        v-for="ep in episodes"
        :key="ep.id"
        :class="['ep-chip', { active: current === ep.id }]"
        @click="selectEp(ep)"
      >
        {{ ep.label }}
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const episodes = [
  { id: 59846708, cid: 104236640, label: '第1话' },
  { id: 934255758, cid: 104236735, label: '第2话' },
  { id: 976767921, cid: 104236899, label: '第3话' },
  { id: 976855059, cid: 104237054, label: '第4话' },
  { id: 634289470, cid: 104237144, label: '第5话' },
  { id: 379307519, cid: 104237246, label: '第6话' },
  { id: 591853944, cid: 104237560, label: '第7话' },
  { id: 591850815, cid: 104237744, label: '第8话' },
  { id: 591854585, cid: 104238021, label: '第9话' },
  { id: 806813018, cid: 104238146, label: '第10话' },
  { id: 934290922, cid: 104238278, label: '第11话' },
  { id: 891823944, cid: 104238448, label: '第12话' },
  { id: 806809838, cid: 104238631, label: '第13话' },
  { id: 421799841, cid: 104239072, label: '第14话' },
  { id: 721841903, cid: 104239373, label: '第15话' },
  { id: 719307234, cid: 104239579, label: '第16话' },
  { id: 294305033, cid: 104239784, label: '第17话' },
  { id: 934266977, cid: 104239964, label: '第18话' },
  { id: 934323356, cid: 104240224, label: '第19话' },
  { id: 379343867, cid: 104240673, label: '第20话' },
  { id: 379351237, cid: 104240906, label: '第21话' },
  { id: 719294454, cid: 104241185, label: '第22话' },
  { id: 764317388, cid: 104241304, label: '第23话' },
  { id: 806780385, cid: 105397332, label: '第24话' },
  { id: 209342384, cid: 104241808, label: 'OVA' },
]

const current = ref(episodes[0].id)

const playerUrl = computed(() => {
  const ep = episodes.find((e) => e.id === current.value)
  if (!ep) return ''
  return `https://player.bilibili.com/player.html?aid=${ep.id}&cid=${ep.cid}&page=1&autoplay=0`
})

function selectEp(ep) {
  current.value = ep.id
}
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
