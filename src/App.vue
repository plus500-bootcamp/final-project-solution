<template>
  <div class="app-container">
    <!-- Header with form and filters -->
    <header class="sticky-header">
      <h1>My Tasks</h1>

      <!-- Add Task Form Component -->
      <TaskForm @add-task="addTask" />

      <!-- Filter Controls Component -->
      <FilterControls
        :current-status="filter.status"
        :current-priority="filter.priority"
        @update:status="filter.status = $event"
        @update:priority="filter.priority = $event"
      />
    </header>

    <!-- Task List Component -->
    <TaskList :tasks="filteredTasks" @toggle-complete="toggleTaskComplete" />
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, computed, onMounted } from "vue";
import type { Task, Filter, Priority } from "./types";
import TaskForm from "./components/TaskForm.vue";
import FilterControls from "./components/FilterControls.vue";
import TaskList from "./components/TaskList.vue";

// Reactive state for tasks
const tasks = ref<Task[]>([]);

// Filter state
const filter = reactive<Filter>({
  status: "all",
  priority: "all",
});

/**
 * Load initial tasks from JSON file
 */
const loadTasks = async () => {
  try {
    const response = await fetch("/tasks.json");
    tasks.value = await response.json();
  } catch (error) {
    console.log("No tasks.json found, starting with empty list");
    tasks.value = [];
  }
};

/**
 * Computed property that filters tasks based on current filter state
 */
const filteredTasks = computed(() => {
  return tasks.value.filter((task) => {
    // Filter by completion status
    if (filter.status === "uncompleted" && task.completed) {
      return false;
    }

    // Filter by priority
    if (filter.priority !== "all" && task.priority !== filter.priority) {
      return false;
    }

    return true;
  });
});

/**
 * Add a new task to the list
 */
const addTask = (taskData: { text: string; priority: Priority }) => {
  const newTask: Task = {
    id: Date.now().toString(),
    text: taskData.text,
    priority: taskData.priority,
    completed: false,
    createdAt: Date.now(),
  };

  tasks.value.unshift(newTask);
};

/**
 * Toggle task completion status
 */
const toggleTaskComplete = (taskId: string) => {
  const task = tasks.value.find((t) => t.id === taskId);
  if (task) {
    task.completed = !task.completed;
  }
};

// Load tasks on component mount
onMounted(() => {
  loadTasks();
});
</script>

<style scoped>
/* Main Container */
.app-container {
  background-color: #ffffff;
  width: 90%;
  min-height: 100vh;
  margin: 0 auto;
}

/* Sticky Header */
.sticky-header {
  position: sticky;
  top: 0;
  background-color: #ffffff;
  z-index: 100;
  padding: 30px 30px 20px;
  border-bottom: 2px solid #f0f0f0;
}

.sticky-header h1 {
  color: #667eea;
  font-size: 2rem;
  margin-bottom: 20px;
  text-align: center;
}

@media (max-width: 480px) {
  .sticky-header {
    padding: 20px 15px 15px;
  }

  .sticky-header h1 {
    font-size: 1.5rem;
  }
}
</style>

<style>
/* Global styles */
body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  background: #667eea;
  min-height: 100vh;
  padding: 0;
  margin: 0;
}
</style>
