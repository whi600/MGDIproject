<script setup>
import featuredPoster from '../../assets/service-video-poster.jpg'

defineProps({
  lead: {
    type: String,
    default: 'Кадры и короткие эпизоды, где видно живую динамику команды и реальные шаги служения.'
  },
  cards: {
    type: Array,
    required: true
  },
  parallaxShift: {
    type: Number,
    default: 0
  }
})
</script>

<template>
  <section id="moments" class="moments section-block">
    <div class="container">
      <p class="section-kicker dark">Моменты</p>
      <h2 class="section-title moments-title">Сцены, где ощущается движение служения</h2>
      <p class="moments-lead">{{ lead }}</p>

      <div class="featured-media" :style="{ transform: `translateY(${-parallaxShift * 0.55}px)` }">
        <img :src="featuredPoster" alt="Кадр приветственного видео проекта" class="featured-poster" loading="lazy" />
        <div class="featured-overlay" aria-hidden="true"></div>
        <div class="featured-caption">
          <span class="orbit-chip">Видео</span>
          <strong>Приветственное слово и атмосфера команды</strong>
        </div>
      </div>

      <div class="slider-row" tabindex="0" aria-label="Галерея моментов">
        <article
          v-for="item in cards"
          :key="item.title"
          class="slider-card"
          :style="{ '--thumb-image': `url(${item.image})` }"
        >
          <div class="slider-thumb"></div>
          <p>{{ item.title }}</p>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.moments {
  position: relative;
  overflow: hidden;
  --surface-border: 1px solid rgba(16, 26, 51, 0.14);
  --surface-radius: var(--radius-lg);
  --surface-shadow: var(--shadow-soft);
  background-color: #ece8de;
}

.moments::before,
.moments::after {
  content: '';
  position: absolute;
  border-radius: 999px;
  pointer-events: none;
}

.moments::before {
  width: clamp(300px, 32vw, 460px);
  height: clamp(300px, 32vw, 460px);
  left: -14%;
  top: 18%;
  background: radial-gradient(circle, rgba(191, 211, 90, 0.11), rgba(191, 211, 90, 0) 74%);
}

.moments::after {
  width: clamp(220px, 24vw, 340px);
  height: clamp(220px, 24vw, 340px);
  right: -14%;
  bottom: 14%;
  background: radial-gradient(circle, rgba(255, 98, 51, 0.09), rgba(255, 98, 51, 0) 74%);
}

.moments .container {
  position: relative;
  z-index: 1;
}

.moments-title {
  max-width: 15ch;
  letter-spacing: -0.012em;
  line-height: 0.98;
  font-size: clamp(1.95rem, 4.8vw, 4.35rem);
  text-wrap: balance;
}

.moments-lead {
  margin: 14px 0 0;
  max-width: 760px;
  color: #44516d;
  line-height: 1.58;
  text-wrap: pretty;
}

.featured-media {
  margin-top: 26px;
  position: relative;
  border-radius: var(--surface-radius);
  overflow: hidden;
  min-height: 420px;
  border: var(--surface-border);
  box-shadow: var(--surface-shadow);
  transition: transform 0.25s ease;
}

.featured-poster {
  min-height: 420px;
  object-fit: cover;
  object-position: center;
  transform: scale(1.03);
}

.featured-overlay {
  position: absolute;
  inset: 0;
  background:
    linear-gradient(180deg, rgba(5, 10, 24, 0.16), rgba(5, 10, 24, 0.62)),
    radial-gradient(circle at 72% 22%, rgba(255, 98, 51, 0.2), rgba(255, 98, 51, 0));
}

.featured-caption {
  position: absolute;
  left: 20px;
  bottom: 20px;
  right: 20px;
  display: grid;
  gap: 10px;
  color: var(--white);
}

.featured-caption strong {
  font-size: clamp(1rem, 2.2vw, 1.45rem);
  font-weight: 700;
  line-height: 1.35;
  text-shadow: 0 8px 20px rgba(0, 0, 0, 0.32);
}

.slider-row {
  margin-top: 22px;
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: minmax(230px, 1fr);
  gap: 16px;
  overflow-x: auto;
  padding: 10px;
  border-radius: var(--surface-radius);
  border: var(--surface-border);
  background: linear-gradient(165deg, rgba(255, 255, 255, 0.58) 0%, rgba(255, 255, 255, 0.3) 100%);
  box-shadow: var(--surface-shadow);
  padding-bottom: 10px;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.slider-row:focus-visible {
  outline: 2px solid rgba(17, 70, 216, 0.68);
  outline-offset: 3px;
}

.slider-row::-webkit-scrollbar {
  display: none;
}

.slider-card {
  border-radius: var(--radius-md);
  overflow: hidden;
  background: var(--white);
  box-shadow: var(--shadow-soft);
  border: var(--surface-border);
  scroll-snap-align: start;
  transition: transform 0.25s ease;
}

.slider-card:hover {
  transform: translateY(-4px);
}

.slider-thumb {
  height: 154px;
  background-image: linear-gradient(180deg, rgba(6, 11, 24, 0.08), rgba(6, 11, 24, 0.34)), var(--thumb-image);
  background-size: cover;
  background-position: center;
}

.slider-card p {
  margin: 0;
  padding: 12px;
  font-weight: 700;
  color: #1a223a;
}

@media (max-width: 900px) {
  .moments::before {
    left: -26%;
  }

  .moments::after {
    right: -30%;
  }

  .featured-media,
  .featured-poster {
    min-height: 280px;
  }

  .slider-row {
    grid-auto-columns: minmax(190px, 1fr);
    padding: 10px;
  }
}

@media (max-width: 640px) {
  .moments-title {
    max-width: 13ch;
    font-size: clamp(1.72rem, 8.2vw, 2.6rem);
    line-height: 1;
  }
}

@media (prefers-reduced-motion: reduce) {
  .featured-media {
    transform: none !important;
    transition: none;
  }

  .slider-card {
    transition: none;
  }

  .slider-card:hover {
    transform: none;
  }
}
</style>
