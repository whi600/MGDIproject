<script setup>
import { computed, ref } from 'vue'
import RussiaMap from '../ui/russia-map/RussiaMap.vue'

const props = defineProps({
  label: {
    type: String,
    default: 'География'
  },
  title: {
    type: String,
    default: 'География проекта МГДИ'
  },
  description: {
    type: String,
    default: 'Кликни по региону на карте или выбери город из списка справа.'
  },
  ctaText: {
    type: String,
    default: 'Открыть проект в новом регионе'
  },
  ctaUrl: {
    type: String,
    default: '#final'
  }
})

const cities = Object.freeze([
  {
    id: 'cherepovets',
    name: 'Череповец',
    regionCode: 'VLG',
    regionName: 'Вологодская область'
  },
  {
    id: 'perm',
    name: 'Пермь',
    regionCode: 'PER',
    regionName: 'Пермский край'
  },
  {
    id: 'omsk',
    name: 'Омск',
    regionCode: 'OMS',
    regionName: 'Омская область'
  },
  {
    id: 'krasnoyarsk',
    name: 'Красноярск',
    regionCode: 'KYA',
    regionName: 'Красноярский край'
  }
])

const selectedRegion = ref('PER')
const hoveredRegion = ref(null)

const activeRegions = computed(() => [...new Set(cities.map((city) => city.regionCode))])

const cityByRegion = computed(() => {
  return Object.fromEntries(cities.map((city) => [city.regionCode, city]))
})

const selectedCity = computed(() => cityByRegion.value[selectedRegion.value] ?? null)

const currentRegion = computed(() => {
  if (hoveredRegion.value) {
    return hoveredRegion.value
  }

  if (selectedCity.value) {
    return {
      code: selectedCity.value.regionCode,
      name: selectedCity.value.regionName
    }
  }

  return null
})

function handleRegionClick(region) {
  selectedRegion.value = region.code

  console.info('[map_city_click]', {
    city: cityByRegion.value[region.code]?.name ?? null,
    region: region.name,
    code: region.code
  })
}

function handleRegionHover(region) {
  hoveredRegion.value = region
}

function selectCity(city) {
  selectedRegion.value = city.regionCode
}

function highlightCity(city) {
  hoveredRegion.value = {
    code: city.regionCode,
    name: city.regionName
  }
}

function clearCityHighlight() {
  hoveredRegion.value = null
}
</script>

<template>
  <section id="4geogrf" class="geo section-block" data-block-name="4geogrf">
    <div class="container geo-shell">
      <p class="section-kicker dark geo-kicker">{{ props.label }}</p>
      <h2 class="section-title geo-title">{{ props.title }}</h2>
      <p class="geo-lead">{{ props.description }}</p>

      <div class="geo-layout">
        <div class="geo-map-card g-frame-sm">
          <RussiaMap
            class-name="geo-map"
            :selected-region="selectedRegion"
            :active-regions="activeRegions"
            @region-click="handleRegionClick"
            @region-hover="handleRegionHover"
          />
        </div>

        <aside class="geo-side-card">
          <p class="geo-side-title">Города на карте</p>

          <ul class="geo-city-list">
            <li v-for="city in cities" :key="city.id">
              <button
                type="button"
                class="geo-city-item"
                :class="{ 'is-active': city.regionCode === selectedRegion }"
                @click="selectCity(city)"
                @mouseenter="highlightCity(city)"
                @mouseleave="clearCityHighlight"
              >
                <span class="geo-city-name">{{ city.name }}</span>
                <span class="geo-city-region">{{ city.regionName }}</span>
              </button>
            </li>
          </ul>

          <div class="geo-current" v-if="currentRegion">
            <p class="geo-current-label">Сейчас выбран регион</p>
            <p class="geo-current-name">{{ currentRegion.name }}</p>
          </div>

          <a class="btn btn-primary btn-small geo-cta" :href="props.ctaUrl">{{ props.ctaText }}</a>
        </aside>
      </div>
    </div>
  </section>
</template>

<style scoped>
.geo {
  position: relative;
  overflow: hidden;
  --surface-border: 1px solid rgba(16, 26, 51, 0.14);
  --surface-radius: var(--radius-lg);
  --surface-shadow: var(--shadow-soft);
  background-color: #ece8de;
}

.geo::before,
.geo::after {
  content: '';
  position: absolute;
  border-radius: 999px;
  pointer-events: none;
}

