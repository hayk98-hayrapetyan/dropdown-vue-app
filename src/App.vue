<script setup lang="ts">
import type { DropDownOption } from '@/types';
import DynamicDropdownList from '@/components/DynamicDropdownList';
import { ref } from 'vue';

const options = ref<DropDownOption[]>([
  { key: "name", value: "Name" },
  { key: "age", value: "Age" },
  { key: "location", value: "Location" },
  { key: "occupation", value: "Occupation" },
  { key: "hobbies", value: "Hobbies" },
  { key: "favoriteColor", value: "Favorite Color" },
  { key: "height", value: "Height" },
  { key: "weight", value: "Weight" },
  { key: "education", value: "Education" },
  { key: "languages", value: "Languages" },
  { key: "company", value: "Company" },
  { key: "role", value: "Role" },
  { key: "experience", value: "Experience" },
  { key: "skills", value: "Skills" },
  { key: "favoriteBook", value: "Favorite Book" },
  { key: "favoriteFood", value: "Favorite Food" },
  { key: "pet", value: "Pet" },
  { key: "favoriteMovie", value: "Favorite Movie" },
  { key: "sports", value: "Sports" },
  { key: "zodiacSign", value: "Zodiac Sign" },
])
</script>

<template>
  <v-container class="pa-8">
    <DynamicDropdownList :options="options" />
  </v-container>
</template>
