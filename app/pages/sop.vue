<script setup>
definePageMeta({
  layout: false,
});

// Dummy data untuk list SOP
const sopList = ref([
  {
    id: 1,
    judul: "SOP Pengadaan Barang dan Jasa",
    kategori: "Pengadaan",
    versi: "v2.1",
    tanggal: "2024-01-15",
    ukuran: "2.5 MB",
    deskripsi:
      "Standar Operasional Prosedur untuk pengadaan barang dan jasa sesuai dengan peraturan yang berlaku",
    status: "aktif",
  },
  {
    id: 2,
    judul: "SOP Kepegawaian dan SDM",
    kategori: "Kepegawaian",
    versi: "v1.8",
    tanggal: "2024-01-10",
    ukuran: "1.8 MB",
    deskripsi:
      "Prosedur standar untuk pengelolaan kepegawaian dan sumber daya manusia",
    status: "aktif",
  },
  {
    id: 3,
    judul: "SOP Keuangan dan Anggaran",
    kategori: "Keuangan",
    versi: "v2.0",
    tanggal: "2024-01-05",
    ukuran: "3.2 MB",
    deskripsi:
      "Standar operasional untuk pengelolaan keuangan dan anggaran organisasi",
    status: "aktif",
  },
  {
    id: 4,
    judul: "SOP Pelayanan Publik",
    kategori: "Pelayanan",
    versi: "v1.5",
    tanggal: "2023-12-20",
    ukuran: "2.1 MB",
    deskripsi:
      "Prosedur standar untuk memberikan pelayanan publik yang berkualitas",
    status: "aktif",
  },
  {
    id: 5,
    judul: "SOP Pengawasan dan Audit",
    kategori: "Pengawasan",
    versi: "v1.9",
    tanggal: "2023-12-15",
    ukuran: "2.8 MB",
    deskripsi:
      "Standar operasional untuk kegiatan pengawasan dan audit internal",
    status: "aktif",
  },
]);

// State untuk search dan filter
const searchQuery = ref("");
const selectedKategori = ref("");

// Kategori yang tersedia
// const kategoriList = [
//   "Semua",
//   "Pengadaan",
//   "Kepegawaian",
//   "Keuangan",
//   "Pelayanan",
//   "Pengawasan",
// ];

// Filtered SOP list
const filteredSopList = computed(() => {
  let filtered = sopList.value;

  // Filter by search query
  if (searchQuery.value) {
    filtered = filtered.filter(
      (sop) =>
        sop.judul.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        sop.deskripsi.toLowerCase().includes(searchQuery.value.toLowerCase()),
    );
  }

  // Filter by kategori
  if (selectedKategori.value && selectedKategori.value !== "Semua") {
    filtered = filtered.filter(
      (sop) => sop.kategori === selectedKategori.value,
    );
  }

  return filtered;
});

// Handle download SOP
const handleDownload = (sop) => {
  // TODO: Implementasi download SOP
  console.log("Downloading SOP:", sop.judul);
  alert(`Memulai download SOP: ${sop.judul}`);
};

