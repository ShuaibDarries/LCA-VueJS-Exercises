<
<template>
  <div
    class="course-card"
    :class="{ 'sold-out': !course.available, saved: isSaved }"
  >
    <div class="card-image-wrapper">
      <img
        :src="course.image"
        :alt="course.title"
        class="card-image"
        loading="lazy"
      />
      <div v-if="!course.available" class="sold-out-overlay">
        <span class="sold-out-badge">Sold Out</span>
      </div>
      <div class="skill-badge" :class="skillClass">{{ course.skillLevel }}</div>
    </div>

    <div class="card-body">
      <h3 class="course-title">{{ course.title }}</h3>
      <p class="course-chef">👨‍🍳 {{ course.chef }}</p>
      <p class="course-description">{{ course.description }}</p>

      <div class="card-footer">
        <span class="course-price">{{ formattedPrice }}</span>
        <button
          class="wishlist-btn"
          :class="{ active: isSaved }"
          :disabled="!course.available"
          @click="toggleWishlist"
          :title="wishlistTitle"
        >
          <span class="heart-icon">{{ isSaved ? "❤️" : "🤍" }}</span>
          <span class="wishlist-text">{{ isSaved ? "Saved" : "Save" }}</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  course: {
    type: Object,
    required: true,
  },
  isSaved: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["toggle-wishlist"]);

const skillClass = computed(() => {
  const map = {
    Beginner: "beginner",
    Intermediate: "intermediate",
    Advanced: "advanced",
  };
  return map[props.course.skillLevel] || "beginner";
});

const formattedPrice = computed(() => {
  return new Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD",
  }).format(props.course.price);
});

const wishlistTitle = computed(() => {
  if (!props.course.available) return "Course is sold out";
  return props.isSaved ? "Remove from wishlist" : "Add to wishlist";
});

function toggleWishlist() {
  if (props.course.available) {
    emit("toggle-wishlist", props.course.id);
  }
}
</script>

<style scoped>
.course-card {
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
  display: flex;
  flex-direction: column;
  position: relative;
}

.course-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.15);
}

.course-card.sold-out {
  opacity: 0.75;
}

.course-card.saved {
  box-shadow: 0 4px 12px rgba(231, 76, 60, 0.15);
}

.card-image-wrapper {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.course-card:hover .card-image {
  transform: scale(1.05);
}

.sold-out-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.sold-out-badge {
  background: #e74c3c;
  color: white;
  font-weight: 700;
  font-size: 0.9rem;
  padding: 0.5rem 1.25rem;
  border-radius: 50px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.skill-badge {
  position: absolute;
  top: 12px;
  right: 12px;
  padding: 0.35rem 0.75rem;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.skill-badge.beginner {
  background: #27ae60;
  color: white;
}

.skill-badge.intermediate {
  background: #f39c12;
  color: white;
}

.skill-badge.advanced {
  background: #8e44ad;
  color: white;
}

.card-body {
  padding: 1.25rem;
  flex: 1;
  display: flex;
  flex-direction: column;
}

.course-title {
  font-size: 1.15rem;
  font-weight: 700;
  color: #1a1a2e;
  margin: 0 0 0.5rem 0;
  line-height: 1.3;
}

.course-chef {
  font-size: 0.9rem;
  color: #666;
  margin: 0 0 0.75rem 0;
}

.course-description {
  font-size: 0.9rem;
  color: #777;
  line-height: 1.5;
  margin: 0 0 1rem 0;
  flex: 1;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
  padding-top: 0.75rem;
  border-top: 1px solid #f0f0f0;
}

.course-price {
  font-size: 1.25rem;
  font-weight: 700;
  color: #e67e22;
}

.wishlist-btn {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.5rem 1rem;
  border: 1.5px solid #ddd;
  background: white;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: 600;
  color: #666;
  cursor: pointer;
  transition: all 0.2s ease;
}

.wishlist-btn:hover:not(:disabled) {
  border-color: #e74c3c;
  color: #e74c3c;
  background: #fdf2f2;
}

.wishlist-btn.active {
  border-color: #e74c3c;
  background: #fdf2f2;
  color: #e74c3c;
}

.wishlist-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.heart-icon {
  font-size: 1rem;
  transition: transform 0.2s ease;
}

.wishlist-btn:hover:not(:disabled) .heart-icon {
  transform: scale(1.2);
}

@media (max-width: 600px) {
  .card-image-wrapper {
    height: 180px;
  }
  .course-title {
    font-size: 1rem;
  }
}
</style>
