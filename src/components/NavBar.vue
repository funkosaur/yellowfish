<template>
  <nav class="navbar" role="navigation" aria-label="Main navigation">
    <div class="navbar__pill">
      <!-- Animated active background indicator -->
      <div
        class="navbar__indicator"
        :style="indicatorStyle"
        aria-hidden="true"
      >
        <div class="navbar__glow">
          <div class="navbar__glow-bar"></div>
          <div class="navbar__glow-blur navbar__glow-blur--wide"></div>
          <div class="navbar__glow-blur navbar__glow-blur--medium"></div>
          <div class="navbar__glow-blur navbar__glow-blur--narrow"></div>
        </div>
      </div>

      <a
        v-for="item in navItems"
        :key="item.name"
        :href="item.url"
        :ref="(el) => setItemRef(item.name, el)"
        class="navbar__link"
        :class="{ 'navbar__link--active': activeTab === item.name }"
        :aria-current="activeTab === item.name ? 'page' : undefined"
        @click.prevent="handleClick(item)"
      >
        <span class="navbar__label">{{ item.name }}</span>
        <component :is="item.icon" class="navbar__icon" :size="18" :stroke-width="2.5" />
      </a>
    </div>
  </nav>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted, nextTick } from 'vue'
import { Home, User, Code2, Briefcase, FolderGit2, Heart, Mail } from 'lucide-vue-next'

const navItems = [
  { name: 'Home', url: '#hero', icon: Home },
  { name: 'About', url: '#about', icon: User },
  { name: 'Skills', url: '#skills', icon: Code2 },
  { name: 'Experience', url: '#experience', icon: Briefcase },
  { name: 'Projects', url: '#projects', icon: FolderGit2 },
  { name: 'Values', url: '#values', icon: Heart },
  { name: 'Contact', url: '#contact', icon: Mail },
]

const activeTab = ref('Home')
const itemRefs = reactive({})
const indicatorStyle = ref({})

function setItemRef(name, el) {
  if (el) {
    itemRefs[name] = el
  }
}

function updateIndicator() {
  const activeEl = itemRefs[activeTab.value]
  if (!activeEl) return

  const pill = activeEl.parentElement
  const pillRect = pill.getBoundingClientRect()
  const activeRect = activeEl.getBoundingClientRect()

  indicatorStyle.value = {
    width: `${activeRect.width}px`,
    transform: `translateX(${activeRect.left - pillRect.left}px)`,
  }
}

function handleClick(item) {
  activeTab.value = item.name
  nextTick(updateIndicator)

  const target = document.querySelector(item.url)
  if (target) {
    target.scrollIntoView({ behavior: 'smooth' })
  }
}

// Track which section is in view
function handleScroll() {
  const sections = navItems.map((item) => ({
    name: item.name,
    el: document.querySelector(item.url),
  })).filter((s) => s.el)

  const scrollY = window.scrollY + window.innerHeight / 3

  for (let i = sections.length - 1; i >= 0; i--) {
    if (sections[i].el.offsetTop <= scrollY) {
      if (activeTab.value !== sections[i].name) {
        activeTab.value = sections[i].name
        nextTick(updateIndicator)
      }
      break
    }
  }
}

let resizeObserver = null

onMounted(() => {
  nextTick(updateIndicator)
  window.addEventListener('scroll', handleScroll, { passive: true })
  window.addEventListener('resize', updateIndicator, { passive: true })

  // Watch for layout changes
  resizeObserver = new ResizeObserver(updateIndicator)
  const pill = document.querySelector('.navbar__pill')
  if (pill) resizeObserver.observe(pill)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  window.removeEventListener('resize', updateIndicator)
  if (resizeObserver) resizeObserver.disconnect()
})
</script>

<style lang="scss" scoped>
@use '../styles/variables' as *;
@use '../styles/mixins' as *;

.navbar {
  position: fixed;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  z-index: 100;
  margin-bottom: $space-lg;

  @include tablet-up {
    bottom: auto;
    top: 0;
    margin-bottom: 0;
    padding-top: $space-lg;
  }

  &__pill {
    position: relative;
    display: flex;
    align-items: center;
    gap: 4px;
    padding: 4px;
    border-radius: $border-radius-full;
    background: rgba($color-secondary, 0.92);
    border: 1px solid $color-secondary-light;
    backdrop-filter: blur(16px);
    box-shadow: $shadow-lg;
  }

  &__indicator {
    position: absolute;
    top: 4px;
    left: 0;
    height: calc(100% - 8px);
    border-radius: $border-radius-full;
    background: rgba($color-primary, 0.15);
    transition: transform 0.35s cubic-bezier(0.4, 0, 0.2, 1),
                width 0.35s cubic-bezier(0.4, 0, 0.2, 1);
    z-index: 0;
  }

  &__glow {
    position: absolute;
    top: -8px;
    left: 50%;
    transform: translateX(-50%);

    @include mobile {
      display: none;
    }
  }

  &__glow-bar {
    width: 32px;
    height: 4px;
    background: $color-primary;
    border-radius: $border-radius-full $border-radius-full 0 0;
    margin: 0 auto;
  }

  &__glow-blur {
    position: absolute;
    border-radius: $border-radius-full;
    background: rgba($color-primary, 0.25);

    &--wide {
      width: 48px;
      height: 24px;
      filter: blur(10px);
      top: -8px;
      left: 50%;
      transform: translateX(-50%);
    }

    &--medium {
      width: 32px;
      height: 24px;
      filter: blur(8px);
      top: -4px;
      left: 50%;
      transform: translateX(-50%);
    }

    &--narrow {
      width: 16px;
      height: 16px;
      filter: blur(6px);
      top: 0;
      left: 50%;
      transform: translateX(-50%);
    }
  }

  &__link {
    position: relative;
    z-index: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: $space-sm $space-lg;
    border-radius: $border-radius-full;
    font-size: $font-size-sm;
    font-weight: $font-weight-semibold;
    color: $color-text-on-dark;
    text-decoration: none;
    transition: color $transition-fast;
    white-space: nowrap;

    @include focus-ring;

    &:hover {
      color: $color-primary;
    }

    &--active {
      color: $color-primary;
    }
  }

  &__label {
    display: none;

    @include tablet-up {
      display: inline;
    }
  }

  &__icon {
    display: block;

    @include tablet-up {
      display: none;
    }
  }
}
</style>