// Get kategori color
// const getKategoriColor = (kategori) => {
//   const colors = {
//     Pengadaan: "bg-blue-100 text-blue-800",
//     Kepegawaian: "bg-green-100 text-green-800",
//     Keuangan: "bg-purple-100 text-purple-800",
//     Pelayanan: "bg-orange-100 text-orange-800",
//     Pengawasan: "bg-red-100 text-red-800",
//   };
//   return colors[kategori] || "bg-gray-100 text-gray-800";
// };
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
      <div class="mx-3 pt-4 pb-3 text-center sm:mx-4 sm:pt-6 sm:pb-4">
        <h1 class="text-xl font-bold text-gray-800 sm:text-2xl">
          Standar Operasional Prosedur (SOP)
        </h1>
        <p class="mt-1 text-sm text-gray-600 sm:text-base">
          Dokumen standar operasional prosedur organisasi
        </p>
      </div>

      <!-- Search and Filter -->
      <div class="mx-3 mb-4 sm:mx-4 sm:mb-6">
        <div class="space-y-3">
          <!-- Search Bar -->
          <div class="relative">
            <UIcon
              name="lucide:search"
              class="absolute top-1/2 left-3 h-4 w-4 -translate-y-1/2 text-gray-400"
            />
            <input
              v-model="searchQuery"
              type="text"
              placeholder="Cari SOP berdasarkan judul atau deskripsi..."
              class="focus:border-primary-500 focus:ring-primary-500 w-full rounded-lg border border-gray-300 py-2 pr-4 pl-10 text-sm focus:ring-1 focus:outline-none"
            />
          </div>

          <!-- Filter Kategori -->
          <!-- <div class="flex flex-wrap gap-2">
            <button
              v-for="kategori in kategoriList"
              :key="kategori"
              @click="selectedKategori = kategori"
              :class="[
                'rounded-full px-3 py-1 text-xs font-medium transition-colors sm:text-sm',
                selectedKategori === kategori
                  ? 'bg-primary-500 text-white'
                  : 'bg-gray-100 text-gray-700 hover:bg-gray-200',
              ]"
            >
              {{ kategori }}
            </button>
          </div> -->
        </div>
      </div>

      <!-- Content Area -->
      <div class="mx-3 sm:mx-4">
        <!-- SOP List -->
        <div class="space-y-3 sm:space-y-4">
          <div v-if="filteredSopList.length === 0" class="py-8 text-center">
            <UIcon
              name="lucide:file-text"
              class="mx-auto mb-4 h-12 w-12 text-gray-300"
            />
            <h3 class="mb-2 text-lg font-medium text-gray-700">
              Tidak ada SOP ditemukan
            </h3>
            <p class="text-gray-500">
              Coba ubah kata kunci pencarian atau filter kategori
            </p>
          </div>

          <div
            v-for="sop in filteredSopList"
            :key="sop.id"
            class="rounded-xl bg-white p-4 shadow-lg transition-all hover:shadow-xl sm:rounded-2xl sm:p-6"
          >
            <div class="space-y-4">
              <!-- Header -->
              <div class="flex flex-wrap items-start justify-between gap-3">
                <div class="min-w-0 flex-1">
                  <!-- <div class="mb-2 flex items-center gap-2">
                    <span
                      :class="`inline-flex items-center rounded-full px-2.5 py-0.5 text-xs font-medium ${getKategoriColor(sop.kategori)}`"
                    >
                      {{ sop.kategori }}
                    </span>
                    <span class="text-xs text-gray-500">v{{ sop.versi }}</span>
                  </div> -->
                  <h3
                    class="mb-1 line-clamp-2 text-lg font-semibold text-gray-900"
                  >
                    {{ sop.judul }}
                  </h3>
                </div>

                <!-- Download Button -->
                <UButton
                  @click="handleDownload(sop)"
                  color="primary"
                  variant="solid"
                  size="sm"
                  class="flex-shrink-0"
                >
                  <UIcon name="lucide:download" class="mr-2 h-4 w-4" />
                  Download
                </UButton>
              </div>

              <!-- Description -->
              <p class="line-clamp-2 text-sm text-gray-600">
                {{ sop.deskripsi }}
              </p>

              <!-- Footer Info -->
              <div
                class="flex flex-wrap items-center justify-between gap-2 border-t border-gray-100 pt-2"
              >
                <div
                  class="flex items-center gap-4 text-xs text-gray-500 sm:text-sm"
                >
                  <div class="flex items-center gap-1">
                    <UIcon name="lucide:calendar" class="h-3 w-3" />
                    {{ new Date(sop.tanggal).toLocaleDateString("id-ID") }}
                  </div>
                  <!-- <div class="flex items-center gap-1">
                    <UIcon name="lucide:file" class="h-3 w-3" />
                    {{ sop.ukuran }}
                  </div> -->
                </div>

                <div class="flex items-center gap-1 text-xs text-green-600">
                  <UIcon name="lucide:check-circle" class="h-3 w-3" />
                  {{ sop.status }}
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Summary -->
        <div class="mt-6 text-center">
          <p class="text-sm text-gray-500">
            Menampilkan {{ filteredSopList.length }} dari
            {{ sopList.length }} SOP
          </p>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>
