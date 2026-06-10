<template>
  <div class="sort-toggle">
    <label class="sort-label">Sort by Price:</label>
    <select
      :value="modelValue"
      @change="$emit('update:modelValue', $event.target.value)"
      class="sort-select"
    >
      <option value="default">Default</option>
      <option value="low-to-high">Low to High</option>
      <option value="high-to-low">High to Low</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'SortToggle',
  props: {
    modelValue: {
      type: String,
      default: 'default'
    }
  },
  emits: ['update:modelValue']
}
</script>

<style scoped>
.sort-toggle {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.sort-label {
  font-weight: 500;
  color: #555;
  font-size: 0.95rem;
}

.sort-select {
  padding: 0.75rem 1rem;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  font-size: 0.95rem;
  background: white;
  cursor: pointer;
  outline: none;
  transition: border-color 0.2s;
}

.sort-select:focus {
  border-color: #159895;
}
</style>
