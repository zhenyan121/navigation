<template>
  <div class="root">
    <SakuraEffect />

    <header class="header">
      <h1 class="title">夢の栞</h1>
      <p class="subtitle">每一次刷新，都是一次新的邂逅</p>
    </header>

    <main class="content">
      <CategorySection
        v-for="cat in categories"
        :key="cat.id"
        :title="cat.title"
        :links="cat.links"
      />
    </main>

    <BilibiliPlayer />

    <footer class="footer">
      <p>于虚幻中寻得一方宁静</p>
      <p class="uptime">本站已稳定运行 {{ uptime }}</p>
    </footer>

    <a
      class="github-corner"
      href="https://github.com/zhenyan121/navigation"
      target="_blank"
      rel="noopener"
      title="GitHub"
    >
      <svg viewBox="0 0 24 24" width="22" height="22" fill="currentColor">
        <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/>
      </svg>
    </a>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import SakuraEffect from './components/SakuraEffect.vue'
import CategorySection from './components/CategorySection.vue'
import BilibiliPlayer from './components/BilibiliPlayer.vue'
import categories from './data/links.json'

const API = 'https://www.dmoe.cc/random.php'
const START = new Date('2026-04-30T23:13:05+08:00')

const uptime = ref('')
let timer = null

function tick() {
  const diff = Date.now() - START.getTime()
  const d = Math.floor(diff / 86400000)
  const h = Math.floor((diff % 86400000) / 3600000)
  const m = Math.floor((diff % 3600000) / 60000)
  uptime.value = `${d} 天 ${h} 小时 ${m} 分钟`
}

onMounted(() => {
  const url = `${API}?t=${Date.now()}`
  const probe = new Image()
  probe.onload = () => {
    document.body.style.backgroundImage = `url(${url})`
  }
  probe.onerror = () => {
    document.body.style.backgroundImage =
      'linear-gradient(135deg, #fbc2eb 0%, #ffd4e8 50%, #fff0f5 100%)'
  }
  probe.src = url

  tick()
  timer = setInterval(tick, 60000)
})

onUnmounted(() => {
  clearInterval(timer)
})
</script>

<style scoped>
.root {
  position: relative;
  z-index: 2;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 64px 24px 32px;
}

.header {
  text-align: center;
  margin-bottom: 48px;
}

.title {
  font-size: 2.5rem;
  font-weight: 700;
  color: #3E001D;
  text-shadow: 0 2px 16px rgba(255, 255, 255, 0.5);
  letter-spacing: 0.08em;
}

.subtitle {
  margin-top: 8px;
  font-size: 1rem;
  color: #5C4048;
  text-shadow: 0 1px 8px rgba(255, 255, 255, 0.5);
}

.content {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  width: 100%;
  max-width: 880px;
}

.footer {
  margin-top: auto;
  padding-top: 40px;
  font-size: 0.8rem;
  color: #8C7880;
  text-shadow: 0 1px 8px rgba(255, 255, 255, 0.5);
  text-align: center;
}

.uptime {
  margin-top: 6px;
  font-size: 0.85em;
  opacity: 0.85;
}

.github-corner {
  position: fixed;
  top: 16px;
  right: 16px;
  z-index: 10;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: var(--md-shape-full);
  background: rgba(255, 255, 255, 0.7);
  color: #333;
  transition: background 150ms ease, transform 150ms ease;
}

.github-corner:hover {
  background: rgba(255, 255, 255, 0.95);
  transform: scale(1.08);
}

@media (max-width: 600px) {
  .root {
    padding: 40px 16px 24px;
  }

  .title {
    font-size: 2rem;
  }

  .header {
    margin-bottom: 32px;
  }
}
</style>
