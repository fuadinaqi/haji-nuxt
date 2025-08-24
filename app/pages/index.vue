<script setup>
const currentSlide = ref(0);
const slides = ["/images/haji-1.jpg", "/images/haji-3.jpeg"];

// Auto sliding banner
onMounted(() => {
  const interval = setInterval(() => {
    currentSlide.value = (currentSlide.value + 1) % slides.length;
  }, 5000);

  onUnmounted(() => clearInterval(interval));
});

// Menu data
const fixedMenus = [
  {
    name: "Presensi",
    icon: "lucide:alarm-clock-check",
    class: "bg-emerald-500",
    to: "/presensi",
  },
  {
    name: "Kepegawaian",
    icon: "lucide:users",
    class: "bg-teal-500",
    to: "/kepegawaian/profil",
  },
  {
    name: "Persuratan",
    icon: "lucide:file-text",
    class: "bg-green-500",
    to: "/persuratan",
  },
  {
    name: "SOP",
    icon: "lucide:newspaper",
    class: "bg-lime-500",
    to: "/sop",
  },
];

const dynamicMenus = [
  {
    name: "Hyperlink 1",
    icon: "lucide:chart-bar",
    class: "bg-emerald-600",
    to: "https://www.google.com",
  },
  {
    name: "Hyperlink 2",
    icon: "lucide:settings",
    class: "bg-teal-600",
    to: "https://www.google.com",
  },
  {
    name: "Hyperlink 3",
    icon: "lucide:info",
    class: "bg-green-600",
    to: "https://www.google.com",
  },
];
</script>

<template>
  <div
    class="from-primary-light min-h-[calc(100vh-60px)] bg-gradient-to-b to-white pb-8"
  >
    <!-- Banner Carousel -->
    <section class="mx-2 py-4">
      <div class="relative overflow-hidden rounded-2xl shadow-lg">
        <div class="relative h-48 sm:h-64 md:h-80 lg:h-96">
          <div
            v-for="(slide, index) in slides"
            :key="index"
            :class="[
              'absolute inset-0 transition-opacity duration-1000',
              index === currentSlide ? 'opacity-100' : 'opacity-0',
            ]"
          >
            <img
              :src="slide"
              :alt="`Slide ${index + 1}`"
              class="h-full w-full object-cover"
            />
            <div class="absolute inset-0 bg-black/20"></div>
          </div>

          <!-- Carousel Indicators -->
          <div
            class="absolute bottom-4 left-1/2 flex -translate-x-1/2 transform space-x-2"
          >
            <button
              v-for="(_, index) in slides"
              :key="index"
              :class="[
                'h-2 w-2 rounded-full transition-all',
                index === currentSlide ? 'w-6 bg-white' : 'bg-white/50',
              ]"
              @click="currentSlide = index"
            ></button>
          </div>
        </div>
      </div>
    </section>

    <!-- Fixed Menu Grid -->
    <section class="mx-2 rounded-md p-2">
      <div class="grid grid-cols-4 gap-2">
        <MenuItem
          v-for="menu in fixedMenus"
          :key="menu.name"
          :name="menu.name"
          :class-name="menu.class"
          :to="menu.to"
        >
          <template #icon>
            <UIcon :name="menu.icon" class="h-8/12 w-8/12 text-white" />
          </template>
        </MenuItem>
      </div>
    </section>

    <!-- Separator -->
    <div class="my-4 px-4">
      <div class="h-px bg-neutral-200"></div>
    </div>

    <!-- Dynamic Menu Grid -->
    <section class="mx-2 rounded-md p-2">
      <div class="grid grid-cols-4 gap-2">
        <MenuItem
          v-for="menu in dynamicMenus"
          :key="menu.name"
          :name="menu.name"
          :class-name="menu.class"
          :to="menu.to"
        >
          <template #icon>
            <UIcon :name="menu.icon" class="h-8/12 w-8/12 text-white" />
          </template>
        </MenuItem>
      </div>
    </section>
  </div>
</template>
