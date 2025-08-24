<script setup>
defineProps({
  name: {
    type: String,
    required: true,
  },
  className: {
    type: String,
    default: "",
  },
  to: {
    type: String,
    default: "",
  },
});
</script>

<template>
  <NuxtLink
    class="flex cursor-pointer flex-col items-center gap-2 transition-all duration-300 hover:scale-105 active:scale-105"
    :to="to"
  >
    <div
      class="flex size-12 items-center justify-center rounded-2xl"
      :class="className"
    >
      <slot name="icon" />
    </div>
    <span class="text-center text-xs font-medium text-neutral-600">{{
      name
    }}</span>
  </NuxtLink>
</template>
