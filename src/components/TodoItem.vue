<template>
  <li class="todoItem" :class="{ 'todoItem--finished': isFinished }">
    <button
      @click="handleClick($event)"
      type="button"
      role="checkbox"
      aria-label="mark as done"
      :aria-checked="isFinished"
      data-label="toggle"
    >
      Toggle me
    </button>
    {{ task }}
    <button
      @click="handleClick($event)"
      type="button"
      aria-label="delete task"
      data-label="delete"
    >
      Do not click me
    </button>
  </li>
</template>

<script setup>
const { id, task, isFinished } = defineProps({
  id: Number,
  task: String,
  isFinished: Boolean,
});

const emit = defineEmits(["bubbleClick"]);

function handleClick(event) {
  emit("bubbleClick", { id, type: event.target.dataset.label });
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
