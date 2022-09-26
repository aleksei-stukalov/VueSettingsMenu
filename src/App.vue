<script setup lang="ts">
import Settings from './components/Settings.vue'

// In the real world case this data would come from some server fetching.
let data = {
  theme: 0,
  background: 0,
  description: ''
}
</script>

<template>
  <Settings :data={data} />
</template>
