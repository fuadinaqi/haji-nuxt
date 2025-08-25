<script setup>
definePageMeta({
  layout: false,
});

const currentTime = ref(new Date());
const currentDate = ref(new Date());

// Update waktu setiap detik
onMounted(() => {
  const timer = setInterval(() => {
    currentTime.value = new Date();
    currentDate.value = new Date();
  }, 1000);

  onUnmounted(() => clearInterval(timer));
});

// Format waktu
const formattedTime = computed(() => {
  const hours = currentTime.value.getHours().toString().padStart(2, "0");
  const minutes = currentTime.value.getMinutes().toString().padStart(2, "0");
  const seconds = currentTime.value.getSeconds().toString().padStart(2, "0");
  return { hours, minutes, seconds };
});

// Format tanggal
const formattedDate = computed(() => {
  const options = {
    weekday: "long",
    year: "numeric",
    month: "long",
    day: "numeric",
  };
  return currentDate.value.toLocaleDateString("id-ID", options);
});

// Handle Clock In/Out
const handleClockIn = () => {
  // TODO: Implementasi Clock In
  console.log("Clock In clicked");
};

const handleClockOut = () => {
  // TODO: Implementasi Clock Out
  console.log("Clock Out clicked");
};
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
        title="Presensi"
        description="Sistem pencatatan kehadiran karyawan"
      />

      <!-- Time Display Card -->
      <div class="mx-4 mb-6">
        <div class="rounded-2xl border border-gray-100 bg-white p-6 shadow-lg">
          <!-- Time -->
          <div class="mb-4 text-center">
            <div class="flex items-baseline justify-center space-x-2">
              <span class="text-6xl font-bold text-gray-800">{{
                formattedTime.hours
              }}</span>
              <span class="text-6xl font-bold text-gray-400">:</span>
              <span class="text-6xl font-bold text-gray-800">{{
                formattedTime.minutes
              }}</span>
              <span class="text-6xl font-bold text-gray-400">:</span>
              <span class="text-6xl font-bold text-gray-800">{{
                formattedTime.seconds
              }}</span>
            </div>
          </div>

          <!-- Date -->
          <div class="text-center">
            <p class="text-lg text-gray-600 capitalize">{{ formattedDate }}</p>
          </div>
        </div>
      </div>

      <!-- Clock In/Out Card -->
      <div class="mx-4">
        <div class="rounded-2xl border border-gray-100 bg-white p-6 shadow-lg">
          <h2 class="mb-4 text-center text-xl font-semibold text-gray-800">
            Status Kehadiran
          </h2>

          <div class="grid grid-cols-2 gap-4">
            <!-- Clock In Button -->
            <button
              class="transform rounded-xl bg-emerald-500 px-6 py-4 font-semibold text-white shadow-lg transition-all duration-200 hover:scale-105 hover:bg-emerald-600 hover:shadow-xl"
              @click="handleClockIn"
            >
              <div class="flex flex-col items-center">
                <UIcon name="lucide:log-in" class="mb-2 h-8 w-8" />
                <span class="text-lg">Clock In</span>
              </div>
            </button>

            <!-- Clock Out Button -->
            <button
              class="transform rounded-xl bg-red-500 px-6 py-4 font-semibold text-white shadow-lg transition-all duration-200 hover:scale-105 hover:bg-red-600 hover:shadow-xl"
              @click="handleClockOut"
            >
              <div class="flex flex-col items-center">
                <UIcon name="lucide:log-out" class="mb-2 h-8 w-8" />
                <span class="text-lg">Clock Out</span>
              </div>
            </button>
          </div>

          <!-- Status Info -->
          <div class="mt-6 rounded-xl bg-gray-50 p-4">
            <div class="flex items-center justify-center space-x-2">
              <UIcon name="lucide:info" class="h-8 w-8 text-gray-500" />
              <span class="text-sm text-gray-600"
                >Klik tombol di atas untuk mencatat kehadiran Anda</span
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>
