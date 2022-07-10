<template>
  <div>{{ task }}</div>
</template>

<script setup>
const { task } = defineProps({
  task: String,
});
</script>
