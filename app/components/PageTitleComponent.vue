<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="mx-4 pt-6 pb-4 text-center">
    <h1 class="text-2xl font-bold text-gray-800">{{ title }}</h1>
    <p class="mt-1 text-gray-600">{{ description }}</p>
  </div>
</template>
