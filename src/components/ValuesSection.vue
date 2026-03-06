<template>
  <section id="values" class="values section">
    <div class="container">
      <div class="section__header">
        <span class="section__label">Values</span>
        <h2 class="section__title">What I Stand For</h2>
        <p class="section__subtitle">
          The principles I bring to every team and project I work on.
        </p>
      </div>

      <div class="values__grid">
        <div
          v-for="value in values"
          :key="value.title"
          class="values__card"
        >
          <div class="values__card-icon" aria-hidden="true">
            <component :is="value.icon" :size="24" />
          </div>
          <h3 class="values__card-title">{{ value.title }}</h3>
          <p class="values__card-desc">{{ value.description }}</p>
        </div>
      </div>

      <div class="values__cta">
        <p class="values__cta-text">
          These aren't just words on a page. I chose to apply to
          <strong>Yellow Fish</strong> because your culture of collaboration,
          curiosity, and high-quality digital craft mirrors how I already
          approach my work. I want to grow alongside a team that shares
          these values.
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
import {
  Users,
  BookOpen,
  Heart,
  Palette,
  MessageCircle,
  Zap,
} from 'lucide-vue-next'

const values = [
  {
    title: 'Collaboration First',
    icon: Users,
    description:
      'I thrive in teams. Whether it\'s pair programming, stand-ups, or design reviews, I believe the best work comes from open communication and shared ownership.',
  },
  {
    title: 'Always Learning',
    icon: BookOpen,
    description:
      'I actively seek out new tools, frameworks, and best practices.',
  },
  {
    title: 'Inclusive & Supportive',
    icon: Heart,
    description:
      'I embrace respectful, inclusive ways of working. Everyone deserves to feel heard and valued, and diverse perspectives lead to better solutions.',
  },
  {
    title: 'Craft & Quality',
    icon: Palette,
    description:
      'I care deeply about the details. Clean code, polished interfaces, and accessible experiences aren\'t optional they\'re the standard I hold myself to.',
  },
  {
    title: 'Clear Communication',
    icon: MessageCircle,
    description:
      'I flag blockers early, ask questions when I\'m unsure, and keep the team informed. No one should be left guessing about where things stand.',
  },
  {
    title: 'Positive Energy',
    icon: Zap,
    description:
      'I bring enthusiasm and a proactive attitude to everything I do. Challenges are opportunities to learn, and setbacks are just part of the process.',
  },
]
</script>

<style lang="scss" scoped>
@use '../styles/variables' as *;
@use '../styles/mixins' as *;

.values {
  background: $color-secondary;
  color: $color-text-on-dark;

  .section__label {
    color: $color-primary;
  }

  .section__title {
    color: $color-white;
  }

  .section__subtitle {
    color: $color-text-on-dark;
    opacity: 0.8;
  }

  &__grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: $space-lg;

    @include tablet-up {
      grid-template-columns: repeat(2, 1fr);
    }

    @include desktop {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  &__card {
    padding: $space-xl;
    border-radius: $border-radius-lg;
    background: rgba($color-white, 0.05);
    border: 1px solid rgba($color-white, 0.1);
    transition: transform $transition-base, background $transition-base;

    &:hover {
      transform: translateY(-3px);
      background: rgba($color-white, 0.08);
    }
  }

  &__card-icon {
    @include flex-center;
    width: 48px;
    height: 48px;
    border-radius: $border-radius-md;
    background: rgba($color-primary, 0.15);
    color: $color-primary;
    margin-bottom: $space-md;
  }

  &__card-title {
    font-size: $font-size-lg;
    font-weight: $font-weight-bold;
    color: $color-white;
    margin-bottom: $space-sm;
  }

  &__card-desc {
    font-size: $font-size-sm;
    color: $color-text-on-dark;
    line-height: $line-height-normal;
    opacity: 0.8;
  }

  &__cta {
    margin-top: $space-3xl;
    text-align: center;
  }

  &__cta-text {
    font-size: $font-size-md;
    color: $color-text-on-dark;
    line-height: $line-height-normal;
    max-width: 700px;
    margin: 0 auto;
    opacity: 0.9;

    strong {
      color: $color-primary;
      font-weight: $font-weight-semibold;
    }
  }
}
</style>
