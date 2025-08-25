<script setup>
definePageMeta({
  layout: false,
});

// Dummy data untuk list disposisi
const disposisiList = ref([
  {
    id: 1,
    nomor: "001/2024",
    perihal: "Surat Undangan Rapat Koordinasi",
    dari: "Sekretaris Daerah",
    tanggal: "2024-01-15",
    status: "pending",
    prioritas: "tinggi",
  },
  {
    id: 2,
    nomor: "002/2024",
    perihal: "Laporan Keuangan Triwulan IV",
    dari: "Badan Pengelola Keuangan",
    tanggal: "2024-01-14",
    status: "disposisi",
    prioritas: "sedang",
  },
  {
    id: 3,
    nomor: "003/2024",
    perihal: "Usulan Pengadaan Barang",
    dari: "Badan Pengadaan Barang",
    tanggal: "2024-01-13",
    status: "selesai",
    prioritas: "rendah",
  },
]);

// State untuk form
const showDisposisiForm = ref(false);
const showTTEForm = ref(false);
const selectedSurat = ref(null);

// Handle action buttons
const handleDisposisiClick = (item) => {
  selectedSurat.value = item;
  showDisposisiForm.value = true;
  showTTEForm.value = false;
};

const handleTTEClick = (item) => {
  selectedSurat.value = item;
  showTTEForm.value = true;
  showDisposisiForm.value = false;
};

