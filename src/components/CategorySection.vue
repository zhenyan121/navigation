<template>
  <div class="category-card">
    <h3 class="category-heading">{{ title }}</h3>
    <ul class="category-links">
      <li v-for="link in links" :key="link.url">
        <a
          :href="link.url"
          target="_blank"
          rel="noopener"
          class="link-chip"
        >
          <span class="chip-label">{{ link.label }}</span>
          <span class="chip-trailing">↗</span>
        </a>
      </li>
    </ul>
  </div>
</template>

<script setup>
defineProps({
  title: { type: String, required: true },
  links: { type: Array, required: true },
})
</script>

<style scoped>
.category-card {
  flex: 1 1 180px;
  min-width: 160px;
  background: var(--md-surface);
  border-radius: var(--md-shape-lg);
  padding: 20px;
  box-shadow: var(--md-elevation-1);
  transition: box-shadow 200ms ease, transform 200ms ease;
}

.category-card:hover {
  box-shadow: var(--md-elevation-2);
  transform: translateY(-2px);
}

.category-heading {
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--md-on-surface);
  padding-bottom: 10px;
  margin-bottom: 14px;
  border-bottom: 2px solid var(--md-primary);
  letter-spacing: 0.02em;
}

.category-links {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.link-chip {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  text-decoration: none;
  color: var(--md-on-surface-variant);
  background: var(--md-surface-variant);
  padding: 8px 16px;
  border-radius: var(--md-shape-full);
  font-size: 0.875rem;
  font-weight: 500;
  transition: background 150ms ease, color 150ms ease, box-shadow 150ms ease;
  width: 100%;
}

.link-chip:hover {
  background: var(--md-primary-container);
  color: var(--md-on-primary-container);
  box-shadow: var(--md-elevation-1);
}

.link-chip:active {
  transform: scale(0.97);
}

.chip-trailing {
  margin-left: auto;
  font-size: 0.8em;
  opacity: 0.4;
}

@media (max-width: 600px) {
  .category-card {
    padding: 16px;
  }
}
</style>
