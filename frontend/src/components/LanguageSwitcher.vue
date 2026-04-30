<template>
  <div class="language-switcher" ref="switcherRef">
    <button class="switcher-trigger" @click="toggleDropdown">
      {{ currentLabel }}
      <span class="caret">{{ open ? '▲' : '▼' }}</span>
    </button>
    <ul v-if="open" class="switcher-dropdown">
      <li
        v-for="loc in availableLocales"
        :key="loc.key"
        class="switcher-option"
        :class="{ active: loc.key === locale }"
        @click="switchLocale(loc.key)"
      >
        {{ loc.label }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { useI18n } from 'vue-i18n'
import { availableLocales } from '@/i18n/index.js'

const { locale } = useI18n()
const open = ref(false)
const switcherRef = ref(null)

const currentLabel = computed(() => {
  const found = availableLocales.find(l => l.key === locale.value)
  return found ? found.label : locale.value
})

const toggleDropdown = () => {
  open.value = !open.value
}

const switchLocale = (key) => {
  locale.value = key
  localStorage.setItem('locale', key)
  document.documentElement.lang = key
  open.value = false
}

const onClickOutside = (e) => {
  if (switcherRef.value && !switcherRef.value.contains(e.target)) {
    open.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', onClickOutside)
  document.documentElement.lang = locale.value
})

onUnmounted(() => {
  document.removeEventListener('click', onClickOutside)
})
</script>

<style scoped>
.language-switcher {
  position: relative;
  display: inline-block;
}

.switcher-trigger {
  background: transparent;
  color: rgba(255, 255, 255, 0.75);
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 6px 16px;
  border-radius: 100px;
  font-family: 'Manrope', Arial, sans-serif;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: all 0.2s;
  white-space: nowrap;
}

.switcher-trigger:hover {
  color: #ffffff;
  border-color: rgba(255, 255, 255, 0.5);
  background: rgba(255, 255, 255, 0.08);
}

.caret {
  font-size: 0.6rem;
  opacity: 0.6;
}

.switcher-dropdown {
  position: absolute;
  top: calc(100% + 8px);
  right: 0;
  background: rgba(20, 20, 35, 0.95);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 12px;
  list-style: none;
  padding: 6px;
  min-width: 130px;
  z-index: 1000;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
}

.switcher-option {
  padding: 8px 14px;
  font-family: 'Manrope', Arial, sans-serif;
  font-size: 14px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.65);
  cursor: pointer;
  white-space: nowrap;
  border-radius: 8px;
  transition: all 0.15s;
}

.switcher-option:hover {
  background: rgba(255, 255, 255, 0.08);
  color: #ffffff;
}

.switcher-option.active {
  color: #45d0bd;
  background: rgba(69, 208, 189, 0.1);
}
</style>
