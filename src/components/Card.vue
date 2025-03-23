<script setup lang="ts">
import { defineProps } from 'vue'

withDefaults(defineProps<{ bg?: string }>(), {
  bg: 'bg-gray-100',
})
</script>

<template>
  <div :class="`${bg} p-6 rounded-lg shadow-md`">
    <!-- slot - odpowiednik children -->
    <slot></slot>
  </div>
</template>
