<script setup lang="ts">
import Navbar from '@/components/Navbar.vue'
import Hero from './components/Hero.vue'
import HomeCards from './components/HomeCards.vue'
import JobListings from './components/JobListings.vue'
</script>

<template>
  <Navbar />
  <Hero
    title="Vue jest super!"
    subtitle="Szybko ucz się Vue i zdobądź pracę."
  />
  <HomeCards />
  <JobListings :limit="3" :showButton="true" />
</template>
