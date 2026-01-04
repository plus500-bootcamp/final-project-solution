<template>
  <ul class="task-list">
    <!-- Empty state -->
    <li v-if="tasks.length === 0" class="empty-state">No tasks to display</li>

    <!-- Task items -->
    <TaskItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @toggle-complete="$emit('toggle-complete', $event)"
    />
  </ul>
</template>

<script setup lang="ts">
import type { Task } from "../types";
import TaskItem from "./TaskItem.vue";

defineProps({
  tasks: {
    type: Array as () => Task[],
    required: true,
  },
});

defineEmits(["toggle-complete"]);
</script>

<style scoped>
.task-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.empty-state {
  text-align: center;
  padding: 40px 20px;
  color: #999;
  font-style: italic;
  font-size: 16px;
}
</style>
