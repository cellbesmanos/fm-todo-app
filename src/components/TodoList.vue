<template>
  <TodoForm v-model="userInput" @add-task="addNewTask" />

  <TodoItemList @toggle-task="toggleTask" :tasks="filteredTasks">
    <TodoListToolbar
      @toggle-filter="toggleFilter"
      :remainingTasks="remainingTasks"
      :activeFilter="activeFilter"
    />
  </TodoItemList>
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
  sampleData.value.push({
    id: itemIdCount.value++,
    task: userInput.value,
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

function toggleFilter(filter) {
  activeFilter.value = filter;
}
</script>
