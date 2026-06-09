<
<template>
  <div class="app">
    <AppHeader :wishlist-count="wishlist.length" />

    <main class="main-content">
      <div class="hero">
        <h2 class="hero-title">Explore Our Cooking Courses</h2>
        <p class="hero-subtitle">
          Learn from world-class chefs and elevate your culinary skills
        </p>
      </div>

      <CourseFilter
        :selected-level="selectedLevel"
        :visible-count="filteredCourses.length"
        @filter-change="selectedLevel = $event"
      />

      <div class="courses-grid">
        <CourseCard
          v-for="course in filteredCourses"
          :key="course.id"
          :course="course"
          :is-saved="wishlist.includes(course.id)"
          @toggle-wishlist="toggleWishlist"
        />
      </div>

      <div v-if="filteredCourses.length === 0" class="empty-state">
        <p class="empty-text">No courses match your filter.</p>
        <button class="clear-btn" @click="selectedLevel = 'All'">
          Show all courses
        </button>
      </div>
    </main>

    <footer class="app-footer">
      <p>© 2026 Cooking Masterclass. All rights reserved.</p>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { courses } from "./data/courses.js";
import AppHeader from "./components/AppHeader.vue";
import CourseCard from "./components/CourseCard.vue";
import CourseFilter from "./components/CourseFilter.vue";

const selectedLevel = ref("All");
const wishlist = ref([]);

const filteredCourses = computed(() => {
  if (selectedLevel.value === "All") {
    return courses;
  }
  return courses.filter((c) => c.skillLevel === selectedLevel.value);
});

function toggleWishlist(courseId) {
  const index = wishlist.value.indexOf(courseId);
  if (index > -1) {
    wishlist.value.splice(index, 1);
  } else {
    wishlist.value.push(courseId);
  }
}
</script>

<style scoped>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background: #f8f9fa;
}

.main-content {
  flex: 1;
  padding-bottom: 2rem;
}

.hero {
  text-align: center;
  padding: 3rem 1.5rem 1.5rem;
  max-width: 800px;
  margin: 0 auto;
}

.hero-title {
  font-size: 2rem;
  font-weight: 700;
  color: #1a1a2e;
  margin: 0 0 0.5rem 0;
}

.hero-subtitle {
  font-size: 1.1rem;
  color: #666;
  margin: 0;
}

.courses-grid {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1.5rem;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

.empty-state {
  text-align: center;
  padding: 3rem 1.5rem;
}

.empty-text {
  font-size: 1.1rem;
  color: #888;
  margin-bottom: 1rem;
}

.clear-btn {
  padding: 0.6rem 1.25rem;
  background: #e67e22;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s ease;
}

.clear-btn:hover {
  background: #d35400;
}

.app-footer {
  background: #1a1a2e;
  color: rgba(255, 255, 255, 0.6);
  text-align: center;
  padding: 1.5rem;
  font-size: 0.9rem;
}

@media (max-width: 600px) {
  .hero-title {
    font-size: 1.5rem;
  }
  .hero-subtitle {
    font-size: 1rem;
  }
  .courses-grid {
    grid-template-columns: 1fr;
    padding: 0 1rem;
  }
}
</style>
