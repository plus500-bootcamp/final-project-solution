# TaskMaster Vue

A task management application built with **Vue 2.7**, **TypeScript**, and **Composition API**.

## 🎯 Project Description

This is a recreation of the reactive-programming project, rebuilt using Vue 2.7's Composition API instead of RxJS. The application demonstrates reactive state management using Vue's built-in reactivity system.

## ✨ Features

- ✅ **Add tasks** with priority selection (Low/Medium/High)
- ✅ **Toggle completion** status with checkboxes
- ✅ **Filter by status**: Show all tasks or only uncompleted
- ✅ **Filter by priority**: Filter by High/Medium/Low
- ✅ **Reactive updates**: UI automatically updates when state changes
- ✅ **Local data**: Tasks loaded from JSON file
- ✅ **Responsive design**: Works on all screen sizes

## 🔧 Technology Stack

- **Vue 2.7.16**: Progressive JavaScript framework
- **TypeScript**: Type-safe development
- **Composition API**: Modern Vue composition pattern
- **Webpack 5**: Module bundler
- **CSS3**: Modern styling with animations

## 🚀 Getting Started

### Install Dependencies

```bash
npm install
```

### Development Server

```bash
npm run dev
```

The app will open at `http://localhost:8080`

### Build for Production

```bash
npm run build
```

## 📂 Project Structure

```
final-project/
├── public/
│   ├── index.html        # HTML template
│   └── tasks.json        # Initial tasks data
├── src/
│   ├── components/
│   │   ├── TaskForm.vue       # Form for adding new tasks
│   │   ├── FilterControls.vue # Status and priority filters
│   │   ├── TaskList.vue       # Container for task items
│   │   └── TaskItem.vue       # Individual task component
│   ├── App.vue           # Main application component
│   ├── main.ts           # Application entry point
│   ├── types.ts          # TypeScript type definitions
│   └── vue-shims.d.ts    # Vue TypeScript declarations
├── package.json          # Dependencies and scripts
├── tsconfig.json         # TypeScript configuration
├── webpack.config.js     # Webpack configuration
└── README.md             # Documentation
```

## 🎨 Vue Composition API Usage

### Reactive State

```typescript
const tasks = ref<Task[]>([]);
const filter = reactive<Filter>({ status: 'all', priority: 'all' });
```

### Computed Properties

```typescript
const filteredTasks = computed(() => {
  return tasks.value.filter(task => /* filter logic */);
});
```

### Lifecycle Hooks

```typescript
onMounted(() => {
  loadTasks();
});
```

## 📊 Data Flow

1. **Page Load**: Fetch `tasks.json` → populate reactive state
2. **Add Task**: User submits → update `tasks` ref → UI auto-updates
3. **Toggle Checkbox**: v-model updates task → computed property recalculates
4. **Change Filter**: Update filter state → computed property recalculates → UI updates

## 🎓 Key Vue Concepts Used

- **Composition API**: `ref`, `reactive`, `computed`, `onMounted`
- **Component Architecture**: Modular, reusable components
- **Props**: Pass data from parent to child components
- **Custom Events**: Child-to-parent communication with `emit`
- **Two-way binding**: `v-model` for form inputs
- **Event handling**: `@submit`, `@click` for user interactions
- **Conditional rendering**: `v-if` for empty state
- **List rendering**: `v-for` with component iteration
- **Dynamic classes**: `:class` for active states
- **Dynamic attributes**: `:data-priority` for styling

## 📦 Component Structure

### App.vue
Main container component that manages application state and coordinates child components.

### TaskForm.vue
Handles task creation with text input and priority selection. Emits `add-task` event with task data.

### FilterControls.vue
Provides UI for filtering tasks by status (All/Uncompleted) and priority. Emits filter update events.

### TaskList.vue
Renders the list of tasks and handles empty state. Passes through toggle events from child items.

### TaskItem.vue
Displays individual task with checkbox, text, and priority badge. Emits `toggle-complete` event.

## ✅ Code Quality

- **TypeScript**: Full type safety with interfaces
- **Clean code**: Well-commented and organized
- **Vue conventions**: Follows Vue style guide
- **Minimal config**: Simple TypeScript and Webpack setup
- **No external state management**: Uses Vue's built-in reactivity
- **No RxJS**: Pure Vue Composition API

## 🎯 Differences from Original

- **No RxJS**: Uses Vue's reactivity instead of observables
- **TypeScript**: Type-safe development
- **Single File Components**: Vue's `.vue` format
- **Composition API**: Modern Vue pattern (not Options API)
- **Webpack**: Module bundler for TypeScript and Vue

## 📝 Notes

- Vue 2.7 includes Composition API built-in (no need for @vue/composition-api plugin in runtime)
- TypeScript configuration is minimal as requested
- No verbose debugging or validation code
- Clean, production-ready code with proper comments
