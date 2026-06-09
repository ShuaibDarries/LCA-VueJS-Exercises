<
<template>
  <div class="filter-bar">
    <div class="filter-group">
      <label class="filter-label">Filter by:</label>
      <div class="filter-buttons">
        <button
          v-for="level in skillLevels"
          :key="level"
          class="filter-btn"
          :class="{ active: selectedLevel === level }"
          @click="$emit('filter-change', level)"
        >
          {{ level }}
        </button>
      </div>
    </div>
    <div class="results-count">
      {{ visibleCount }} course{{ visibleCount !== 1 ? "s" : "" }} available
    </div>
  </div>
</template>

<script setup>
const skillLevels = ["All", "Beginner", "Intermediate", "Advanced"];

defineProps({
  selectedLevel: {
    type: String,
    default: "All",
  },
  visibleCount: {
    type: Number,
    required: true,
  },
});

defineEmits(["filter-change"]);
</script>

<style scoped>
.filter-bar {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.filter-group {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.filter-label {
  font-weight: 600;
  color: #555;
  font-size: 0.95rem;
}

.filter-buttons {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.5rem 1rem;
  border: 1.5px solid #ddd;
  background: white;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: 500;
  color: #555;
  cursor: pointer;
  transition: all 0.2s ease;
}

.filter-btn:hover {
  border-color: #e67e22;
  color: #e67e22;
}

.filter-btn.active {
  background: #e67e22;
  border-color: #e67e22;
  color: white;
}

.results-count {
  font-size: 0.9rem;
  color: #888;
  font-weight: 500;
}

@media (max-width: 600px) {
  .filter-bar {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
