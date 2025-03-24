<script setup lang="ts">
import jobsData from '@/jobs.json'
import { reactive, defineProps, onMounted } from 'vue'
import JobListing from './JobListing.vue'
import { RouterLink } from 'vue-router'
import axios from 'axios'

interface Company {
  name: string
  description: string
  contactEmail: string
  contactPhone: string
}

export interface Job {
  id: number
  title: string
  type: string
  description: string
  location: string
  salary: string
  company: Company
}

withDefaults(defineProps<{ limit: number; showButton: boolean }>(), {
  showButton: false,
})

// const jobs = ref<Job[]>([])
const state = reactive<{ jobs: Job[] | []; isLoading: boolean }>({
  jobs: [],
  isLoading: true,
})

onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:5000/jobs')
    state.jobs = response.data
  } catch (error) {
    console.error('Error while fetching data', error)
  } finally {
    state.isLoading = false
  }
})
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing
          v-for="job of state.jobs.slice(0, limit || state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>

  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>
