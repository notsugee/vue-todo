<template>
  <div class="task-list">
    <article v-for="task in props.tasks" :key="task.id">
      <input
        type="checkbox"
        :checked="task.done"
        @change="() => emit('toggleTask', task.id)"
      />
      <span v-if="editingId !== task.id" :class="{ done: task.done }">
        {{ task.text }}
      </span>
      <input
        v-else
        v-model="editText"
        @keyup.enter="saveEdit(task)"
        class="edit-input"
      />
      <div class="btns">
        <button v-if="editingId !== task.id" @click="startEdit(task)">
          Edit
        </button>
        <button v-else @click="saveEdit(task)">Save</button>
        <button @click="emit('deleteTask', task.id)">Delete</button>
      </div>
    </article>
  </div>
</template>

<script setup lang="js">
import { ref } from "vue";
import { defineProps } from "vue";
import { defineEmits } from "vue";

const emit = defineEmits(["toggleTask", "deleteTask", "editTask"]);
const props = defineProps({
  tasks: {
    type: Array,
    required: true
  }
});

const editingId = ref(null);
const editText = ref("");

function startEdit(task) {
  editingId.value = task.id;
  editText.value = task.text;
}

function saveEdit(task) {
  if (editText.value.trim() && editText.value !== task.text) {
    emit("editTask", { id: task.id, text: editText.value });
    editingId.value = null;
  }
}
</script>

<style scoped>
.done {
  text-decoration: line-through;
  color: gray;
}

.btns {
  display: flex;
  gap: 10px;
  justify-content: end;
}
</style>
