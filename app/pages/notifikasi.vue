<script setup>
definePageMeta({
  layout: false,
});

// Dummy data untuk notifikasi
const notifications = ref([
  {
    id: 1,
    title: "Surat Disposisi Baru",
    message:
      "Surat nomor 001/2024 telah didisposisikan kepada Anda untuk ditindaklanjuti",
    type: "disposisi",
    timestamp: "2024-01-15T10:30:00",
    isRead: false,
    sender: "Sistem Persuratan",
  },
  {
    id: 2,
    title: "Surat Disposisi Penting",
    message:
      "Surat nomor 002/2024 tentang pengadaan barang telah didisposisikan",
    type: "disposisi",
    timestamp: "2024-01-15T09:15:00",
    isRead: false,
    sender: "Sistem Persuratan",
  },
  {
    id: 3,
    title: "Disposisi Surat Kepegawaian",
    message:
      "Surat nomor 003/2024 tentang mutasi pegawai memerlukan tindak lanjut",
    type: "disposisi",
    timestamp: "2024-01-15T07:00:00",
    isRead: true,
    sender: "Sistem Persuratan",
  },
  {
    id: 4,
    title: "Disposisi SOP Terbaru",
    message:
      "Surat nomor 004/2024 tentang update SOP telah didisposisikan untuk review",
    type: "disposisi",
    timestamp: "2024-01-14T16:45:00",
    isRead: true,
    sender: "Sistem Persuratan",
  },
  {
    id: 5,
    title: "Disposisi Laporan Keuangan",
    message:
      "Surat nomor 005/2024 tentang laporan keuangan triwulan IV memerlukan approval",
    type: "disposisi",
    timestamp: "2024-01-14T14:20:00",
    isRead: false,
    sender: "Sistem Persuratan",
  },
  {
    id: 6,
    title: "Disposisi Pengajuan Cuti",
    message:
      "Surat nomor 006/2024 tentang pengajuan cuti karyawan perlu ditindaklanjuti",
    type: "disposisi",
    timestamp: "2024-01-14T11:30:00",
    isRead: true,
    sender: "Sistem Persuratan",
  },
  {
    id: 7,
    title: "Disposisi Maintenance Sistem",
    message:
      "Surat nomor 007/2024 tentang jadwal maintenance sistem IT perlu koordinasi",
    type: "disposisi",
    timestamp: "2024-01-14T10:00:00",
    isRead: false,
    sender: "Sistem Persuratan",
  },
  {
    id: 8,
    title: "Disposisi Rapat Koordinasi",
    message:
      "Surat nomor 008/2024 tentang jadwal rapat koordinasi bulanan perlu konfirmasi",
    type: "disposisi",
    timestamp: "2024-01-14T08:00:00",
    isRead: true,
    sender: "Sistem Persuratan",
  },
]);

// State untuk filter dan search
const searchQuery = ref("");
const showUnreadOnly = ref(false);

// Filtered notifications
const filteredNotifications = computed(() => {
  let filtered = notifications.value;

  // Filter by search query
  if (searchQuery.value) {
    filtered = filtered.filter(
      (notification) =>
        notification.title
          .toLowerCase()
          .includes(searchQuery.value.toLowerCase()) ||
        notification.message
          .toLowerCase()
          .includes(searchQuery.value.toLowerCase()) ||
        notification.sender
          .toLowerCase()
          .includes(searchQuery.value.toLowerCase()),
    );
  }

  // Filter by read status
  if (showUnreadOnly.value) {
    filtered = filtered.filter((notification) => !notification.isRead);
  }

  return filtered;
});

// Mark notification as read
const markAsRead = (notification) => {
  notification.isRead = true;
};

// Mark all as read
const markAllAsRead = () => {
  notifications.value.forEach((notification) => {
    notification.isRead = true;
  });
};

// Get notification type color and icon
const getNotificationTypeInfo = (_type) => {
  return { color: "bg-blue-100 text-blue-800", icon: "lucide:send" };
};

// Format timestamp
const formatTimestamp = (timestamp) => {
  const date = new Date(timestamp);
  const now = new Date();
  const diffInHours = Math.floor((now - date) / (1000 * 60 * 60));

  if (diffInHours < 1) {
    return "Baru saja";
  } else if (diffInHours < 24) {
    return `${diffInHours} jam yang lalu`;
  } else {
    return date.toLocaleDateString("id-ID", {
      day: "numeric",
      month: "short",
      hour: "2-digit",
      minute: "2-digit",
    });
  }
};

// Unread count
const unreadCount = computed(() => {
  return notifications.value.filter((notification) => !notification.isRead)
    .length;
});
</script>

