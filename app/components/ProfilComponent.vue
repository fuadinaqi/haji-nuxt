<script setup>
// Data dummy untuk profil
const profileData = {
  nik: "198501152010012001",
  nama: "Ahmad Hidayat",
  email: "ahmad.hidayat@example.com",
  jabatan: "Kepala Seksi Kepegawaian",
  pangkat: "III/a - Penata Muda",
};
</script>

<template>
  <div class="mx-4 space-y-6">
    <!-- Header Profil -->
    <div class="text-center">
      <div
        class="from-primary-main to-secondary-main mx-auto mb-4 flex h-24 w-24 items-center justify-center rounded-full bg-gradient-to-br text-white"
      >
        <UIcon name="lucide:user" size="48" />
      </div>
      <h2 class="text-xl font-bold text-gray-800">{{ profileData.nama }}</h2>
      <p class="text-sm text-gray-600">{{ profileData.jabatan }}</p>
    </div>

    <!-- Informasi Profil -->
    <div class="space-y-4">
      <!-- NIK -->
      <div class="rounded-lg border border-gray-100 bg-white p-4 shadow-sm">
        <div class="flex items-center gap-3">
          <div
            class="flex h-10 w-10 items-center justify-center rounded-full bg-blue-100"
          >
            <UIcon name="lucide:id-card" class="h-5 w-5 text-blue-600" />
          </div>
          <div class="flex-1">
            <p class="text-sm font-medium text-gray-500">NIK</p>
            <p class="text-base font-semibold text-gray-800">
              {{ profileData.nik }}
            </p>
          </div>
        </div>
      </div>

      <!-- Nama -->
      <div class="rounded-lg border border-gray-100 bg-white p-4 shadow-sm">
        <div class="flex items-center gap-3">
          <div
            class="flex h-10 w-10 items-center justify-center rounded-full bg-green-100"
          >
            <UIcon name="lucide:user" class="h-5 w-5 text-green-600" />
          </div>
          <div class="flex-1">
            <p class="text-sm font-medium text-gray-500">Nama Lengkap</p>
            <p class="text-base font-semibold text-gray-800">
              {{ profileData.nama }}
            </p>
          </div>
        </div>
      </div>

      <!-- Email -->
      <div class="rounded-lg border border-gray-100 bg-white p-4 shadow-sm">
        <div class="flex items-center gap-3">
          <div
            class="flex h-10 w-10 items-center justify-center rounded-full bg-purple-100"
          >
            <UIcon name="lucide:mail" class="h-5 w-5 text-purple-600" />
          </div>
          <div class="flex-1">
            <p class="text-sm font-medium text-gray-500">Email</p>
            <p class="text-base font-semibold text-gray-800">
              {{ profileData.email }}
            </p>
          </div>
        </div>
      </div>

      <!-- Jabatan -->
      <div class="rounded-lg border border-gray-100 bg-white p-4 shadow-sm">
        <div class="flex items-center gap-3">
          <div
            class="flex h-10 w-10 items-center justify-center rounded-full bg-orange-100"
          >
            <UIcon name="lucide:briefcase" class="h-5 w-5 text-orange-600" />
          </div>
          <div class="flex-1">
            <p class="text-sm font-medium text-gray-500">Jabatan</p>
            <p class="text-base font-semibold text-gray-800">
              {{ profileData.jabatan }}
            </p>
          </div>
        </div>
      </div>

      <!-- Pangkat -->
      <div class="rounded-lg border border-gray-100 bg-white p-4 shadow-sm">
        <div class="flex items-center gap-3">
          <div
            class="flex h-10 w-10 items-center justify-center rounded-full bg-red-100"
          >
            <UIcon name="lucide:star" class="h-5 w-5 text-red-600" />
          </div>
          <div class="flex-1">
            <p class="text-sm font-medium text-gray-500">Pangkat/Golongan</p>
            <p class="text-base font-semibold text-gray-800">
              {{ profileData.pangkat }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
