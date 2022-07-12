<template>
  <form @submit.prevent="$emit('addTask')">
    <input
      :value="modelValue"
      @input="handleInput($event)"
      type="text"
      placeholder="Feed the dogs..."
    />

    <button type="submit">Add Task</button>
  </form>
</template>

<script setup>
defineProps(["modelValue"]);
const emit = defineEmits(["update:modelValue", "addTask"]);

function toProperCase(str) {
  if (!str) {
    return;
  }
  return `${str[0].toUpperCase()}${str.slice(1)}`;
}

function handleInput(event) {
  emit("update:modelValue", toProperCase(event.target.value));
}
</script>
