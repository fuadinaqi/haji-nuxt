<script setup>
definePageMeta({
  layout: false,
});

const { menu, getMenuIcon, activeTab, handleMenuSelect } = useKepegawaian();
const MENU = menu.value;
</script>

<template>
  <NuxtLayout name="default">
    <template #back-button>
      <NuxtLink to="/" class="flex">
        <UIcon name="lucide:arrow-left" size="24" class="h-6 w-6" />
      </NuxtLink>
    </template>

    <div
      class="from-primary-light min-h-[calc(100vh-60px)] bg-gradient-to-b to-white pb-8"
    >
      <!-- Header -->
      <PageTitleComponent
        title="Kepegawaian"
        description="Manajemen data kepegawaian dan administrasi"
      />

      <!-- Dropdown Menu Navigation -->
      <div class="mx-4 mb-6">
        <UDropdownMenu
          :items="
            MENU.map((item, index) => ({
              label: item.name,
              icon: getMenuIcon(item.name),
              onSelect: () => handleMenuSelect(index),
            }))
          "
          :ui="{
            content: 'w-80 max-h-96 overflow-y-auto',
          }"
        >
          <UButton
            :label="MENU[activeTab]?.name || 'Pilih Menu'"
            :icon="getMenuIcon(MENU[activeTab]?.name)"
            color="neutral"
            variant="solid"
            class="w-full justify-between"
          >
            <template #trailing>
              <UIcon name="lucide:chevron-down" class="h-4 w-4" />
            </template>
          </UButton>
        </UDropdownMenu>
      </div>

      <!-- Content Area -->
      <NuxtPage />
    </div>
  </NuxtLayout>
</template>