<template>
  <NuxtLayout name="default">
    <template #back-button>
      <NuxtLink to="/" class="flex">
        <UIcon name="lucide:arrow-left" size="24" class="h-6 w-6" />
      </NuxtLink>
    </template>
    <template #user-profile>
      <NuxtLink to="/kepegawaian/profil">
        <button>
          <UIcon
            name="material-symbols:account-circle"
            size="30"
            class="text-primary-main"
          />
        </button>
      </NuxtLink>
    </template>

    <div
      class="from-primary-light min-h-[calc(100vh-60px)] bg-gradient-to-b to-white pb-8"
    >
      <!-- Header -->
      <div class="mx-4 pt-6 pb-4 text-center">
        <h1 class="text-2xl font-bold text-gray-800">Notifikasi</h1>
        <p class="mt-1 text-gray-600">Kelola semua notifikasi sistem Anda</p>
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
              placeholder="Cari notifikasi..."
              class="focus:border-primary-500 focus:ring-primary-500 w-full rounded-lg border border-gray-300 py-2 pr-4 pl-10 text-sm focus:ring-1 focus:outline-none"
            />
          </div>

          <!-- Filter Controls -->
          <div class="flex flex-wrap items-center justify-end gap-3">
            <!-- Unread Only Toggle -->
            <!-- <label class="flex items-center">
              <input
                v-model="showUnreadOnly"
                type="checkbox"
                class="text-primary-600 focus:ring-primary-500 h-4 w-4 rounded border-gray-300"
              />
              <span class="ml-2 text-sm text-gray-700"
                >Hanya yang belum dibaca</span
              >
            </label> -->

            <!-- Mark All as Read -->
            <UButton
              v-if="unreadCount > 0"
              @click="markAllAsRead"
              color="primary"
              size="sm"
            >
              <UIcon name="lucide:check-check" class="mr-1 h-4 w-4" />
              Tandai semua dibaca
            </UButton>
          </div>
        </div>
      </div>

      <!-- Content Area -->
      <div class="mx-3 sm:mx-4">
        <!-- Notifications List -->
        <div class="space-y-3 sm:space-y-4">
          <!-- Empty State -->
          <div
            v-if="filteredNotifications.length === 0"
            class="py-8 text-center"
          >
            <UIcon
              name="lucide:bell-off"
              class="mx-auto mb-4 h-12 w-12 text-gray-300"
            />
            <h3 class="mb-2 text-lg font-medium text-gray-700">
              Tidak ada notifikasi
            </h3>
            <p class="text-gray-500">
              {{
                searchQuery || showUnreadOnly
                  ? "Coba ubah filter atau kata kunci pencarian"
                  : "Semua notifikasi sudah dibaca"
              }}
            </p>
          </div>

          <!-- Notification Items -->
          <div
            v-for="notification in filteredNotifications"
            :key="notification.id"
            :class="[
              'rounded-xl bg-white p-4 shadow-lg transition-all hover:shadow-xl sm:rounded-2xl sm:p-6',
              !notification.isRead ? 'border-primary-500 border-l-4' : '',
            ]"
            @click="markAsRead(notification)"
          >
            <div class="space-y-3">
              <!-- Header -->
              <div class="flex items-start justify-between gap-3">
                <div class="min-w-0 flex-1">
                  <div class="mb-2 flex items-center gap-2">
                    <span
                      :class="`inline-flex items-center rounded-full px-2.5 py-0.5 text-xs font-medium ${getNotificationTypeInfo(notification.type).color}`"
                    >
                      <UIcon
                        :name="getNotificationTypeInfo(notification.type).icon"
                        class="mr-1 h-3 w-3"
                      />
                      {{ notification.type }}
                    </span>
                    <span
                      v-if="!notification.isRead"
                      class="bg-primary-500 inline-flex h-2 w-2 rounded-full"
                    ></span>
                  </div>
                  <h3
                    class="mb-1 line-clamp-2 text-lg font-semibold text-gray-900"
                  >
                    {{ notification.title }}
                  </h3>
                </div>

                <!-- Timestamp -->
                <div class="text-right">
                  <p class="text-xs text-gray-500">
                    {{ formatTimestamp(notification.timestamp) }}
                  </p>
                </div>
              </div>

              <!-- Message -->
              <p class="line-clamp-3 text-sm text-gray-600">
                {{ notification.message }}
              </p>

              <!-- Footer -->
              <div
                class="flex items-center justify-between border-t border-gray-100 pt-2"
              >
                <div class="flex items-center gap-2 text-xs text-gray-500">
                  <UIcon name="lucide:user" class="h-3 w-3" />
                  <span>{{ notification.sender }}</span>
                </div>

                <div class="flex items-center gap-2">
                  <span
                    v-if="!notification.isRead"
                    class="text-primary-600 text-xs font-medium"
                  >
                    Belum dibaca
                  </span>
                  <!-- <UIcon
                    v-if="!notification.isRead"
                    name="lucide:arrow-right"
                    class="h-4 w-4 text-gray-400"
                  /> -->
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Summary -->
        <div class="mt-6 text-center">
          <p class="text-sm text-gray-500">
            Menampilkan {{ filteredNotifications.length }} dari
            {{ notifications.length }} notifikasi
            <span v-if="unreadCount > 0" class="text-primary-600 font-medium">
              ({{ unreadCount }} belum dibaca)
            </span>
          </p>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>
