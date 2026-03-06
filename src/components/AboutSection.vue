<template>
  <section id="about" class="about section">
    <div class="container">
      <div class="section__header">
        <span class="section__label">About Me</span>
        <h2 class="section__title">Who I Am</h2>
        <p class="section__subtitle">
          A developer who thrives on turning ideas into polished digital experiences.
        </p>
      </div>

      <div class="about__grid">
        <div class="about__story">
          <p class="about__text">
            I'm a final year <strong>BSc Computer Science</strong> student at the
            <strong>University of Brighton</strong>, predicted a First. I'm currently
            working as a <strong>Student Software Developer</strong> at Eschmann Technologies
            alongside my studies balancing both with the same dedication.
          </p>
          <p class="about__text">
            My placement year opened my eyes to the full software lifecycle, from
            building automated booking systems with Azure Functions, to containerising
            apps with Docker on Raspberry Pi devices. I've worked across the stack, but
            what excites me most is crafting interfaces and applications that people genuinely enjoy using.
          </p>
          <p class="about__text">
            I'm naturally curious, always picking up new tools and frameworks.
            This website, for example, is my first time using <strong>Vue</strong> —
            I built it specifically for this application to demonstrate that I can
            adapt and learn quickly.
          </p>
        </div>

        <div class="about__details">
          <div class="about__card">
            <div class="about__card-icon" aria-hidden="true">
              <GraduationCap :size="24" />
            </div>
            <div>
              <h3 class="about__card-title">Education</h3>
              <p class="about__card-text">BSc Computer Science (Placement Year)</p>
              <p class="about__card-sub">University of Brighton &middot; Predicted 1st</p>
            </div>
          </div>

          <div class="about__card">
            <div class="about__card-icon" aria-hidden="true">
              <MapPin :size="24" />
            </div>
            <div>
              <h3 class="about__card-title">Location</h3>
              <p class="about__card-text">Hove, East Sussex</p>
              <p class="about__card-sub">Open to hybrid in London / Brighton</p>
            </div>
          </div>

          <div class="about__card">
            <div class="about__card-icon" aria-hidden="true">
              <Briefcase :size="24" />
            </div>
            <div>
              <h3 class="about__card-title">Current Role</h3>
              <p class="about__card-text">Student Software Developer</p>
              <p class="about__card-sub">Eschmann Technologies &middot; Aug 2024 - Present</p>
            </div>
          </div>

          <div class="about__card">
            <div class="about__card-icon" aria-hidden="true">
              <Sparkles :size="24" />
            </div>
            <div>
              <h3 class="about__card-title">Fun Fact</h3>
              <p class="about__card-text">First time using Vue</p>
              <p class="about__card-sub">Built this site to prove I can adapt fast</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { GraduationCap, MapPin, Briefcase, Sparkles } from 'lucide-vue-next'
</script>

<style lang="scss" scoped>
@use '../styles/variables' as *;
@use '../styles/mixins' as *;

.about {
  background: $color-bg;

  &__grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: $space-3xl;
    align-items: start;

    @include desktop {
      grid-template-columns: 1.2fr 1fr;
      gap: $space-4xl;
    }
  }

  &__story {
    display: flex;
    flex-direction: column;
    gap: $space-lg;
  }

  &__text {
    font-size: $font-size-md;
    color: $color-text-light;
    line-height: $line-height-normal;

    strong {
      color: $color-secondary;
      font-weight: $font-weight-semibold;
    }
  }

  &__details {
    display: grid;
    grid-template-columns: 1fr;
    gap: $space-md;

    @include tablet-up {
      grid-template-columns: 1fr 1fr;
    }

    @include desktop {
      grid-template-columns: 1fr;
    }
  }

  &__card {
    display: flex;
    align-items: flex-start;
    gap: $space-md;
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

  &__card-icon {
    @include flex-center;
    width: 48px;
    height: 48px;
    border-radius: $border-radius-md;
    background: rgba($color-primary, 0.12);
    color: $color-primary-dark;
    flex-shrink: 0;
  }

  &__card-title {
    font-size: $font-size-sm;
    font-weight: $font-weight-semibold;
    color: $color-secondary;
    margin-bottom: 2px;
  }

  &__card-text {
    font-size: $font-size-base;
    color: $color-text;
    font-weight: $font-weight-medium;
  }

  &__card-sub {
    font-size: $font-size-sm;
    color: $color-text-muted;
    margin-top: 2px;
  }
}
</style>
