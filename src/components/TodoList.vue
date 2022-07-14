<template>
  <div class="todoList">
    <TodoForm
      v-model="userInput"
      @add-task="addNewTask"
      :submitDisabled="submitDisabled"
    />

    <TodoItemList
      @toggle-task="toggleTask"
      @delete-task="deleteTask"
      :tasks="filteredTasks"
    >
      <TodoListToolbar
        @toggle-filter="toggleFilter"
        @clear-completed="clearCompleted"
        :remainingTasks="remainingTasks"
        :activeFilter="activeFilter"
      />
    </TodoItemList>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import TodoItemList from "./TodoItemList.vue";
import TodoForm from "./TodoForm.vue";
import TodoListToolbar from "./TodoListToolbar.vue";

const userInput = ref("");
const initialData = ref([
  {
    id: 0,
    task: "Complete online JavaScript course",
    isFinished: true,
  },
  {
    id: 1,
    task: "Jog around the park 3x",
    isFinished: false,
  },
  {
    id: 2,
    task: "10 minutes meditation",
    isFinished: false,
  },
  {
    id: 3,
    task: "Read for 1 hour",
    isFinished: false,
  },
  {
    id: 4,
    task: "Pick up groceries",
    isFinished: false,
  },
  {
    id: 5,
    task: "Complete Todo App on Frontend Mentor",
    isFinished: true,
  },
  {
    id: 6,
    task: "Learn Vue Router v4",
    isFinished: false,
  },
]);
const activeFilter = ref("all");
const itemIdCount = ref(initialData.value.length);
const submitDisabled = computed(() => {
  if (!userInput.value) {
    return true;
  }

  return userInput.value.length <= 3;
});
const remainingTasks = computed(
  () => initialData.value.filter((task) => task.isFinished === false).length
);

const filteredTasks = computed(() =>
  initialData.value.filter((task) => {
    if (activeFilter.value === "active") {
      if (task.isFinished === false) {
        return task;
      }
    } else if (activeFilter.value === "completed") {
      if (task.isFinished === true) {
        return task;
      }
    } else {
      return task;
    }
  })
);

function addNewTask() {
  if (!userInput.value) {
    return;
  }

  initialData.value.unshift({
    id: itemIdCount.value++,
    task: userInput.value,
    isFinished: false,
  });
  userInput.value = "";
}

function toggleTask(id) {
  const updated = initialData.value.map((task) => {
    if (task.id === id) {
      return {
        ...task,
        isFinished: !task.isFinished,
      };
    } else {
      return task;
    }
  });

  initialData.value = updated;
}

function deleteTask(id) {
  const remainingTasks = initialData.value.filter((task) => task.id !== id);

  initialData.value = remainingTasks;
}

function toggleFilter(filter) {
  activeFilter.value = filter;
}

function clearCompleted() {
  const allActiveTasks = initialData.value.filter(
    (task) => task.isFinished === false
  );

  initialData.value = allActiveTasks;
}
</script>

<style>
.todoList {
  grid-row-start: 2;
  grid-column-start: 1;
  grid-column-end: 2;
  padding-inline: 2.4rem;
  margin-inline: auto;
  width: min(100%, 54rem);
}
</style>
