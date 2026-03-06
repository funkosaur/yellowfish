<template>
  <section id="experience" class="experience section">
    <div class="container">
      <div class="section__header">
        <span class="section__label">Experience</span>
        <h2 class="section__title">Where I've Worked</h2>
        <p class="section__subtitle">
          Professional roles that have shaped my skills and approach to development.
        </p>
      </div>

      <div class="experience__timeline">
        <div class="experience__line" aria-hidden="true"></div>

        <article
          v-for="(job, index) in jobs"
          :key="job.title"
          class="experience__item"
          :class="{ 'experience__item--right': index % 2 !== 0 }"
        >
          <div class="experience__dot" aria-hidden="true">
            <component :is="job.icon" :size="16" />
          </div>

          <div class="experience__card">
            <div class="experience__card-top">
              <span class="experience__date">
                <Calendar :size="14" />
                {{ job.date }}
              </span>
              <span class="experience__location">
                <MapPin :size="14" />
                {{ job.location }}
              </span>
            </div>
            <h3 class="experience__title">{{ job.title }}</h3>
            <p class="experience__company">{{ job.company }}</p>
            <ul class="experience__list">
              <li
                v-for="point in job.points"
                :key="point"
                class="experience__point"
              >
                {{ point }}
              </li>
            </ul>
            <div v-if="job.tech" class="experience__tech">
              <span
                v-for="tag in job.tech"
                :key="tag"
                class="experience__tech-tag"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
import { Code2, Globe, Database, Package, ShoppingCart, Calendar, MapPin } from 'lucide-vue-next'

const jobs = [
  {
    title: 'Student Software Developer',
    company: 'Eschmann Technologies',
    date: 'Aug 2024 - Present',
    location: 'Lancing, UK',
    icon: Code2,
    points: [
      'Created an automated booking system using Azure Functions integrated with third-party APIs, implementing intelligent calendar parsing and bidirectional email notifications that reduced scheduling conflicts.',
      'Completed and containerised an auto-calibration application combining a C# backend with TypeScript React frontend, deployed on Raspberry Pi devices via Docker with automated RS-232 serial communication.',
      'Developed a Python-based inventory optimisation application processing multi-table datasets using dataframes to calculate dynamic min-max stock levels for field engineer vans.',
    ],
    tech: ['Azure Functions', 'React', 'TypeScript', 'C#', 'Python', 'Docker', 'Raspberry Pi'],
  },
  {
    title: 'Web Developer Research Placement',
    company: 'University of Brighton',
    date: 'Jun 2023 - Oct 2023',
    location: 'Brighton, UK',
    icon: Globe,
    points: [
      'Developed a museum storage image gallery web application using a web-based visualisation system to deliver a dynamic presentation of an extensive image collection.',
      'Employed IIIF (International Image Interoperability Framework) to standardise image description and delivery methods, ensuring continuous access to structured image sequences.',
    ],
    tech: ['IIIF', 'JavaScript', 'HTML', 'CSS'],
  },
  {
    title: 'Back End Developer Research Placement',
    company: 'University of Brighton',
    date: 'Apr 2023 - Jun 2023',
    location: 'Brighton, UK',
    icon: Database,
    points: [
      'Led the migration of a database system from an Excel-based architecture to a structured SQL database, introducing efficiency and scalability.',
      'Developed a RESTful API to optimise data retrieval and integration for an existing website, enhancing user experience and real-time data access.',
    ],
    tech: ['SQL', 'REST API'],
  },
  {
    title: 'FC Associate',
    company: 'Amazon',
    date: 'Sep 2022 - Present',
    location: 'Bognor Regis, UK',
    icon: Package,
    points: [
      'Manage high-volume warehouse operations including shipment processing, quality control, and inventory accuracy in a fast-paced environment.',
      'Collaborate with cross-functional teams to maintain operational efficiency and safety standards.',
    ],
    tech: null,
  },
  {
    title: 'Manager',
    company: "Papa John's",
    date: 'Jan 2019 - Aug 2022',
    location: 'Brighton, UK',
    icon: ShoppingCart,
    points: [
      'Managed all aspects of operations including staff scheduling, inventory control, and financial management.',
      'Trained and supervised a team of kitchen staff, servers, and delivery drivers to maintain high-quality service.',
    ],
    tech: null,
  },
]
</script>

<style lang="scss" scoped>
@use '../styles/variables' as *;
@use '../styles/mixins' as *;

.experience {
  background: $color-bg;

  &__timeline {
    position: relative;
    max-width: 900px;
    margin: 0 auto;
  }

  &__line {
    position: absolute;
    left: 20px;
    top: 0;
    bottom: 0;
    width: 2px;
    background: linear-gradient(to bottom, $color-primary, $color-accent);

    @include desktop {
      left: 50%;
      transform: translateX(-50%);
    }
  }

  &__item {
    position: relative;
    padding-left: 56px;
    margin-bottom: $space-2xl;

    @include desktop {
      width: 50%;
      padding-left: 0;
      padding-right: $space-3xl;

      &--right {
        margin-left: 50%;
        padding-right: 0;
        padding-left: $space-3xl;
      }
    }

    &:last-child {
      margin-bottom: 0;
    }
  }

  &__dot {
    position: absolute;
    left: 10px;
    top: 0;
    width: 22px;
    height: 22px;
    border-radius: 50%;
    background: $color-primary;
    color: $color-secondary;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1;
    box-shadow: 0 0 0 4px $color-bg;

    @include desktop {
      left: auto;
      right: -11px;

      .experience__item--right & {
        right: auto;
        left: -11px;
      }
    }
  }

  &__card {
    padding: $space-lg;
    border-radius: $border-radius-lg;
    background: $color-white;
    border: 1px solid $color-border;
    transition: transform $transition-base, box-shadow $transition-base;

    &:hover {
      transform: translateY(-2px);
      box-shadow: $shadow-md;
    }
  }

  &__card-top {
    display: flex;
    flex-wrap: wrap;
    gap: $space-md;
    margin-bottom: $space-sm;
  }

  &__date,
  &__location {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    font-size: $font-size-sm;
    color: $color-text-muted;
  }

  &__title {
    font-size: $font-size-lg;
    font-weight: $font-weight-bold;
    color: $color-secondary;
    margin-bottom: 2px;
  }

  &__company {
    font-size: $font-size-base;
    font-weight: $font-weight-medium;
    color: $color-primary-dark;
    margin-bottom: $space-md;
  }

  &__list {
    display: flex;
    flex-direction: column;
    gap: $space-sm;
    margin-bottom: $space-md;
  }

  &__point {
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
      background: $color-accent;
    }
  }

  &__tech {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    padding-top: $space-sm;
    border-top: 1px solid $color-border;
  }

  &__tech-tag {
    font-size: $font-size-xs;
    padding: 2px 8px;
    border-radius: $border-radius-full;
    background: rgba($color-accent, 0.08);
    color: $color-accent;
    font-weight: $font-weight-medium;
  }
}
</style>
