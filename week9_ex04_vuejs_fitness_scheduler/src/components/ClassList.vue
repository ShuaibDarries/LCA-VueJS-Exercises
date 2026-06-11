<template>
  <section class="list-section">
    <h2>Scheduled Classes</h2>

    <!-- Empty state with v-if -->
    <div v-if="classes.length === 0" class="empty-state">
      <div class="empty-icon">📅</div>
      <p class="empty-title">No sessions scheduled</p>
      <p class="empty-subtitle">Use the form above to add your first class!</p>
    </div>

    <!-- Class list with v-for and transition-group (Stretch Goal: animation) -->
    <TransitionGroup
      v-else
      name="list"
      tag="div"
      class="class-grid"
    >
      <ClassCard
        v-for="classItem in classes"
        :key="classItem.id"
        :class-item="classItem"
        @delete-class="$emit('delete-class', classItem.id)"
      />
    </TransitionGroup>
  </section>
</template>

<script>
import ClassCard from './ClassCard.vue'

export default {
  name: 'ClassList',
  components: {
    ClassCard
  },
  props: {
    classes: {
      type: Array,
      required: true
    }
  },
  emits: ['delete-class']
}
</script>

<style scoped>
.list-section {
  background: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.08);
}

.list-section h2 {
  margin-bottom: 20px;
  color: #333;
  font-size: 1.3rem;
}

.empty-state {
  text-align: center;
  padding: 50px 20px;
  color: #888;
}

.empty-icon {
  font-size: 3rem;
  margin-bottom: 12px;
}

.empty-title {
  font-size: 1.2rem;
  font-weight: 600;
  color: #555;
  margin-bottom: 6px;
}

.empty-subtitle {
  font-size: 0.95rem;
}

.class-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 16px;
}

/* Transition animations for list items (Stretch Goal) */
.list-enter-active,
.list-leave-active {
  transition: all 0.4s ease;
}

.list-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.list-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

.list-move {
  transition: transform 0.4s ease;
}
</style>
