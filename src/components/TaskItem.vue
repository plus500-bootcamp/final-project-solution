<template>
  <li class="task-item" :data-priority="task.priority">
    <input
      :id="`task-${task.id}`"
      :checked="task.completed"
      type="checkbox"
      class="task-checkbox"
      @change="toggleComplete"
    />
    <label :for="`task-${task.id}`" class="task-label">
      <span class="task-text">{{ task.text }}</span>
      <span class="priority-badge" :data-priority="task.priority">
        {{ task.priority }}
      </span>
    </label>
  </li>
</template>

<script setup lang="ts">
import type { Task } from "../types";

const props = defineProps({
  task: {
    type: Object as () => Task,
    required: true,
  },
});

const emit = defineEmits(["toggle-complete"]);

/**
 * Toggle task completion status
 */
const toggleComplete = () => {
  emit("toggle-complete", props.task.id);
};
</script>

<style scoped>
.task-item {
  display: flex;
  align-items: center;
  padding: 18px 30px;
  border-bottom: 1px solid #f0f0f0;
  transition: background-color 0.2s ease;
  animation: slideIn 0.3s ease;
}

.task-item:hover {
  background-color: #f9f9f9;
}

.task-item:last-child {
  border-bottom: none;
}

.task-checkbox {
  width: 20px;
  height: 20px;
  margin-right: 15px;
  cursor: pointer;
  accent-color: #667eea;
}

.task-label {
  flex-grow: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
  font-size: 16px;
  color: #333;
}

.task-text {
  transition: all 0.3s ease;
}

/* Completed task styling */
.task-checkbox:checked + .task-label .task-text {
  text-decoration: line-through;
  color: #999;
  opacity: 0.6;
}

/* Priority Badge */
.priority-badge {
  font-size: 12px;
  padding: 4px 12px;
  border-radius: 12px;
  font-weight: bold;
  margin-left: 10px;
}

.priority-badge[data-priority="high"] {
  background-color: #fee;
  color: #c33;
  border: 1px solid #fcc;
}

.priority-badge[data-priority="medium"] {
  background-color: #fff4e6;
  color: #d97706;
  border: 1px solid #fed7aa;
}

.priority-badge[data-priority="low"] {
  background-color: #f0f9ff;
  color: #0369a1;
  border: 1px solid #bae6fd;
}

/* Task item priority border */
.task-item[data-priority="high"] {
  border-left: 4px solid #c33;
}

.task-item[data-priority="medium"] {
  border-left: 4px solid #d97706;
}

.task-item[data-priority="low"] {
  border-left: 4px solid #0369a1;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 480px) {
  .task-item {
    padding: 15px;
  }

  .task-label {
    flex-direction: column;
    align-items: flex-start;
    gap: 8px;
  }

  .priority-badge {
    margin-left: 0;
  }
}
</style>
