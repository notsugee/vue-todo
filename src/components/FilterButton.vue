<script setup>
import { String } from "core-js";
import { defineProps, defineEmits } from "vue";

const emit = defineEmits(["filterTasks"]);
const props = defineProps({
  filter: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <button class="secondary" @click="emit('filterTasks', props.filter)">
    {{ props.filter }}
  </button>
</template>

<style scoped>
.secondary {
  text-transform: capitalize;
}
</style>
