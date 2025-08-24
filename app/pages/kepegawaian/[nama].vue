<script setup>
const route = useRoute();
const nama = route.params.nama;
const { menu, getMenuIcon, activeTab } = useKepegawaian();
const MENU = menu.value;

onBeforeMount(() => {
  activeTab.value = MENU.findIndex((item) => item.to === nama);
});
</script>

<template>
  <div class="mx-4">
    <div class="rounded-2xl border border-gray-100 bg-white p-6 shadow-lg">
      <div class="mb-4 flex items-center justify-between">
        <h2 class="text-xl font-semibold text-gray-800">
          {{ MENU[activeTab]?.name }}
        </h2>
        <UIcon
          :name="getMenuIcon(MENU[activeTab]?.name)"
          class="h-6 w-6 text-gray-500"
        />
      </div>

      <div class="py-8 text-center">
        <UIcon
          :name="getMenuIcon(MENU[activeTab]?.name)"
          class="mx-auto mb-4 h-16 w-16 text-gray-300"
        />
        <h3 class="mb-2 text-lg font-medium text-gray-700">
          {{ MENU[activeTab]?.name }}
        </h3>
        <p class="text-gray-500">
          Halaman ini akan menampilkan informasi
          {{ MENU[activeTab]?.name.toLowerCase() }}
        </p>
      </div>
    </div>
  </div>
</template>
