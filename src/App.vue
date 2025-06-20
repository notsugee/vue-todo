<template>
  <main>
    <h1>Task Manager</h1>
    <TaskForm @addTask="handleAddTask" />
    <h3>There are {{ tasks.length }} tasks in the list</h3>
    <div class="filter-btns">
      <FilterButton filter="all" @filterTasks="handleFilterTasks" />
      <FilterButton filter="active" @filterTasks="handleFilterTasks" />
      <FilterButton filter="completed" @filterTasks="handleFilterTasks" />
    </div>
    <TaskList
      :tasks="filteredTasks"
      @toggleTask="handleToggleTask"
      @deleteTask="handleDeleteTask"
      @editTask="handleEditTask"
    />
  </main>
</template>

<script setup>
import { computed, ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import FilterButton from "./components/FilterButton.vue";

const filter = ref("all");

function handleAddTask(task) {
  tasks.value.push({
    id: Date.now(),
    text: task,
    done: false,
  });
  console.log("Current tasks:", tasks.value);
}

const filteredTasks = computed(() => {
  switch (filter.value) {
    case "active":
      return tasks.value.filter((task) => !task.done);
    case "completed":
      return tasks.value.filter((task) => task.done);
    case "all":
      return tasks.value;
    default:
      return tasks.value;
  }
});

function handleToggleTask(id) {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.done = !task.done;
  }
  console.log("Current tasks after toggle:", tasks.value);
}

function handleDeleteTask(id) {
  tasks.value = tasks.value.filter((task) => task.id !== id);
  console.log("Current tasks after delete:", tasks.value);
}

function handleEditTask({ id, text }) {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.text = text;
  }
  console.log("Current tasks after edit:", tasks.value);
}

function handleFilterTasks(newFilter) {
  filter.value = newFilter;
}

const tasks = ref([]);
</script>

<style scoped>
main {
  max-width: 800px;
  margin: 20px auto;
}
h1 {
  text-align: center;
}
.filter-btns {
  display: flex;
  justify-content: center;
  gap: 10px;
}
</style>
