<script setup lang="ts">
import { computed } from 'vue'
import { RouterLink } from 'vue-router'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const features = computed(() => [
  { icon: 'supply', label: t('home.hero.features.supply') },
  { icon: 'equipment', label: t('home.hero.features.equipment') },
  { icon: 'support', label: t('home.hero.features.support') },
  { icon: 'turnkey', label: t('home.hero.features.turnkey') },
])

const metrics = computed(() => [
  { value: '100+', label: t('home.hero.metrics.projects') },
  { value: '50+', label: t('home.hero.metrics.partners') },
  { value: '24/7', label: t('home.hero.metrics.service') },
])
</script>

<template>
  <section class="hero">
    <div class="backdrop">
      <NuxtImg
        src="/hero.png"
        :alt="$t('home.hero.imageAlt')"
        width="1983"
        height="793"
        sizes="xs:100vw sm:100vw md:100vw lg:100vw xl:100vw xxl:1983px"
        format="webp"
        quality="85"
        loading="eager"
        fetchpriority="high"
        decoding="async"
      />
    </div>
    <div class="scrim" aria-hidden="true"></div>

    <div class="inner">
      <div class="copy">
        <span class="tagline">{{ $t('home.hero.tagline') }}</span>
        <h1>
          {{ $t('home.hero.titleMain') }}
          <span class="accent">{{ $t('home.hero.titleAccent') }}</span>
        </h1>
        <p class="lead">{{ $t('home.hero.lead') }}</p>
        <RouterLink to="/contacts" class="cta">
          {{ $t('home.hero.cta') }}
          <svg viewBox="0 0 16 16" fill="none" aria-hidden="true">
            <path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
          </svg>
        </RouterLink>
      </div>

      <ul class="features">
        <li v-for="f in features" :key="f.icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
            <g v-if="f.icon === 'supply'">
              <path d="M12 3l7.5 2.8v5.5c0 4.2-3.1 7.5-7.5 9.2-4.4-1.7-7.5-5-7.5-9.2V5.8L12 3z" />
              <path d="M8.8 12.1l2.2 2.2 4.2-4.4" />
            </g>
            <g v-else-if="f.icon === 'equipment'">
              <path d="M12.2 2.4h-.4a1.9 1.9 0 00-1.9 1.9v.2a1.9 1.9 0 01-1 1.6l-.4.3a1.9 1.9 0 01-1.9 0l-.2-.1a1.9 1.9 0 00-2.6.7l-.2.4a1.9 1.9 0 00.7 2.6l.2.1a1.9 1.9 0 011 1.6v.5a1.9 1.9 0 01-1 1.7l-.2.1a1.9 1.9 0 00-.7 2.6l.2.4a1.9 1.9 0 002.6.7l.2-.1a1.9 1.9 0 011.9 0l.4.3a1.9 1.9 0 011 1.6v.2a1.9 1.9 0 001.9 1.9h.4a1.9 1.9 0 001.9-1.9v-.2a1.9 1.9 0 011-1.6l.4-.3a1.9 1.9 0 011.9 0l.2.1a1.9 1.9 0 002.6-.7l.2-.4a1.9 1.9 0 00-.7-2.6l-.2-.1a1.9 1.9 0 01-1-1.7v-.5a1.9 1.9 0 011-1.6l.2-.1a1.9 1.9 0 00.7-2.6l-.2-.4a1.9 1.9 0 00-2.6-.7l-.2.1a1.9 1.9 0 01-1.9 0l-.4-.3a1.9 1.9 0 01-1-1.6v-.2a1.9 1.9 0 00-1.9-1.9z" />
              <circle cx="12" cy="12" r="2.7" />
            </g>
            <g v-else-if="f.icon === 'support'">
              <circle cx="9.2" cy="8.4" r="3.1" />
              <circle cx="17" cy="9.6" r="2.2" />
              <path d="M3.4 19.4c0-3.1 2.6-5.2 5.8-5.2s5.8 2.1 5.8 5.2" />
              <path d="M16.2 14.4c2.6.3 4.4 2.2 4.4 4.8" />
            </g>
            <g v-else>
              <path d="M3.2 20.6h17.6" />
              <path d="M5.4 20.6V6.6a1.2 1.2 0 011.2-1.2h10.8a1.2 1.2 0 011.2 1.2v14" />
              <path d="M12 8.4v4.6M9.7 10.7h4.6" />
              <path d="M9.6 20.6v-4.2h4.8v4.2" />
            </g>
          </svg>
          <span>{{ f.label }}</span>
        </li>
      </ul>
    </div>

    <div class="metrics-echo" aria-hidden="true"></div>
    <ul class="metrics">
      <li v-for="m in metrics" :key="m.label">
        <span class="value">{{ m.value }}</span>
        <span class="metric-label">{{ m.label }}</span>
      </li>
    </ul>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  border-radius: var(--radius-lg);
  border: 1px solid var(--color-border);
  background: var(--color-surface);
  min-height: clamp(480px, 44vw, 620px);
  display: flex;
  flex-direction: column;
}

.backdrop {
  position: absolute;
  inset: 0;
  z-index: -2;
}

.backdrop img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 72% 50%;
}

.scrim {
  position: absolute;
  inset: 0;
  z-index: -1;
  background:
    linear-gradient(
      96deg,
      rgba(249, 248, 245, 0.97) 0%,
      rgba(249, 248, 245, 0.95) 34%,
      rgba(249, 248, 245, 0.86) 46%,
      rgba(249, 248, 245, 0.5) 58%,
      rgba(249, 248, 245, 0.14) 70%,
      rgba(249, 248, 245, 0) 84%
    ),
    linear-gradient(180deg, rgba(249, 248, 245, 0.45) 0%, rgba(249, 248, 245, 0) 34%);
}

