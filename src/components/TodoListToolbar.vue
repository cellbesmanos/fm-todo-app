<template>
  <div class="todoList__toolbar">
    <p>
      {{ `${remainingTasks} ${remainingTasks > 1 ? "tasks" : "task"} left` }}
    </p>

    <div class="todoList__toolbar-filters">
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
.todoList__toolbar {
  --padding: 2.4rem;

  position: relative;

  display: flex;
  align-items: center;
  justify-content: space-between;
  min-height: 5rem;
  padding-inline: var(--padding);

  font-size: 1.2rem;
  font-weight: var(--fw-400);

  border-bottom-left-radius: var(--bradius);
  border-bottom-right-radius: var(--bradius);
  background-color: white;
  box-shadow: var(--bshadow);
}

@media screen and (min-width: 34.375em) {
  .todoList__toolbar {
    font-size: 1.3rem;
  }
}

.todoList__toolbar button {
  padding-block-start: 0.4rem;
  font-size: inherit;
  color: var(--clr-blue-gray-600);
  transition: color 0.2s ease-in-out;
}

.todoList__toolbar button:hover,
.todoList__toolbar button:focus {
  color: var(--clr-blue-gray-500);
}

.todoList__toolbar-filters {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1.6rem;
}

@media screen and (max-width: 31.25em) {
  .todoList__toolbar-filters {
    position: absolute;
    top: calc(4.8rem + 1.6rem);
    left: 0;
    width: 100%;
    min-height: 4.8rem;
    border-radius: inherit;
    background-color: inherit;
    box-shadow: inherit;
  }
}

.todoList__toolbar-filters button {
  font-weight: var(--fw-500);
}

button.todoList__filter--active {
  color: var(--clr-blue);
}
</style>
