<template>
  <div>
    <p>
      {{ `${remainingTasks} ${remainingTasks > 1 ? "tasks" : "task"} left` }}
    </p>

    <div>
      <button type="button" data-filter="all">All</button>
      <button type="button" data-filter="active">Active</button>
      <button type="button" data-filter="completed">Completed</button>
    </div>

    <button type="button">Clear Completed</button>
  </div>
</template>

<script setup>
const { remainingTasks } = defineProps({
  remainingTasks: Number,
});
</script>
