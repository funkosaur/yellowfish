<template>
  <section id="hero" class="hero">
    <!-- Animated swimming fish -->
    <div class="hero__bg" aria-hidden="true">
      <svg
        v-for="fish in fishes"
        :key="fish.id"
        class="hero__fish"
        :class="fish.className"
        :style="fish.style"
        viewBox="0 0 64 34"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M48 17C48 17 64 8 64 0C56 6 48 4 48 4C48 4 42 0 32 0C14.3 0 0 7.6 0 17C0 26.4 14.3 34 32 34C42 34 48 30 48 30C48 30 56 28 64 34C64 26 48 17 48 17Z"
          :fill="fish.color"
        />
        <circle cx="10" cy="16" r="2.5" :fill="fish.eyeColor" />
      </svg>
    </div>

    <div class="hero__content container">
      <div class="hero__text">
        <p class="hero__greeting" :class="{ visible: showGreeting }">
          Hello, I'm
        </p>
        <h1 class="hero__name" :class="{ visible: showName }">
          Mario<br />
          <span class="hero__name--accent">Boykovski</span>
        </h1>
        <div class="hero__role-wrapper" :class="{ visible: showRole }">
          <div class="hero__role-line" aria-hidden="true"></div>
          <p class="hero__role">
            Junior Front-End Developer
          </p>
        </div>
        <p class="hero__tagline" :class="{ visible: showTagline }">
          Turning creative concepts into clean
          and responsive digital experiences.
        </p>
        <div class="hero__actions" :class="{ visible: showActions }">
          <a href="#contact" class="hero__btn hero__btn--primary" @click.prevent="scrollTo('#contact')">
            Get In Touch
          </a>
          <a href="#experience" class="hero__btn hero__btn--outline" @click.prevent="scrollTo('#experience')">
            View My Work
          </a>
        </div>
      </div>

      <div class="hero__visual" :class="{ visible: showVisual }">
        <div class="hero__card">
          <div class="hero__card-header">
            <span class="hero__card-title">mario.js</span>
            <div class="hero__card-controls">
              <span class="hero__card-btn" aria-hidden="true">&#8212;</span>
              <span class="hero__card-btn" aria-hidden="true">&#9633;</span>
              <span class="hero__card-btn hero__card-btn--close" aria-hidden="true">&#10005;</span>
            </div>
          </div>
          <pre class="hero__code"><code><span class="code-keyword">const</span> <span class="code-var">mario</span> = {
  <span class="code-key">location</span>: <span class="code-string">"Hove, East Sussex"</span>,
  <span class="code-key">education</span>: <span class="code-string">"University of Brighton"</span>,
  <span class="code-key">degree</span>: <span class="code-string">"BSc Computer Science with a placement year"</span>,
  <span class="code-key">passion</span>: <span class="code-string">"Full Stack Development"</span>,
  <span class="code-key">currentRole</span>: <span class="code-string">"Student Software Dev"</span>,
  <span class="code-key">loves</span>: [
    <span class="code-string">"Clean Code"</span>,
    <span class="code-string">"Cool UIs"</span>,
    <span class="code-string">"Learning New Tech"</span>
  ]
};</code></pre>
        </div>
      </div>
    </div>

    <div class="hero__scroll" :class="{ visible: showActions }" aria-hidden="true">
      <div class="hero__scroll-mouse">
        <div class="hero__scroll-wheel"></div>
      </div>
      <span class="hero__scroll-text">Scroll to explore</span>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const showGreeting = ref(false)
const showName = ref(false)
const showRole = ref(false)
const showTagline = ref(false)
const showActions = ref(false)
const showVisual = ref(false)

const fishColors = [
  { color: 'rgba(245, 197, 24, 0.55)', eyeColor: 'rgba(196, 155, 0, 0.8)' },
  { color: 'rgba(245, 197, 24, 0.4)', eyeColor: 'rgba(196, 155, 0, 0.7)' },
  { color: 'rgba(0, 180, 216, 0.4)', eyeColor: 'rgba(0, 140, 180, 0.7)' },
  { color: 'rgba(0, 180, 216, 0.3)', eyeColor: 'rgba(0, 140, 180, 0.6)' },
]

