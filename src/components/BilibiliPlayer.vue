<template>
  <section class="player-section">
    <h2 class="player-heading">追番</h2>

    <div class="player-wrapper">
      <template v-if="loading">
        <div class="player-placeholder">加载中…</div>
      </template>
      <template v-else-if="playerUrl">
        <iframe
          :src="playerUrl"
          allow="autoplay; encrypted-media"
          allowfullscreen
          sandbox="allow-scripts allow-same-origin allow-popups"
          class="player-frame"
        ></iframe>
      </template>
      <template v-else>
        <div class="player-placeholder">无法加载播放器</div>
      </template>
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
import { ref, computed, onMounted } from 'vue'

const API_BASE = 'https://api.bilibili.com/pgc/view/web/season?ep_id='

const episodes = ref([])
const epMap = ref({})
const current = ref(0)
const loading = ref(true)

const playerUrl = computed(() => {
  const ep = epMap.value[current.value]
  if (!ep) return ''
  return `https://player.bilibili.com/player.html?aid=${ep.aid}&cid=${ep.cid}&page=1&autoplay=0`
})

function selectEp(ep) {
  current.value = ep.id
}

async function fetchSeason(epId) {
  try {
    const res = await fetch(`${API_BASE}${epId}`)
    const data = await res.json()
    if (data.code !== 0 || !data.result) return

    const list = data.result.episodes || []
    for (const ep of list) {
      if (epMap.value[ep.id]) continue
      epMap.value[ep.id] = {
        aid: ep.aid,
        cid: ep.cid,
      }
      episodes.value.push({
        id: ep.id,
        label: ep.title || `第${ep.episode || '?'}集`,
      })
    }
    if (list.length > 0 && !current.value) {
      current.value = list[0].id
    }
  } catch {
    // ignore
  } finally {
    loading.value = false
  }
}

onMounted(async () => {
  await fetchSeason(35595)
  await fetchSeason(278737)
})
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

.player-placeholder {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.9rem;
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