// Close forms
const closeForms = () => {
  showDisposisiForm.value = false;
  showTTEForm.value = false;
  selectedSurat.value = null;
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
      <!-- <div class="mx-3 pt-4 pb-3 text-center sm:mx-4 sm:pt-6 sm:pb-4">
        <h1 class="text-xl font-bold text-gray-800 sm:text-2xl">Persuratan</h1>
        <p class="mt-1 text-sm text-gray-600 sm:text-base">
          Sistem pengelolaan surat dan disposisi
        </p>
      </div> -->
      <PageTitleComponent
        title="Persuratan"
        description="Sistem pengelolaan surat dan disposisi"
      />

      <!-- Content Area -->
      <div class="mx-3 mt-4 sm:mx-4">
        <!-- List Disposisi -->
        <div
          v-if="!showDisposisiForm && !showTTEForm"
          class="space-y-3 sm:space-y-4"
        >
          <div class="rounded-xl bg-white p-4 sm:rounded-2xl sm:p-6">
            <h2 class="mb-4 text-xl font-semibold text-gray-800">
              List Disposisi
            </h2>

            <div class="flex flex-col gap-2 space-y-3">
              <div
                v-for="item in disposisiList"
                :key="item.id"
                class="rounded-lg p-3 shadow-lg transition-colors hover:bg-gray-50 sm:p-4"
              >
                <div class="space-y-3">
                  <!-- Header dengan nomor dan badges -->
                  <div class="flex flex-wrap items-start justify-between gap-2">
                    <span
                      class="text-sm font-semibold text-gray-900 sm:text-base"
                      >{{ item.nomor }}</span
                    >
                    <!-- <div class="flex flex-wrap gap-1">
                      <span
                        :class="`inline-flex items-center rounded-full px-2 py-0.5 text-xs font-medium ${getStatusColor(item.status)}`"
                      >
                        {{ item.status }}
                      </span>
                      <span
                        :class="`inline-flex items-center rounded-full px-2 py-0.5 text-xs font-medium ${getPrioritasColor(item.prioritas)}`"
                      >
                        {{ item.prioritas }}
                      </span>
                    </div> -->
                  </div>

                  <!-- Content -->
                  <div class="flex flex-col gap-1 space-y-1">
                    <h3
                      class="line-clamp-2 text-sm font-medium text-gray-800 sm:text-base"
                    >
                      {{ item.perihal }}
                    </h3>
                    <p class="text-xs text-gray-600 sm:text-sm">
                      Dari: {{ item.dari }}
                    </p>
                    <p class="text-xs text-gray-500 sm:text-sm">
                      {{ new Date(item.tanggal).toLocaleDateString("id-ID") }}
                    </p>
                  </div>

                  <!-- Action Buttons -->
                  <div
                    class="mt-4 flex flex-col gap-2 sm:flex-row sm:justify-end"
                  >
                    <UButton
                      size="sm"
                      color="primary"
                      variant="outline"
                      @click="handleDisposisiClick(item)"
                      class="w-full sm:w-auto"
                    >
                      <UIcon name="lucide:send" class="mr-2 h-4 w-4" />
                      Disposisi
                    </UButton>
                    <UButton
                      size="sm"
                      color="emerald"
                      variant="outline"
                      @click="handleTTEClick(item)"
                      class="w-full sm:w-auto"
                    >
                      <UIcon name="lucide:pen-tool" class="mr-2 h-4 w-4" />
                      TTE
                    </UButton>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Form Disposisi -->
      <div v-if="showDisposisiForm" class="mx-3 mt-6 sm:mx-4">
        <div class="rounded-xl bg-white p-4 shadow-lg sm:rounded-2xl sm:p-6">
          <div class="mb-4 flex items-center justify-between">
            <h3 class="text-lg font-semibold text-gray-800">Form Disposisi</h3>
            <UButton
              color="gray"
              variant="ghost"
              icon="lucide:x"
              size="sm"
              @click="closeForms"
            />
          </div>

          <!-- Info Surat -->
          <div class="mb-4 rounded-lg bg-gray-50 p-3">
            <h4 class="mb-2 font-medium text-gray-900">Informasi Surat</h4>
            <div class="space-y-1 text-sm text-gray-600">
              <p>
                <span class="font-medium">Nomor:</span>
                {{ selectedSurat?.nomor }}
              </p>
              <p>
                <span class="font-medium">Perihal:</span>
                {{ selectedSurat?.perihal }}
              </p>
              <p>
                <span class="font-medium">Dari:</span> {{ selectedSurat?.dari }}
              </p>
            </div>
          </div>

          <!-- Form Fields -->
          <div class="space-y-4">
            <div>
              <label class="mb-1 block text-sm font-medium text-gray-700">
                Pilih Pegawai
              </label>
              <select
                class="focus:border-primary-500 focus:ring-primary-500 w-full rounded-lg border border-gray-300 px-3 py-2 text-sm focus:ring-1 focus:outline-none"
              >
                <option value="" disabled selected>
                  Pilih pegawai untuk disposisi
                </option>
                <option value="1">Ahmad Fauzi - Kepala Seksi</option>
                <option value="2">Siti Nurhaliza - Staff Administrasi</option>
                <option value="3">Budi Santoso - Analis</option>
                <option value="4">Dewi Sartika - Staff IT</option>
                <option value="5">Rudi Hermawan - Kepala Sub Bagian</option>
              </select>
            </div>

            <div>
              <label class="mb-1 block text-sm font-medium text-gray-700">
                Catatan Disposisi
              </label>
              <textarea
                rows="3"
                placeholder="Masukkan catatan atau instruksi disposisi..."
                class="focus:border-primary-500 focus:ring-primary-500 w-full resize-none rounded-lg border border-gray-300 px-3 py-2 text-sm focus:ring-1 focus:outline-none"
              ></textarea>
            </div>

            <div class="flex justify-end gap-2">
              <UButton color="gray" variant="outline" @click="closeForms">
                Batal
              </UButton>
              <UButton color="primary" @click="closeForms">
                Kirim Disposisi
              </UButton>
            </div>
          </div>
        </div>
      </div>

      <!-- Form TTE -->
      <div v-if="showTTEForm" class="mx-3 mt-6 sm:mx-4">
        <div class="rounded-xl bg-white p-4 shadow-lg sm:rounded-2xl sm:p-6">
          <div class="mb-4 flex items-center justify-between">
            <h3 class="text-lg font-semibold text-gray-800">
              Form Tanda Tangan Elektronik
            </h3>
            <UButton
              color="gray"
              variant="ghost"
              icon="lucide:x"
              size="sm"
              @click="closeForms"
            />
          </div>

          <!-- Info Surat -->
          <div class="mb-4 rounded-lg bg-gray-50 p-3">
            <h4 class="mb-2 font-medium text-gray-900">Informasi Surat</h4>
            <div class="space-y-1 text-sm text-gray-600">
              <p>
                <span class="font-medium">Nomor:</span>
                {{ selectedSurat?.nomor }}
              </p>
              <p>
                <span class="font-medium">Perihal:</span>
                {{ selectedSurat?.perihal }}
              </p>
              <p>
                <span class="font-medium">Dari:</span> {{ selectedSurat?.dari }}
              </p>
            </div>
          </div>

          <!-- Form Fields -->
          <div class="space-y-4">
            <div>
              <label class="mb-1 block text-sm font-medium text-gray-700">
                Upload File PDF
              </label>
              <input
                type="file"
                accept=".pdf"
                class="file:bg-primary-50 file:text-primary-700 hover:file:bg-primary-100 block w-full text-sm text-gray-500 file:mr-4 file:rounded-full file:border-0 file:px-4 file:py-2 file:text-sm file:font-semibold"
              />
              <p class="mt-1 text-xs text-gray-500">
                Hanya file PDF yang diperbolehkan
              </p>
            </div>

            <div>
              <label class="mb-1 block text-sm font-medium text-gray-700">
                Catatan TTE
              </label>
              <textarea
                rows="3"
                placeholder="Masukkan catatan untuk tanda tangan elektronik..."
                class="focus:border-primary-500 focus:ring-primary-500 w-full resize-none rounded-lg border border-gray-300 px-3 py-2 text-sm focus:ring-1 focus:outline-none"
              ></textarea>
            </div>

            <div class="flex justify-end gap-2">
              <UButton color="gray" variant="outline" @click="closeForms">
                Batal
              </UButton>
              <UButton color="primary" @click="closeForms">
                Submit TTE
              </UButton>
            </div>
          </div>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>
