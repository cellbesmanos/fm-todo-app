<template>
  <li
    @click="handleClick"
    class="todoItem"
    :class="{ 'todoItem--finished': isFinished }"
  >
    {{ task }}
  </li>
</template>

<script setup>
const { id, task, isFinished } = defineProps({
  id: Number,
  task: String,
  isFinished: Boolean,
});

const emit = defineEmits(["bubbleClick"]);

function handleClick() {
  emit("bubbleClick", id);
}
</script>

<style>
.todoItem {
  cursor: pointer;
  transition: color 0.2s ease-in-out, text-decoration 0.2s ease-in-out;
}

.todoItem:hover,
.todoItem:focus {
  color: hsl(120, 54%, 33%);
}

.todoItem--finished {
  text-decoration: line-through;
}
</style>
