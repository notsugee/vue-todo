<template>
  <div>
    <form @submit.prevent="formSubmitted">
      <div>
        <label>
          <input v-model="newTask" name="newTask" placeholder="I have to..." />
        </label>
      </div>
    </form>
  </div>
</template>

<script setup lang="js">
import { ref } from "vue";
import defineEmits from "vue";
const newTask = ref("");

const emit = defineEmits(["addTask"]);

function formSubmitted() {
  emit("addTask", newTask.value);
  newTask.value = "";
}
</script>
