<template>
  <div>
    <p>
      {{ `${remainingTasks} ${remainingTasks > 1 ? "tasks" : "task"} left` }}
    </p>

    <div>
      <button
        v-for="{ id, filter, label } in filters"
        @click="handleClick('filter', $event)"
        :key="id"
        type="button"
        :class="addFilterStyles(activeFilter, filter)"
        :data-filter="filter"
      >
        {{ label }}
      </button>
    </div>

    <button @click="handleClick('clear')" type="button">Clear Completed</button>
  </div>
</template>

<script setup>
const { remainingTasks } = defineProps({
  remainingTasks: Number,
  activeFilter: String,
});

const emit = defineEmits(["toggleFilter", "clearCompleted"]);

const filters = [
  { id: 1, filter: "all", label: "All" },
  { id: 2, filter: "active", label: "Active" },
  { id: 3, filter: "completed", label: "Completed" },
];

function addFilterStyles(activeFilter, filterName) {
  if (filterName === activeFilter) {
    return {
      "todoList__filter--active": true,
    };
  } else {
    return {
      "todoList__filter--active": false,
    };
  }
}

function handleClick(type, event = null) {
  switch (type) {
    case "filter":
      emit("toggleFilter", event.target.dataset.filter);
      break;
    case "clear":
      emit("clearCompleted");
      break;
    default:
      throw new Error("Invalid type for click.");
  }
}
</script>

<style>
.todoList__filter--active {
  border: 1px solid hsl(120, 54%, 33%);
  background-color: transparent;
}
</style>
