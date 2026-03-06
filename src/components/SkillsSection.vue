<template>
  <section id="skills" class="skills section">
    <div class="container">
      <div class="section__header">
        <span class="section__label">Skills</span>
        <h2 class="section__title">What I Work With</h2>
        <p class="section__subtitle">
          Technologies and tools I've used across professional and personal projects.
        </p>
      </div>

      <div class="skills__categories">
        <div
          v-for="category in categories"
          :key="category.title"
          class="skills__category"
        >
          <div class="skills__category-header">
            <component :is="category.icon" :size="20" class="skills__category-icon" />
            <h3 class="skills__category-title">{{ category.title }}</h3>
          </div>
          <div class="skills__tags">
            <span
              v-for="skill in category.skills"
              :key="skill"
              class="skills__tag"
            >
              {{ skill }}
            </span>
          </div>
        </div>
      </div>

      <div class="skills__highlight">
        <div class="skills__highlight-inner">
          <Lightbulb :size="20" class="skills__highlight-icon" />
          <p class="skills__highlight-text">
            This website is built with <strong>Vue 3</strong>, <strong>Vite</strong>,
            and <strong>SCSS</strong> my first Vue project, built from scratch.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import {
  Code2,
  Layout,
  Cloud,
  Database,
  Wrench,
  Users,
  Lightbulb,
} from 'lucide-vue-next'

const categories = [
  {
    title: 'Languages',
    icon: Code2,
    skills: ['JavaScript', 'TypeScript', 'Python', 'C#', 'Java', 'SQL', 'HTML', 'CSS', 'SCSS'],
  },
  {
    title: 'Frameworks',
    icon: Layout,
    skills: ['React', '.NET', 'Polars', 'Slim Framework', 'Webpack', 'Vite'],
  },
  {
    title: 'Cloud & DevOps',
    icon: Cloud,
    skills: ['Azure Functions', 'Azure Logic Apps', 'Azure DevOps', 'Docker', 'Linux'],
  },
  {
    title: 'Databases',
    icon: Database,
    skills: ['MySQL', 'PostgreSQL', 'Azure Table Storage'],
  },
  {
    title: 'Tools',
    icon: Wrench,
    skills: ['Git', 'REST APIs', 'Sendgrid', 'JIRA', 'Raspberry Pi', 'Figma'],
  },
  {
    title: 'Soft Skills',
    icon: Users,
    skills: ['Teamwork', 'Problem Solving', 'Communication', 'Adaptability', 'Attention to Detail'],
  },
]
</script>

<style lang="scss" scoped>
@use '../styles/variables' as *;
@use '../styles/mixins' as *;

.skills {
  background: $color-bg-alt;

  &__categories {
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

  &__category {
    padding: $space-lg;
    border-radius: $border-radius-lg;
    background: $color-white;
    border: 1px solid $color-border;
    transition: transform $transition-base, box-shadow $transition-base;

    &:hover {
      transform: translateY(-3px);
      box-shadow: $shadow-md;
    }
  }

  &__category-header {
    display: flex;
    align-items: center;
    gap: $space-sm;
    margin-bottom: $space-md;
  }

  &__category-icon {
    color: $color-primary-dark;
  }

  &__category-title {
    font-size: $font-size-base;
    font-weight: $font-weight-semibold;
    color: $color-secondary;
  }

  &__tags {
    display: flex;
    flex-wrap: wrap;
    gap: $space-sm;
  }

  &__tag {
    display: inline-block;
    padding: 4px 12px;
    border-radius: $border-radius-full;
    font-size: $font-size-sm;
    font-weight: $font-weight-medium;
    color: $color-secondary;
    background: rgba($color-primary, 0.1);
    border: 1px solid rgba($color-primary, 0.2);
    transition: background $transition-fast, transform $transition-fast;

    &:hover {
      background: rgba($color-primary, 0.2);
      transform: translateY(-1px);
    }
  }

  &__highlight {
    margin-top: $space-3xl;
  }

  &__highlight-inner {
    display: flex;
    align-items: center;
    gap: $space-md;
    padding: $space-lg $space-xl;
    border-radius: $border-radius-lg;
    background: $color-secondary;
    color: $color-text-on-dark;
  }

  &__highlight-icon {
    color: $color-primary;
    flex-shrink: 0;
  }

  &__highlight-text {
    font-size: $font-size-base;
    color: $color-text-on-dark;
    line-height: $line-height-normal;

    strong {
      color: $color-primary;
      font-weight: $font-weight-semibold;
    }
  }
}
</style>
