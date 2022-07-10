<template>
  <li>{{ task }}</li>
</template>

<script setup>
const { task } = defineProps({
  task: String,
});
</script>