.geo::before {
  width: clamp(300px, 30vw, 460px);
  height: clamp(300px, 30vw, 460px);
  top: 16%;
  right: -14%;
  background: radial-gradient(circle, rgba(255, 98, 51, 0.1), rgba(255, 98, 51, 0) 74%);
}

.geo::after {
  width: clamp(240px, 24vw, 360px);
  height: clamp(240px, 24vw, 360px);
  left: -10%;
  bottom: 18%;
  background: radial-gradient(circle, rgba(191, 211, 90, 0.12), rgba(191, 211, 90, 0) 74%);
}

.geo-shell {
  position: relative;
  z-index: 1;
}

.geo-kicker {
  letter-spacing: 0.34em;
  color: rgba(16, 25, 51, 0.68);
}

.geo-title {
  max-width: 880px;
  color: #101a35;
  text-wrap: balance;
}

.geo-lead {
  margin: 14px 0 24px;
  max-width: 720px;
  color: #44516d;
  line-height: 1.58;
  text-wrap: pretty;
}

.geo-layout {
  display: grid;
  grid-template-columns: minmax(0, 1.35fr) minmax(280px, 0.65fr);
  gap: 18px;
  align-items: start;
}

.geo-map-card {
  position: relative;
  border-radius: var(--surface-radius);
  border: var(--surface-border);
  background: linear-gradient(165deg, rgba(255, 255, 255, 0.9) 0%, rgba(244, 248, 255, 0.9) 100%);
  box-shadow: var(--surface-shadow);
  padding: clamp(14px, 2vw, 24px);
}

.geo-map {
  width: 100%;
}

.geo-side-card {
  border-radius: var(--surface-radius);
  border: var(--surface-border);
  background:
    linear-gradient(160deg, rgba(255, 255, 255, 0.93) 0%, rgba(248, 250, 255, 0.92) 100%),
    radial-gradient(circle at 84% 12%, rgba(17, 70, 216, 0.06), rgba(17, 70, 216, 0) 38%);
  box-shadow: var(--surface-shadow);
  padding: 18px;
}

.geo-side-title {
  margin: 0;
  font-family: 'Dela Gothic One', sans-serif;
  font-weight: 400;
  font-size: 1.02rem;
  color: #15244a;
  text-transform: uppercase;
  letter-spacing: 0.06em;
}

.geo-city-list {
  list-style: none;
  margin: 14px 0 0;
  padding: 0;
  display: grid;
  gap: 8px;
}

.geo-city-item {
  width: 100%;
  min-height: 44px;
  text-align: left;
  border-radius: 12px;
  border: 1px solid rgba(16, 26, 51, 0.14);
  background: rgba(255, 255, 255, 0.82);
  padding: 10px 12px;
  display: grid;
  gap: 3px;
  cursor: pointer;
  transition: border-color 0.2s ease, background 0.2s ease, transform 0.2s ease;
}

.geo-city-item:hover {
  transform: translateY(-1px);
  border-color: rgba(17, 70, 216, 0.4);
  background: rgba(255, 255, 255, 0.95);
}

.geo-city-item:focus-visible {
  outline: 2px solid rgba(17, 70, 216, 0.72);
  outline-offset: 2px;
  border-color: rgba(17, 70, 216, 0.58);
  background: rgba(255, 255, 255, 0.96);
}

.geo-city-item.is-active {
  border-color: rgba(17, 70, 216, 0.56);
  background: rgba(17, 70, 216, 0.08);
}

.geo-city-name {
  font-weight: 700;
  color: #122349;
}

.geo-city-region {
  font-size: 0.8rem;
  color: #5a6782;
}

.geo-current {
  margin-top: 14px;
  padding: 10px 12px;
  border-radius: 12px;
  background: rgba(17, 70, 216, 0.08);
  border: 1px solid rgba(17, 70, 216, 0.2);
}

.geo-current-label {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.68rem;
  color: #5b6885;
}

.geo-current-name {
  margin: 4px 0 0;
  color: #112248;
  font-weight: 700;
}

.geo-cta {
  margin-top: 14px;
  width: 100%;
}

.geo-cta:focus-visible {
  outline: 2px solid rgba(17, 70, 216, 0.72);
  outline-offset: 3px;
}

@media (max-width: 980px) {
  .geo::before {
    top: 22%;
    right: -22%;
  }

  .geo::after {
    left: -24%;
  }

  .geo-layout {
    grid-template-columns: 1fr;
  }

  .geo-side-card {
    max-width: 620px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .geo-city-item {
    transition: none;
  }

  .geo-city-item:hover {
    transform: none;
  }
}
</style>
