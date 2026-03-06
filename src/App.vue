<template>
  <NavBar />
  <main>
    <HeroSection />
    <AboutSection />
    <section id="skills" style="min-height: 100vh;"></section>
    <section id="experience" style="min-height: 100vh;"></section>
    <section id="projects" style="min-height: 100vh;"></section>
    <section id="values" style="min-height: 100vh;"></section>
    <section id="contact" style="min-height: 100vh;"></section>
  </main>
</template>

<script setup>
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
</script>
