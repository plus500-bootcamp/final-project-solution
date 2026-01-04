<template>
  <div class="filter-controls">
    <button
      class="filter-btn"
      :class="{ active: currentStatus === 'all' }"
      @click="updateStatus('all')"
    >
      All
    </button>
    <button
      class="filter-btn"
      :class="{ active: currentStatus === 'uncompleted' }"
      @click="updateStatus('uncompleted')"
    >
      Uncompleted
    </button>
    <select
      :value="currentPriority"
      class="priority-select"
      @change="updatePriority($event)"
    >
      <option value="all">All Priorities</option>
      <option value="high">High</option>
      <option value="medium">Medium</option>
      <option value="low">Low</option>
    </select>
  </div>
</template>

<script setup lang="ts">
import type { FilterStatus } from "../types";

defineProps({
  currentStatus: {
    type: String,
    required: true,
  },
  currentPriority: {
    type: String,
    required: true,
  },
});

const emit = defineEmits(["update:status", "update:priority"]);

/**
 * Update the status filter
 */
const updateStatus = (status: FilterStatus) => {
  emit("update:status", status);
};

/**
 * Update the priority filter
 */
const updatePriority = (event: Event) => {
  const target = event.target as HTMLSelectElement;
  emit("update:priority", target.value);
};
</script>

<style scoped>
.filter-controls {
  display: flex;
  gap: 10px;
  margin-top: 15px;
  align-items: center;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 8px 16px;
  border: 2px solid #e0e0e0;
  background: white;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: all 0.3s ease;
}

.filter-btn:hover {
  border-color: #667eea;
}

.filter-btn.active {
  background: #667eea;
  color: white;
  border-color: #667eea;
}

.priority-select {
  padding: 8px 12px;
  border: 2px solid #e0e0e0;
  border-radius: 6px;
  font-size: 14px;
  background-color: white;
  cursor: pointer;
  transition: border-color 0.3s ease;
}

.priority-select:focus {
  outline: none;
  border-color: #667eea;
}
</style>
