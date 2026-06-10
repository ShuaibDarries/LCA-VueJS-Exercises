<template>
  <div class="property-card" :class="{ 'not-available': !property.available }">
    <div class="card-image-wrapper">
      <img :src="property.image" :alt="property.title" class="card-image" />
      <div v-if="!property.available" class="ribbon">Not Available</div>
      <button
        class="bookmark-btn"
        :class="{ bookmarked: isBookmarked }"
        @click="toggleBookmark"
        :title="isBookmarked ? 'Remove bookmark' : 'Add bookmark'"
      >
        {{ isBookmarked ? '&#9733;' : '&#9734;' }}
      </button>
    </div>
    <div class="card-body">
      <div class="card-header">
        <h3 class="card-title">{{ property.title }}</h3>
        <span class="property-type">{{ property.type }}</span>
      </div>
      <p class="card-location">&#128205; {{ property.location }}</p>
      <div class="card-footer">
        <span class="card-price">R {{ property.price.toLocaleString() }} <small>/ night</small></span>
        <span
          class="availability-badge"
          :class="property.available ? 'available' : 'unavailable'"
        >
          {{ property.available ? 'Available' : 'Unavailable' }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PropertyCard',
  props: {
    property: {
      type: Object,
      required: true
    },
    isBookmarked: {
      type: Boolean,
      default: false
    }
  },
  emits: ['toggle-bookmark'],
  methods: {
    toggleBookmark() {
      this.$emit('toggle-bookmark', this.property.id)
    }
  }
}
</script>

<style scoped>
.property-card {
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  position: relative;
}

.property-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}

.property-card.not-available {
  opacity: 0.75;
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
  transition: transform 0.3s ease;
}

.property-card:hover .card-image {
  transform: scale(1.05);
}

.ribbon {
  position: absolute;
  top: 12px;
  left: -30px;
  background: #e74c3c;
  color: white;
  padding: 0.35rem 2.5rem;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  transform: rotate(-45deg);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}

.bookmark-btn {
  position: absolute;
  top: 12px;
  right: 12px;
  background: white;
  border: none;
  border-radius: 50%;
  width: 38px;
  height: 38px;
  font-size: 1.3rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
  transition: background 0.2s, transform 0.2s;
  color: #bbb;
}

.bookmark-btn:hover {
  transform: scale(1.1);
}

.bookmark-btn.bookmarked {
  color: #f1c40f;
}

.card-body {
  padding: 1.25rem;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 0.5rem;
  margin-bottom: 0.5rem;
}

.card-title {
  font-size: 1.15rem;
  font-weight: 600;
  margin: 0;
  color: #222;
  line-height: 1.3;
}

.property-type {
  background: #eef7f7;
  color: #159895;
  padding: 0.25rem 0.6rem;
  border-radius: 6px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  white-space: nowrap;
}

.card-location {
  color: #777;
  font-size: 0.9rem;
  margin: 0 0 1rem;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.card-price {
  font-size: 1.1rem;
  font-weight: 700;
  color: #1a5f7a;
}

.card-price small {
  font-weight: 400;
  font-size: 0.8rem;
  color: #888;
}

.availability-badge {
  font-size: 0.75rem;
  font-weight: 600;
  padding: 0.3rem 0.7rem;
  border-radius: 20px;
  text-transform: uppercase;
}

.availability-badge.available {
  background: #d4edda;
  color: #155724;
}

.availability-badge.unavailable {
  background: #f8d7da;
  color: #721c24;
}
</style>
