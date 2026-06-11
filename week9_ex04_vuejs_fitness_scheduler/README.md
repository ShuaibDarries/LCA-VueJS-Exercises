# FlexZone Fitness - Class Scheduler

A Vue 3 single-page application for managing fitness class schedules at FlexZone Fitness gym.

## Project Overview

This app allows gym staff to:
- View all scheduled fitness classes
- Add new class sessions with details (name, coach, date, time, capacity)
- Delete cancelled sessions
- Search/filter classes by coach name
- See the next upcoming session at a glance
- Persist data across browser sessions using localStorage

## Tech Stack

- **Vue 3** with Composition API
- **Vite** for fast development and building
- Pure Vue reactivity (no external validation libraries)

## Project Structure

```
week9_ex04_vuejs_fitness_scheduler/
├── index.html
├── package.json
├── vite.config.js
├── .gitignore
├── README.md
└── src/
    ├── main.js
    ├── App.vue
    └── components/
        ├── ClassForm.vue
        ├── ClassList.vue
        └── ClassCard.vue
```

## Installation & Run Instructions

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Run the development server:**
   ```bash
   npm run dev
   ```

3. **Build for production:**
   ```bash
   npm run build
   ```

## Features Implemented

### Required Features
- ✅ Add Class form with user input validation (all fields required)
- ✅ Dynamic schedule list that updates in real time
- ✅ Delete button for removing sessions
- ✅ Conditional rendering for empty states ("No sessions scheduled")
- ✅ Computed total session count
- ✅ Responsive layout for mobile and desktop screens

### Stretch Goals (Optional)
- ✅ Save and load sessions from localStorage
- ✅ Computed display of the next upcoming session
- ✅ Search bar / filter by coach name
- ✅ Animate session addition and deletion transitions

## Vue Concepts Used

- `v-model` for two-way form binding
- `v-for` for rendering the class list
- `v-if` / `v-else` for conditional rendering (empty state)
- `computed` properties for total count, filtering, and next upcoming session
- `methods` for add/delete actions
- `watch` for localStorage persistence
- `TransitionGroup` for animated list changes
- `props` and `emits` for parent-child component communication
- `reactive` for form and error state management

## Screenshot

*(Add a screenshot of your running app here before submission)*

## Author

FlexZone Fitness Scheduler - Vue.js Exercise
