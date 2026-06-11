<template>
  <div class="app-container">
    <header class="app-header">
      <h1>FlexZone Fitness</h1>
      <p class="subtitle">Class Schedule Manager</p>
    </header>

    <main class="main-content">
      <!-- Search Bar (Stretch Goal) -->
      <section class="search-section">
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search by coach name..."
          class="search-input"
        />
      </section>

      <!-- Add Class Form -->
      <ClassForm @add-class="addClass" />

      <!-- Stats Bar -->
      <section class="stats-bar">
        <div class="stat">
          <span class="stat-number">{{ totalSessions }}</span>
          <span class="stat-label">Total Sessions</span>
        </div>
        <div class="stat" v-if="nextUpcoming">
          <span class="stat-label">Next Up:</span>
          <span class="stat-highlight">{{ nextUpcoming.name }}</span>
          <span class="stat-time">{{ formatDateTime(nextUpcoming) }}</span>
        </div>
      </section>

      <!-- Class List -->
      <ClassList
        :classes="filteredClasses"
        @delete-class="deleteClass"
      />
    </main>

    <footer class="app-footer">
      <p>FlexZone Fitness &copy; 2026</p>
    </footer>
  </div>
</template>

<script>
import { ref, computed, onMounted, watch } from 'vue'
import ClassForm from './components/ClassForm.vue'
import ClassList from './components/ClassList.vue'

export default {
  name: 'App',
  components: {
    ClassForm,
    ClassList
  },
  setup() {
    // Reactive state for classes array
    const classes = ref([])
    const searchQuery = ref('')

    // Load from localStorage on mount (Stretch Goal)
    onMounted(() => {
      const saved = localStorage.getItem('flexzone-classes')
      if (saved) {
        try {
          classes.value = JSON.parse(saved)
        } catch (e) {
          console.error('Failed to load classes from localStorage')
        }
      }
    })

    // Save to localStorage whenever classes change (Stretch Goal)
    watch(classes, (newClasses) => {
      localStorage.setItem('flexzone-classes', JSON.stringify(newClasses))
    }, { deep: true })

    // Add a new class session
    const addClass = (newClass) => {
      const session = {
        id: Date.now(),
        ...newClass
      }
      classes.value.push(session)
    }

    // Delete a class session
    const deleteClass = (id) => {
      classes.value = classes.value.filter(c => c.id !== id)
    }

    // Computed: total number of sessions
    const totalSessions = computed(() => {
      return classes.value.length
    })

    // Computed: filtered classes by coach name (Stretch Goal)
    const filteredClasses = computed(() => {
      if (!searchQuery.value.trim()) {
        return classes.value
      }
      const query = searchQuery.value.toLowerCase()
      return classes.value.filter(c =>
        c.coach.toLowerCase().includes(query)
      )
    })

    // Computed: next upcoming session (Stretch Goal)
    const nextUpcoming = computed(() => {
      const now = new Date()
      const upcoming = classes.value.filter(c => {
        const sessionDate = new Date(`${c.date}T${c.time}`)
        return sessionDate > now
      })
      upcoming.sort((a, b) => {
        const dateA = new Date(`${a.date}T${a.time}`)
        const dateB = new Date(`${b.date}T${b.time}`)
        return dateA - dateB
      })
      return upcoming.length > 0 ? upcoming[0] : null
    })

    // Helper: format date and time for display
    const formatDateTime = (session) => {
      const date = new Date(`${session.date}T${session.time}`)
      return date.toLocaleString('en-US', {
        weekday: 'short',
        month: 'short',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
      })
    }

    return {
      classes,
      searchQuery,
      addClass,
      deleteClass,
      totalSessions,
      filteredClasses,
      nextUpcoming,
      formatDateTime
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f5f7fa;
  color: #333;
  line-height: 1.6;
}

.app-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.app-header {
  text-align: center;
  padding: 30px 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 12px;
  margin-bottom: 24px;
}

.app-header h1 {
  font-size: 2.2rem;
  margin-bottom: 8px;
}

.subtitle {
  font-size: 1.1rem;
  opacity: 0.9;
}

.main-content {
  flex: 1;
}

.search-section {
  margin-bottom: 20px;
}

.search-input {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s;
}

.search-input:focus {
  outline: none;
  border-color: #667eea;
}

.stats-bar {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.stat {
  background: white;
  padding: 16px 24px;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  display: flex;
  align-items: center;
  gap: 8px;
}

.stat-number {
  font-size: 1.8rem;
  font-weight: bold;
  color: #667eea;
}

.stat-label {
  color: #666;
  font-size: 0.95rem;
}

.stat-highlight {
  font-weight: bold;
  color: #764ba2;
}

.stat-time {
  color: #888;
  font-size: 0.85rem;
}

.app-footer {
  text-align: center;
  padding: 20px;
  color: #888;
  font-size: 0.9rem;
}

@media (max-width: 600px) {
  .app-header h1 {
    font-size: 1.6rem;
  }
  .stats-bar {
    flex-direction: column;
  }
}
</style>
