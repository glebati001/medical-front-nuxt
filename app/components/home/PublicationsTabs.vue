<script setup lang="ts">
import { computed, ref, onMounted } from 'vue'
import { RouterLink } from 'vue-router'
import { usePublicationsDataStore } from '@/stores/publicationsData'

const store = usePublicationsDataStore()
onMounted(() => store.load())

const HOME_LIMIT = 8

const tab = ref<'article' | 'media'>('article')
const items = computed(() => store.items.filter((p) => p.type === tab.value).slice(0, HOME_LIMIT))
</script>

<template>
  <div>
    <div class="tabs">
      <button :class="{ active: tab === 'article' }" @click="tab = 'article'">Статьи</button>
      <button :class="{ active: tab === 'media' }" @click="tab = 'media'">СМИ о нас</button>
    </div>
    <div class="grid">
      <component
        v-for="p in items"
        :is="p.slug ? 'RouterLink' : 'article'"
        :key="p.id"
        :to="p.slug ? `/news/${p.slug}` : undefined"
        class="card"
      >
        <img :src="p.image" :alt="p.title" loading="lazy" />
        <div class="body">
          <time>{{ p.date }}</time>
          <h3>{{ p.title }}</h3>
          <p>{{ p.excerpt }}</p>
        </div>
      </component>
    </div>
    <div class="more">
      <RouterLink to="/news" class="more-link">
        {{ $t('home.blogShowAll') }}
        <svg viewBox="0 0 16 16" fill="none" aria-hidden="true">
          <path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
        </svg>
      </RouterLink>
    </div>
  </div>
</template>

<style scoped>
.tabs {
  display: flex;
  gap: var(--space-3);
  margin-bottom: var(--space-5);
  border-bottom: 1px solid var(--color-border);
}

.tabs button {
  padding: var(--space-3) var(--space-2);
  font-size: 16px;
  font-weight: 500;
  color: var(--color-text-muted);
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
}

.tabs button.active {
  color: var(--color-text);
  border-color: var(--color-primary);
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: var(--space-4);
}

.card {
  background: #fff;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: border-color 0.2s, transform 0.2s, box-shadow 0.2s;
  text-decoration: none;
  color: inherit;
}
a.card {
  cursor: pointer;
}

.card:hover {
  border-color: var(--color-primary);
  transform: translateY(-3px);
  box-shadow: var(--shadow);
}

.card img {
  width: 100%;
  aspect-ratio: 5/3;
  object-fit: cover;
}

.body {
  padding: var(--space-4);
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}

.body time {
  font-size: 12px;
  color: var(--color-text-muted);
  text-transform: uppercase;
  letter-spacing: 0.06em;
}

.body h3 {
  font-size: 16px;
  font-weight: 600;
  line-height: 1.35;
}

.body p {
  font-size: 14px;
  color: var(--color-text-muted);
  line-height: 1.5;
}

.more {
  margin-top: var(--space-5);
  display: flex;
  justify-content: center;
}

.more-link {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 12px 24px;
  font-size: 15px;
  font-weight: 500;
  color: var(--color-text);
  background: transparent;
  border: 1px solid var(--color-border-strong, #c8c2b6);
  border-radius: 999px;
  text-decoration: none;
  transition: background 0.2s, border-color 0.2s;
}

.more-link:hover {
  background: #fff;
  border-color: var(--color-text);
}

.more-link svg {
  width: 14px;
  height: 14px;
  transition: transform 0.2s;
}

.more-link:hover svg {
  transform: translateX(3px);
}
</style>
