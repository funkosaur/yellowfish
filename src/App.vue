<template>
  <NavBar />
  <main>
    <HeroSection />
    <AboutSection />
    <SkillsSection />
    <ExperienceSection />
    <section id="projects" style="min-height: 100vh;"></section>
    <section id="values" style="min-height: 100vh;"></section>
    <section id="contact" style="min-height: 100vh;"></section>
  </main>
</template>

<script setup>
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
</script>
