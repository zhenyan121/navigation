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

    <div class="player-actions">
      <a
        :href="bilibiliUrl"
        target="_blank"
        rel="noopener"
        class="ext-link"
      >在 B 站打开</a>
    </div>

    <div class="episode-bar">
      <button
        v-for="ep in episodes"
        :key="ep.aid"
        :class="['ep-chip', { active: current === ep.aid }]"
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
  { aid: 59846708, cid: 105396981, bvid: 'BV13t411n7ex', ep: 35595, label: '第1话' },
  { aid: 934255758, cid: 104236735, bvid: 'BV1tT4y1R7Ji', ep: 35596, label: '第2话' },
  { aid: 976767921, cid: 104236899, bvid: 'BV1144y1a75d', ep: 35597, label: '第3话' },
  { aid: 976855059, cid: 104237054, bvid: 'BV1W44y1Y735', ep: 35598, label: '第4话' },
  { aid: 634289470, cid: 104237144, bvid: 'BV1Fb4y1b7JW', ep: 35599, label: '第5话' },
  { aid: 379307519, cid: 104237246, bvid: 'BV1xf4y1M7Lg', ep: 35600, label: '第6话' },
  { aid: 591853944, cid: 104237560, bvid: 'BV1mq4y167LV', ep: 35601, label: '第7话' },
  { aid: 591850815, cid: 104237744, bvid: 'BV11q4y1671P', ep: 35602, label: '第8话' },
  { aid: 591854585, cid: 104238021, bvid: 'BV1mq4y167HS', ep: 35604, label: '第9话' },
  { aid: 806813018, cid: 104238146, bvid: 'BV1Q34y1d76i', ep: 35606, label: '第10话' },
  { aid: 934290922, cid: 104238278, bvid: 'BV1CM4y1A7hB', ep: 35608, label: '第11话' },
  { aid: 891823944, cid: 104238448, bvid: 'BV1rP4y1G7do', ep: 35611, label: '第12话' },
  { aid: 806809838, cid: 104238631, bvid: 'BV1X34y1d7bD', ep: 35613, label: '第13话' },
  { aid: 421799841, cid: 104239072, bvid: 'BV183411t7Ls', ep: 35614, label: '第14话' },
  { aid: 721841903, cid: 104239373, bvid: 'BV1FS4y1R7KS', ep: 35615, label: '第15话' },
  { aid: 719307234, cid: 104239579, bvid: 'BV1BQ4y1U7r8', ep: 35616, label: '第16话' },
  { aid: 294305033, cid: 104239784, bvid: 'BV1DF411h7EC', ep: 35617, label: '第17话' },
  { aid: 934266977, cid: 104239964, bvid: 'BV1HT4y1R7e9', ep: 35618, label: '第18话' },
  { aid: 934323356, cid: 104240224, bvid: 'BV19M4y1A73e', ep: 35619, label: '第19话' },
  { aid: 379343867, cid: 104240673, bvid: 'BV1df4y1N7UC', ep: 35620, label: '第20话' },
  { aid: 379351237, cid: 104240906, bvid: 'BV1ff4y1N7cr', ep: 35621, label: '第21话' },
  { aid: 719294454, cid: 104241185, bvid: 'BV1kQ4y1U7mB', ep: 35622, label: '第22话' },
  { aid: 764317388, cid: 104241304, bvid: 'BV1vr4y1k7p3', ep: 35623, label: '第23话' },
  { aid: 806780385, cid: 105397332, bvid: 'BV1r34y1d7Rs', ep: 35624, label: '第24话' },
  { aid: 209342384, cid: 104241808, bvid: 'BV1Wh41147dA', ep: 278737, label: 'OVA' },
]

const current = ref(episodes[0].aid)

const playerUrl = computed(() => {
  const ep = episodes.find((e) => e.aid === current.value)
  if (!ep) return ''
  return `https://player.bilibili.com/player.html?aid=${ep.aid}&autoplay=0`
})

const bilibiliUrl = computed(() => {
  const ep = episodes.find((e) => e.aid === current.value)
  if (!ep) return '#'
  return `https://www.bilibili.com/bangumi/play/ep${ep.ep}`
})

function selectEp(ep) {
  current.value = ep.aid
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

.player-actions {
  display: flex;
  justify-content: flex-end;
  margin-top: 8px;
}

.ext-link {
  font-size: 0.8rem;
  color: var(--md-primary);
  text-decoration: none;
  font-weight: 500;
  padding: 4px 12px;
  border-radius: var(--md-shape-full);
  background: var(--md-primary-container);
  transition: background 150ms ease;
}

.ext-link:hover {
  background: var(--md-primary);
  color: var(--md-on-primary);
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
