<template>
  <div
    v-if="isLoading"
    class="bg-opacity-90 fixed inset-0 z-50 flex items-center justify-center bg-white"
  >
    <div class="text-center">
      <div class="mb-4">
        <UIcon
          name="lucide:loader-2"
          class="text-primary-main mx-auto h-8 w-8 animate-spin"
        />
      </div>
      <p class="text-gray-600">Memeriksa autentikasi...</p>
    </div>
  </div>
</template>

<script setup>
const { isLoading } = useAuth();
</script>
