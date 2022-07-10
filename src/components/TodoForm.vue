<template>
  <form @submit.prevent="$emit('addTask')">
    <input
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      type="text"
      placeholder="Feed the dogs..."
    />

    <button type="submit">Add Task</button>
  </form>
</template>

<script setup>
defineProps(["modelValue"]);
defineEmits(["update:modelValue", "addTask"]);
</script>
