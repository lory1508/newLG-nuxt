<template>
  <div
    class="w-full justify-center text-center flex flex-col gap-4 pt-16 pb-8 bg-gradient-to-r from-[#b1d698] to-[#ffb7e2]"
  >
    <div class="text-3xl font-mono">{{ title }}</div>
    <div v-if="subtitle">{{ subtitle }}</div>
    <pre>{{ gradient.from }}</pre>
    <pre>{{ gradient.to }}</pre>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  subtitle: {
    type: String,
    required: false,
  },
  image: {
    type: String,
    required: false,
  },
  gradient: {
    type: Object,
    required: false,
  },
});

const heroClasses = ref("");
</script>
