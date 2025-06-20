<template>
  <main>
    <h1>Task Manager</h1>
    <TaskForm @addTask="handleAddTask" />
    <h3>There are {{ tasks.length }} tasks in the list</h3>
    <TaskList
      :tasks="tasks"
      @toggleTask="handleToggleTask"
      @deleteTask="handleDeleteTask"
      @editTask="handleEditTask"
    />
  </main>
</template>

<script setup>
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
function handleAddTask(task) {
  tasks.value.push({
    id: Date.now(),
    text: task,
    done: false,
  });
  console.log("Current tasks:", tasks.value);
}

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
</style>
