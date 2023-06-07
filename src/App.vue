<script setup lang="ts">
import { reactive } from 'vue';

const generateRandomId = () => crypto.randomUUID()

const dropdowns = reactive([
  { 
    value: '', 
    id: generateRandomId, 
    options: [
      { key: "Option 1", value: "Value 1" },
      { key: "Option 2", value: "Value 2" },
      { key: "Option 3", value: "Value 3" }
    ] 
  }
])
</script>

<template>
  <div>

  </div>
</template>

<style scoped>

</style>
