<script setup>
definePageMeta({
  layout: false,
});

const { logout } = useAuth();
</script>

<template>
  <NuxtLayout name="default">
    <template #back-button>
      <NuxtLink to="/" class="flex">
        <UIcon name="lucide:arrow-left" size="24" class="h-6 w-6" />
      </NuxtLink>
    </template>

    <template #user-profile>
      <UButton
        color="gray"
        variant="ghost"
        icon="lucide:log-out"
        @click="logout"
      >
        Logout
      </UButton>
    </template>

    <div
      class="from-primary-light min-h-[calc(100vh-60px)] bg-gradient-to-b to-white pt-4 pb-8"
    >
      <!-- Komponen Profil -->
      <ProfilComponent />
    </div>
  </NuxtLayout>
</template>
