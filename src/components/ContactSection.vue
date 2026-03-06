<template>
  <section id="contact" class="contact section">
    <div class="container">
      <div class="section__header">
        <span class="section__label">Contact</span>
        <h2 class="section__title">Let's Connect</h2>
        <p class="section__subtitle">
          I'd love to chat about the Junior Front-End Developer role at Yellow Fish.
        </p>
      </div>

      <div class="contact__grid">
        <div class="contact__info">
          <p class="contact__intro">
            Whether you want to discuss the role, see more of my work,
            or just say hello, I'm always happy to hear from you.
          </p>

          <div class="contact__channels">
            <a
              href="mailto:mario.bojkovski@outlook.com"
              class="contact__channel"
            >
              <div class="contact__channel-icon" aria-hidden="true">
                <Mail :size="20" />
              </div>
              <div>
                <p class="contact__channel-label">Email</p>
                <p class="contact__channel-value">mario.bojkovski@outlook.com</p>
              </div>
            </a>

            <a
              href="tel:+447895408449"
              class="contact__channel"
            >
              <div class="contact__channel-icon" aria-hidden="true">
                <Phone :size="20" />
              </div>
              <div>
                <p class="contact__channel-label">Phone</p>
                <p class="contact__channel-value">+44 7895 408449</p>
              </div>
            </a>

            <a
              href="https://www.linkedin.com/in/mario-boykovski-a74584236/"
              target="_blank"
              rel="noopener noreferrer"
              class="contact__channel"
            >
              <div class="contact__channel-icon" aria-hidden="true">
                <Linkedin :size="20" />
              </div>
              <div>
                <p class="contact__channel-label">LinkedIn</p>
                <p class="contact__channel-value">mario-boykovski</p>
              </div>
            </a>

            <a
              href="https://github.com/funkosaur"
              target="_blank"
              rel="noopener noreferrer"
              class="contact__channel"
            >
              <div class="contact__channel-icon" aria-hidden="true">
                <Github :size="20" />
              </div>
              <div>
                <p class="contact__channel-label">GitHub</p>
                <p class="contact__channel-value">funkosaur</p>
              </div>
            </a>
          </div>
        </div>

        <div class="contact__closing">
          <div class="contact__closing-card">
            <h3 class="contact__closing-title">Thanks for scrolling this far</h3>
            <p class="contact__closing-text">
              Every colour, layout, and interaction on this page was chosen
              with Yellow Fish in mind. I wanted my application to feel like
              something I'd be proud to ship, not just something I'd submit.
            </p>
            <p class="contact__closing-text">
              Every section, component, and animation was written by hand to
              demonstrate the skills listed in the job description. I hope it
              shows not just what I can do, but who I am as a developer.
            </p>
            <p class="contact__closing-sign">
              Mario Boykovski
            </p>
          </div>
        </div>
      </div>

      <footer class="contact__footer">
        <p class="contact__footer-text">
          Built with Vue 3, Vite &amp; SCSS
        </p>
      </footer>
    </div>
  </section>
</template>

<script setup>
import { Mail, Phone, Linkedin, Github, MapPin } from 'lucide-vue-next'
</script>

<style lang="scss" scoped>
@use '../styles/variables' as *;
@use '../styles/mixins' as *;

.contact {
  background: $color-bg;
  padding-bottom: $space-2xl;

  &__grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: $space-3xl;
    align-items: center;

    @include desktop {
      grid-template-columns: 1fr 1fr;
      gap: $space-4xl;
    }
  }

  &__intro {
    font-size: $font-size-md;
    color: $color-text-light;
    line-height: $line-height-normal;
    margin-bottom: $space-2xl;
  }

  &__channels {
    display: flex;
    flex-direction: column;
    gap: $space-md;
  }

  &__channel {
    display: flex;
    align-items: center;
    gap: $space-md;
    padding: $space-md $space-lg;
    border-radius: $border-radius-lg;
    background: $color-white;
    border: 1px solid $color-border;
    text-decoration: none;
    transition: transform $transition-base, box-shadow $transition-base;

    @include focus-ring;

    &:hover {
      transform: translateX(4px);
      box-shadow: $shadow-md;
    }

    &--static {
      cursor: default;

      &:hover {
        transform: none;
        box-shadow: none;
      }
    }
  }

  &__channel-icon {
    @include flex-center;
    width: 44px;
    height: 44px;
    border-radius: $border-radius-md;
    background: rgba($color-primary, 0.12);
    color: $color-primary-dark;
    flex-shrink: 0;
  }

  &__channel-label {
    font-size: $font-size-xs;
    font-weight: $font-weight-semibold;
    color: $color-text-muted;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  &__channel-value {
    font-size: $font-size-base;
    font-weight: $font-weight-medium;
    color: $color-secondary;
  }

  &__closing-card {
    padding: $space-xl;
    border-radius: $border-radius-lg;
    background: $color-secondary;
    color: $color-text-on-dark;
  }

  &__closing-title {
    font-size: $font-size-xl;
    font-weight: $font-weight-bold;
    color: $color-white;
    margin-bottom: $space-lg;
  }

  &__closing-text {
    font-size: $font-size-base;
    color: $color-text-on-dark;
    line-height: $line-height-normal;
    opacity: 0.85;
    margin-bottom: $space-md;

    &:last-of-type {
      margin-bottom: $space-xl;
    }
  }

  &__closing-sign {
    font-size: $font-size-lg;
    font-weight: $font-weight-bold;
    color: $color-primary;
    font-style: italic;
  }

  &__footer {
    margin-top: $space-3xl;
    padding-top: $space-lg;
    border-top: 1px solid $color-border;
    text-align: center;
  }

  &__footer-text {
    font-size: $font-size-sm;
    color: $color-text-muted;
  }
}
</style>
