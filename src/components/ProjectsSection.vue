<template>
  <section id="projects" class="projects section">
    <div class="container">
      <div class="section__header">
        <span class="section__label">Projects</span>
        <h2 class="section__title">What I've Built</h2>
        <p class="section__subtitle">
          Personal and academic projects that showcase my skills beyond the workplace.
        </p>
      </div>

      <div class="projects__grid">
        <article
          v-for="project in projects"
          :key="project.title"
          class="projects__card"
        >
          <div class="projects__card-badge" v-if="project.badge">
            {{ project.badge }}
          </div>
          <div class="projects__card-icon" aria-hidden="true">
            <component :is="project.icon" :size="28" />
          </div>
          <h3 class="projects__card-title">{{ project.title }}</h3>
          <p class="projects__card-desc">{{ project.description }}</p>
          <ul class="projects__card-points">
            <li
              v-for="point in project.points"
              :key="point"
              class="projects__card-point"
            >
              {{ point }}
            </li>
          </ul>
          <div class="projects__card-tech">
            <span
              v-for="tag in project.tech"
              :key="tag"
              class="projects__card-tag"
            >
              {{ tag }}
            </span>
          </div>
          <div v-if="project.link" class="projects__card-footer">
            <a
              :href="project.link"
              target="_blank"
              rel="noopener noreferrer"
              class="projects__card-link"
            >
              <ExternalLink :size="14" />
              View Project
            </a>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
import { Shield, PawPrint, Globe, ExternalLink } from 'lucide-vue-next'

const projects = [
  {
    title: 'Artisan Authentication Platform',
    badge: 'Final Year Project',
    icon: Shield,
    description:
      'A multilingual web application enabling artisans to document craft creation processes and generate W3C Verifiable Credentials for authenticity verification.',
    points: [
      'Implementing Decentralised Identifier (DID) resolution and cryptographic credential signing for tamper-proof provenance.',
      'Pairing Verifiable Credentials with QR codes without reliance on centralised authorities.',
    ],
    tech: ['React', 'TypeScript', 'W3C VCs', 'DID', 'QR Codes'],
    link: null,
  },
  {
    title: 'ZapApp - Pangolin Wildlife Tracker',
    badge: 'PWA',
    icon: PawPrint,
    description:
      'A Progressive Web Application for pangolin wildlife tracking with offline-first capabilities.',
    points: [
      'Built with React frontend and Slim Framework (PHP) backend with MySQL database.',
      'Deployed on university hosting infrastructure with full offline support via service workers.',
    ],
    tech: ['React', 'PHP', 'Slim Framework', 'MySQL', 'PWA'],
    link: null,
  },
  {
    title: 'MinMax Inventory Calculator',
    badge: 'Work Project',
    icon: Globe,
    description:
      'A Python-based inventory optimisation application that calculates dynamic min-max stock levels for field engineer vans at Eschmann Technologies.',
    points: [
      'Processes multi-table datasets using dataframes to apply custom formulas across parts fitted, equipment, and usage data.',
      'Ensures optimal inventory distribution across the fleet, reducing overstock and preventing shortages.',
    ],
    tech: ['Python', 'Polars', 'Data Engineering', 'Automation'],
    link: null,
  },
]
</script>

<style lang="scss" scoped>
@use '../styles/variables' as *;
@use '../styles/mixins' as *;

.projects {
  background: $color-bg-alt;

  &__grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: $space-xl;

    @include tablet-up {
      grid-template-columns: repeat(2, 1fr);
    }

    @include desktop {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  &__card {
    position: relative;
    display: flex;
    flex-direction: column;
    padding: $space-xl;
    border-radius: $border-radius-lg;
    background: $color-white;
    border: 1px solid $color-border;
    transition: transform $transition-base, box-shadow $transition-base;

    &:hover {
      transform: translateY(-4px);
      box-shadow: $shadow-lg;
    }
  }

  &__card-badge {
    position: absolute;
    top: $space-md;
    right: $space-md;
    padding: 2px 10px;
    border-radius: $border-radius-full;
    font-size: $font-size-xs;
    font-weight: $font-weight-semibold;
    background: rgba($color-primary, 0.15);
    color: $color-primary-dark;
  }

  &__card-icon {
    @include flex-center;
    width: 56px;
    height: 56px;
    border-radius: $border-radius-md;
    background: $color-secondary;
    color: $color-primary;
    margin-bottom: $space-lg;
  }

  &__card-title {
    font-size: $font-size-lg;
    font-weight: $font-weight-bold;
    color: $color-secondary;
    margin-bottom: $space-sm;
  }

  &__card-desc {
    font-size: $font-size-sm;
    color: $color-text-light;
    line-height: $line-height-normal;
    margin-bottom: $space-md;
  }

  &__card-points {
    display: flex;
    flex-direction: column;
    gap: $space-sm;
    margin-bottom: $space-lg;
    flex-grow: 1;
  }

  &__card-point {
    position: relative;
    padding-left: $space-lg;
    font-size: $font-size-sm;
    color: $color-text-light;
    line-height: $line-height-normal;

    &::before {
      content: '';
      position: absolute;
      left: 0;
      top: 8px;
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: $color-primary;
    }
  }

  &__card-tech {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    padding-top: $space-md;
    border-top: 1px solid $color-border;
  }

  &__card-tag {
    font-size: $font-size-xs;
    padding: 2px 8px;
    border-radius: $border-radius-full;
    background: rgba($color-accent, 0.08);
    color: $color-accent;
    font-weight: $font-weight-medium;
  }

  &__card-footer {
    margin-top: $space-md;
  }

  &__card-link {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-size: $font-size-sm;
    font-weight: $font-weight-semibold;
    color: $color-primary-dark;
    transition: color $transition-fast;

    @include focus-ring;

    &:hover {
      color: $color-accent;
    }
  }
}
</style>