const fishes = Array.from({ length: 8 }, (_, i) => {
  const palette = fishColors[i % fishColors.length]
  const size = Math.random() * 40 + 30
  const goesRight = i % 2 === 0

  return {
    id: i,
    color: palette.color,
    eyeColor: palette.eyeColor,
    className: goesRight ? 'hero__fish--right' : 'hero__fish--left',
    style: {
      width: `${size}px`,
      top: `${10 + Math.random() * 75}%`,
      animationDelay: `${Math.random() * 10}s`,
      animationDuration: `${Math.random() * 12 + 14}s`,
    },
  }
})

function scrollTo(selector) {
  const el = document.querySelector(selector)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

onMounted(() => {
  // Staggered entrance animation
  setTimeout(() => (showGreeting.value = true), 200)
  setTimeout(() => (showName.value = true), 500)
  setTimeout(() => (showRole.value = true), 900)
  setTimeout(() => (showTagline.value = true), 1200)
  setTimeout(() => (showActions.value = true), 1500)
  setTimeout(() => (showVisual.value = true), 800)
})
</script>

<style lang="scss" scoped>
@use 'sass:color';
@use '../styles/variables' as *;
@use '../styles/mixins' as *;

.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  overflow: hidden;
  background: linear-gradient(
    160deg,
    $color-bg 0%,
    $color-bg-alt 40%,
    color.adjust($color-accent-light, $lightness: 18%) 100%
  );
  padding-top: $space-4xl;

  // ---- Swimming fish background ----
  &__bg {
    position: absolute;
    inset: 0;
    pointer-events: none;
    overflow: hidden;
  }

  &__fish {
    position: absolute;
    animation-timing-function: linear;
    animation-iteration-count: infinite;

    // SVG fish faces left, so right-swimmers need to be flipped
    &--right {
      left: -80px;
      transform: scaleX(-1);
      animation-name: swim-right;
    }

    // Left-swimmers: fish already faces left, no flip needed
    &--left {
      right: -80px;
      animation-name: swim-left;
    }

    &:nth-child(odd) {
      animation-timing-function: ease-in-out;
    }
  }

  // ---- Content grid ----
  &__content {
    display: grid;
    grid-template-columns: 1fr;
    gap: $space-3xl;
    align-items: center;
    position: relative;
    z-index: 1;

    @include desktop {
      grid-template-columns: 1fr 1fr;
      gap: $space-4xl;
    }
  }

  // ---- Text side ----
  &__text {
    order: 1;
  }

  &__greeting {
    font-size: $font-size-lg;
    font-weight: $font-weight-medium;
    color: $color-text-light;
    margin-bottom: $space-sm;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s ease;

    &.visible {
      opacity: 1;
      transform: translateY(0);
    }
  }

  &__name {
    font-size: $font-size-4xl;
    font-weight: $font-weight-black;
    color: $color-secondary;
    line-height: $line-height-tight;
    margin-bottom: $space-lg;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.7s ease;

    @include mobile {
      font-size: $font-size-3xl;
    }

    &.visible {
      opacity: 1;
      transform: translateY(0);
    }

    &--accent {
      background: linear-gradient(135deg, $color-primary, $color-primary-dark);
      -webkit-background-clip: text;
      background-clip: text;
      -webkit-text-fill-color: transparent;
    }
  }

  &__role-wrapper {
    display: flex;
    align-items: center;
    gap: $space-md;
    margin-bottom: $space-lg;
    opacity: 0;
    transform: translateX(-20px);
    transition: all 0.6s ease;

    &.visible {
      opacity: 1;
      transform: translateX(0);
    }
  }

  &__role-line {
    width: 40px;
    height: 3px;
    background: $color-primary;
    border-radius: $border-radius-full;
    flex-shrink: 0;
  }

  &__role {
    font-size: $font-size-xl;
    font-weight: $font-weight-semibold;
    color: $color-accent;
    letter-spacing: -0.02em;
  }

  &__tagline {
    font-size: $font-size-md;
    color: $color-text-light;
    line-height: $line-height-normal;
    max-width: 480px;
    margin-bottom: $space-2xl;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s ease;

    &.visible {
      opacity: 1;
      transform: translateY(0);
    }
  }

  // ---- CTA buttons ----
  &__actions {
    display: flex;
    gap: $space-md;
    flex-wrap: wrap;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s ease;

    &.visible {
      opacity: 1;
      transform: translateY(0);
    }
  }

  &__btn {
    display: inline-flex;
    align-items: center;
    padding: $space-sm $space-xl;
    border-radius: $border-radius-full;
    font-size: $font-size-base;
    font-weight: $font-weight-semibold;
    text-decoration: none;
    transition: all $transition-base;

    @include focus-ring;

    &--primary {
      background: $color-primary;
      color: $color-secondary;
      box-shadow: 0 4px 16px rgba($color-primary, 0.35);

      &:hover {
        background: $color-primary-light;
        transform: translateY(-2px);
        box-shadow: 0 6px 24px rgba($color-primary, 0.45);
        color: $color-secondary;
      }
    }

    &--outline {
      border: 2px solid $color-secondary;
      color: $color-secondary;

      &:hover {
        background: $color-secondary;
        color: $color-white;
        transform: translateY(-2px);
      }
    }
  }

  // ---- Code card visual ----
  &__visual {
    order: 2;
    opacity: 0;
    transform: translateY(40px) rotateX(5deg);
    transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);

    &.visible {
      opacity: 1;
      transform: translateY(0) rotateX(0);
    }
  }

  &__card {
    @include glass-card;
    overflow: hidden;
    border: 1px solid $color-border;

    @include hover-lift;
  }

  &__card-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 6px $space-md;
    background: $color-secondary;
    border-bottom: 1px solid $color-secondary-light;
  }

  &__card-title {
    font-family: $font-mono;
    font-size: $font-size-xs;
    color: $color-text-on-dark;
    opacity: 0.8;
  }

  &__card-controls {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  &__card-btn {
    font-size: 11px;
    color: $color-text-on-dark;
    opacity: 0.6;
    line-height: 1;

    &--close:hover {
      opacity: 1;
      color: #e81123;
    }
  }

  &__code {
    padding: $space-lg;
    font-family: $font-mono;
    font-size: $font-size-sm;
    line-height: 1.8;
    overflow-x: auto;

    @include mobile {
      font-size: $font-size-xs;
      padding: $space-md;
    }

    code {
      color: $color-secondary;
    }
  }

  // ---- Scroll indicator ----
  &__scroll {
    position: absolute;
    bottom: $space-2xl;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: $space-sm;
    opacity: 0;
    transition: opacity 0.6s ease;

    &.visible {
      opacity: 1;
    }

    @include mobile {
      display: none;
    }
  }

  &__scroll-mouse {
    width: 24px;
    height: 38px;
    border: 2px solid $color-text-muted;
    border-radius: 12px;
    position: relative;
  }

  &__scroll-wheel {
    width: 4px;
    height: 8px;
    background: $color-text-muted;
    border-radius: $border-radius-full;
    position: absolute;
    top: 6px;
    left: 50%;
    transform: translateX(-50%);
    animation: scroll-wheel 1.5s ease-in-out infinite;
  }

  &__scroll-text {
    font-size: $font-size-xs;
    color: $color-text-muted;
    text-transform: uppercase;
    letter-spacing: 2px;
  }
}

// ---- Syntax highlighting colors ----
.code-keyword { color: #c678dd; }
.code-var { color: #e06c75; }
.code-key { color: $color-accent; }
.code-string { color: #98c379; }

// ---- Keyframes ----
@keyframes swim-right {
  0% {
    transform: scaleX(-1) translateX(0) translateY(0);
    opacity: 0;
  }
  5% {
    opacity: 1;
  }
  50% {
    transform: scaleX(-1) translateX(calc(50vw)) translateY(-20px);
  }
  95% {
    opacity: 1;
  }
  100% {
    transform: scaleX(-1) translateX(calc(100vw + 80px)) translateY(10px);
    opacity: 0;
  }
}

@keyframes swim-left {
  0% {
    transform: translateX(0) translateY(0);
    opacity: 0;
  }
  5% {
    opacity: 1;
  }
  50% {
    transform: translateX(calc(-50vw)) translateY(15px);
  }
  95% {
    opacity: 1;
  }
  100% {
    transform: translateX(calc(-100vw - 80px)) translateY(-10px);
    opacity: 0;
  }
}

@keyframes scroll-wheel {
  0% {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
  100% {
    opacity: 0;
    transform: translateX(-50%) translateY(12px);
  }
}
</style>
