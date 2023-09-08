<script setup>
const props = defineProps({
  tasks: Object,
});
</script>
<template>
  <div class="bg-white w-full shadow-md rounded-md p-4">
    <p class="text-2xl hover:text-gray-300 transition-all">{{ tasks.item }}</p>
  </div>
</template>

<style></style>