.inner {
  position: relative;
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: var(--space-7);
  padding: clamp(var(--space-6), 3.4vw, var(--space-8));
}

.copy {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  max-width: 640px;
  min-width: 0;
}

.tagline {
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.16em;
  line-height: 1.5;
  text-transform: uppercase;
  color: var(--color-primary);
}

h1 {
  font-family: var(--font-sans);
  font-size: clamp(30px, 4.1vw, 54px);
  line-height: 1.08;
  letter-spacing: -0.03em;
  font-weight: 700;
  color: var(--color-text);
  margin: var(--space-4) 0 0;
  max-width: 16ch;
}

.accent {
  display: block;
  color: var(--color-primary);
}

.lead {
  margin-top: var(--space-4);
  font-size: clamp(15px, 1.2vw, 18px);
  line-height: 1.6;
  color: var(--color-text-muted);
  max-width: 34ch;
}

.cta {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  margin-top: var(--space-6);
  padding: 14px 28px;
  font-size: 15px;
  font-weight: 600;
  color: #fff;
  background: var(--color-primary);
  border-radius: 999px;
  box-shadow: 0 10px 26px rgba(26, 79, 156, 0.28);
  transition: background 0.2s, box-shadow 0.2s, transform 0.2s;
}

.cta:hover {
  background: var(--color-primary-dark);
  box-shadow: 0 14px 32px rgba(15, 53, 119, 0.32);
  transform: translateY(-1px);
}

.cta svg {
  width: 15px;
  height: 15px;
  transition: transform 0.2s;
}

.cta:hover svg {
  transform: translateX(3px);
}

.features {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  max-width: min(52%, 640px);
}

.features li {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 0 clamp(10px, 1vw, 14px);
  min-width: 0;
}

.features li:first-child {
  padding-left: 0;
}

.features li + li {
  border-left: 1px solid rgba(11, 25, 41, 0.14);
}

.features svg {
  flex: none;
  width: 22px;
  height: 22px;
  color: var(--color-primary);
}

.features span {
  font-size: 11px;
  font-weight: 500;
  line-height: 1.35;
  color: var(--color-text);
  max-width: 13ch;
}

.metrics,
.metrics-echo {
  position: absolute;
  right: 0;
  bottom: 0;
  border-top-left-radius: 24% 100%;
}

.metrics-echo {
  width: min(56%, 700px);
  height: clamp(160px, 22vw, 240px);
  background: rgba(26, 79, 156, 0.12);
  transform: translate(-26px, 0);
}

.metrics {
  width: min(46%, 580px);
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  padding: clamp(var(--space-5), 2.4vw, var(--space-6)) clamp(var(--space-4), 2vw, var(--space-5))
    clamp(var(--space-5), 2.4vw, var(--space-6)) clamp(var(--space-7), 6vw, 88px);
  background: linear-gradient(112deg, #0f3577 0%, #1a4f9c 100%);
  color: #fff;
}

.metrics li {
  display: flex;
  flex-direction: column;
  gap: 6px;
  padding: 0 clamp(var(--space-3), 1.2vw, var(--space-4));
  min-width: 0;
}

.metrics li:first-child {
  padding-left: 0;
}

.metrics li + li {
  border-left: 1px solid rgba(255, 255, 255, 0.22);
}

.value {
  font-size: clamp(24px, 2.6vw, 38px);
  font-weight: 700;
  letter-spacing: -0.02em;
  line-height: 1;
}

.metric-label {
  font-size: 13px;
  line-height: 1.35;
  color: rgba(255, 255, 255, 0.82);
}

@media (max-width: 1200px) {
  .hero {
    min-height: 0;
  }

  .metrics-echo {
    display: none;
  }

  .metrics {
    position: static;
    width: 100%;
    border-top-left-radius: 0;
    padding: var(--space-6) clamp(var(--space-5), 3.4vw, var(--space-7));
  }

  .features {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: var(--space-4) var(--space-5);
    max-width: 520px;
  }

  .features li,
  .features li:first-child {
    padding: 0;
  }

  .features li + li {
    border-left: 0;
  }

  .features svg {
    width: 24px;
    height: 24px;
  }

  .features span {
    font-size: 13px;
    max-width: none;
  }
}

@media (max-width: 900px) {
  .backdrop img {
    object-position: 66% 40%;
  }

  .scrim {
    background:
      linear-gradient(
        170deg,
        rgba(249, 248, 245, 0.97) 0%,
        rgba(249, 248, 245, 0.9) 42%,
        rgba(249, 248, 245, 0.55) 66%,
        rgba(249, 248, 245, 0.2) 100%
      );
  }

  h1 {
    max-width: 20ch;
  }

  .features {
    max-width: 460px;
  }

  .features svg {
    width: 26px;
    height: 26px;
  }
}

@media (max-width: 640px) {
  .inner {
    gap: var(--space-6);
    padding: var(--space-6) var(--space-5);
  }

  .tagline {
    font-size: 11px;
    letter-spacing: 0.12em;
  }

  .accent {
    display: inline;
  }

  .lead {
    max-width: none;
  }

  .cta {
    align-self: stretch;
    justify-content: center;
  }

  .metrics {
    grid-template-columns: 1fr;
    gap: var(--space-4);
    padding: var(--space-5);
  }

  .metrics li {
    flex-direction: row;
    align-items: baseline;
    gap: var(--space-4);
    padding: 0;
  }

  .metrics li + li {
    border-left: 0;
    border-top: 1px solid rgba(255, 255, 255, 0.2);
    padding-top: var(--space-4);
  }

  .value {
    flex: none;
    min-width: 3.4em;
  }
}
</style>
