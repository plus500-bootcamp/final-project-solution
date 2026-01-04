<template>
  <form class="add-task-form" @submit.prevent="handleSubmit">
    <div class="input-group">
      <input
        v-model="taskText"
        type="text"
        placeholder="Enter a new task..."
        required
      />
      <select v-model="priority" class="priority-select">
        <option value="low">Low</option>
        <option value="medium">Medium</option>
        <option value="high">High</option>
      </select>
      <button type="submit" class="add-btn">Add</button>
    </div>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue";
import type { Priority } from "../types";

const emit = defineEmits(["add-task"]);

const taskText = ref("");
const priority = ref<Priority>("low");

/**
 * Handle form submission and emit add-task event
 */
const handleSubmit = () => {
  const text = taskText.value.trim();
  if (!text) return;

  emit("add-task", {
    text,
    priority: priority.value,
  });

  // Reset form
  taskText.value = "";
  priority.value = "low";
};
</script>

<style scoped>
.add-task-form {
  margin-bottom: 0;
}

.input-group {
  display: flex;
  gap: 10px;
  align-items: stretch;
}

.input-group input[type="text"] {
  flex-grow: 1;
  padding: 12px 15px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 16px;
  transition: border-color 0.3s ease;
  min-width: 0;
}

.input-group input[type="text"]:focus {
  outline: none;
  border-color: #667eea;
}

.priority-select {
  padding: 12px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 16px;
  background-color: white;
  cursor: pointer;
  transition: border-color 0.3s ease;
}

.priority-select:focus {
  outline: none;
  border-color: #667eea;
}

.add-btn {
  padding: 12px 25px;
  background-color: #667eea;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(102, 126, 234, 0.3);
}

.add-btn:hover {
  background-color: #5568d3;
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(102, 126, 234, 0.4);
}

.add-btn:active {
  transform: translateY(2px);
  box-shadow: 0 2px 4px rgba(102, 126, 234, 0.3);
}

@media (max-width: 480px) {
  .input-group {
    flex-direction: column;
  }

  .input-group input[type="text"],
  .priority-select,
  .add-btn {
    width: 100%;
  }
}
</style>
