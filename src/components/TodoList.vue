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
const sampleData = ref([
  {
    id: 0,
    task: "Write a cool JS library",
    isFinished: false,
  },
  {
    id: 1,
    task: "Make it generic enough",
    isFinished: false,
  },
  {
    id: 2,
    task: "Write README",
    isFinished: false,
  },
  {
    id: 3,
    task: "Create some examples",
    isFinished: false,
  },
  {
    id: 4,
    task: "Spam in Twitter and IRC to promote it",
    isFinished: false,
  },
  {
    id: 5,
    task: "???",
    isFinished: false,
  },
  {
    id: 6,
    task: "PROFIT",
    isFinished: false,
  },
]);
const activeFilter = ref("all");
const itemIdCount = ref(sampleData.value.length);
const submitDisabled = computed(() => {
  if (!userInput.value) {
    return true;
  }

  return userInput.value.length <= 3;
});
const remainingTasks = computed(
  () => sampleData.value.filter((task) => task.isFinished === false).length
);

const filteredTasks = computed(() =>
  sampleData.value.filter((task) => {
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

  sampleData.value.unshift({
    id: itemIdCount.value++,
    task: userInput.value,
    isFinished: false,
  });
  userInput.value = "";
}

function toggleTask(id) {
  const updated = sampleData.value.map((task) => {
    if (task.id === id) {
      return {
        ...task,
        isFinished: !task.isFinished,
      };
    } else {
      return task;
    }
  });

  sampleData.value = updated;
}

function deleteTask(id) {
  const remainingTasks = sampleData.value.filter((task) => task.id !== id);

  sampleData.value = remainingTasks;
}

function toggleFilter(filter) {
  activeFilter.value = filter;
}

function clearCompleted() {
  const allActiveTasks = sampleData.value.filter(
    (task) => task.isFinished === false
  );

  sampleData.value = allActiveTasks;
}
</script>

<style>
.todoList {
  grid-area: 2;
  padding-inline: 2.4rem;
  margin-inline: auto;
  width: min(100%, 54rem);
}
</style>
