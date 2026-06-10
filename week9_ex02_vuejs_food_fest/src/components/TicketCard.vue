<template>
  <div class="ticket-card" :class="{ 'featured': ticket.featured, 'favourited': isFavourited }">
    <div class="card-header">
      <h3 class="tier-name">{{ ticket.name }}</h3>
      <button
        class="favourite-btn"
        @click="toggleFavourite"
        :aria-label="isFavourited ? 'Remove from favourites' : 'Add to favourites'"
      >
        <span class="heart">{{ isFavourited ? '❤️' : '🤍' }}</span>
      </button>
      <span v-if="ticket.featured" class="featured-badge">⭐ Featured</span>
    </div>

    <div class="price-block">
      <span class="currency">R</span>
      <span class="price">{{ ticket.price }}</span>
    </div>

    <p class="description">{{ ticket.description }}</p>

    <ul class="benefits-list">
      <li v-for="(benefit, index) in ticket.benefits" :key="index">
        ✅ {{ benefit }}
      </li>
    </ul>

    <div class="card-footer">
      <slot name="action" :tier="ticket">
        <button class="cta-btn" :class="{ 'featured-btn': ticket.featured }">
          {{ ticket.featured ? 'Get This Tier' : 'Select' }}
        </button>
      </slot>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  ticket: {
    type: Object,
    required: true
  }
})

const isFavourited = ref(false)

const toggleFavourite = () => {
  isFavourited.value = !isFavourited.value
}
</script>

<style scoped>
.ticket-card {
  background: #ffffff;
  border-radius: 16px;
  padding: 28px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  position: relative;
  display: flex;
  flex-direction: column;
  border: 2px solid transparent;
}

.ticket-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.12);
}

.ticket-card.featured {
  border-color: #f59e0b;
  background: linear-gradient(180deg, #fffbeb 0%, #ffffff 100%);
  box-shadow: 0 8px 28px rgba(245, 158, 11, 0.18);
}

.ticket-card.favourited {
  border-color: #ef4444;
}

.card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 16px;
  position: relative;
}

.tier-name {
  font-size: 1.5rem;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.favourite-btn {
  background: none;
  border: none;
  font-size: 1.4rem;
  cursor: pointer;
  padding: 4px;
  line-height: 1;
  transition: transform 0.2s ease;
}

.favourite-btn:hover {
  transform: scale(1.2);
}

.featured-badge {
  position: absolute;
  top: -44px;
  left: 50%;
  transform: translateX(-50%);
  background: #f59e0b;
  color: #fff;
  font-size: 0.75rem;
  font-weight: 700;
  padding: 6px 14px;
  border-radius: 20px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.price-block {
  margin-bottom: 12px;
}

.currency {
  font-size: 1.25rem;
  font-weight: 600;
  color: #4b5563;
  vertical-align: top;
}

.price {
  font-size: 2.8rem;
  font-weight: 800;
  color: #111827;
  line-height: 1;
}

.description {
  color: #6b7280;
  font-size: 0.95rem;
  margin-bottom: 20px;
  line-height: 1.5;
}

.benefits-list {
  list-style: none;
  padding: 0;
  margin: 0 0 24px 0;
  flex-grow: 1;
}

.benefits-list li {
  padding: 8px 0;
  font-size: 0.9rem;
  color: #374151;
  border-bottom: 1px solid #f3f4f6;
}

.benefits-list li:last-child {
  border-bottom: none;
}

.card-footer {
  margin-top: auto;
}

.cta-btn {
  width: 100%;
  padding: 14px;
  border-radius: 10px;
  border: 2px solid #e5e7eb;
  background: #ffffff;
  color: #374151;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.cta-btn:hover {
  background: #f9fafb;
  border-color: #d1d5db;
}

.cta-btn.featured-btn {
  background: #f59e0b;
  border-color: #f59e0b;
  color: #ffffff;
}

.cta-btn.featured-btn:hover {
  background: #d97706;
  border-color: #d97706;
}
</style>
