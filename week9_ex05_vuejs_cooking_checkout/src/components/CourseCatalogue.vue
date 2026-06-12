<template>
  <div class="courses-section">
    <h2 class="section-title">Available Courses</h2>
    <div class="courses-grid">
      <div
        v-for="course in courses"
        :key="course.id"
        class="course-card"
        :class="{ 'sold-out': course.soldOut }"
      >
        <div class="course-image-wrap">
          <span>{{ course.emoji }}</span>
          <span v-if="course.soldOut" class="sold-out-badge">Sold Out</span>
        </div>
        <div class="course-body">
          <div class="course-name">{{ course.name }}</div>
          <div class="course-meta">
            {{ course.instructor }} &middot; {{ course.duration }}
          </div>
          <div class="course-price">R {{ course.price.toLocaleString('en-ZA') }}</div>
          <button
            class="btn btn-primary"
            :disabled="course.soldOut"
            @click="$emit('add-to-cart', course)"
          >
            {{ course.soldOut ? 'Sold Out' : 'Add to Cart' }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  courses: {
    type: Array,
    required: true,
  },
})

defineEmits(['add-to-cart'])
</script>
