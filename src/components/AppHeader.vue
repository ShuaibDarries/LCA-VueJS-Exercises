<
<template>
  <header class="app-header">
    <div class="header-content">
      <div class="brand">
        <span class="brand-icon">👨‍🍳</span>
        <h1 class="brand-title">Cooking Masterclass</h1>
      </div>
      <div class="wishlist-badge" :class="{ 'has-items': wishlistCount > 0 }">
        <span class="wishlist-icon">❤️</span>
        <span class="wishlist-label">Wishlist</span>
        <span class="wishlist-count">{{ wishlistCount }}</span>
      </div>
    </div>
  </header>
</template>

<script setup>
defineProps({
  wishlistCount: {
    type: Number,
    required: true,
    default: 0,
  },
});
</script>

<style scoped>
.app-header {
  background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
  color: white;
  padding: 1rem 0;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.15);
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.brand {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.brand-icon {
  font-size: 1.75rem;
}

.brand-title {
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: -0.5px;
  margin: 0;
}

.wishlist-badge {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(255, 255, 255, 0.1);
  padding: 0.5rem 1rem;
  border-radius: 50px;
  transition: all 0.3s ease;
}

.wishlist-badge.has-items {
  background: rgba(231, 76, 60, 0.2);
  border: 1px solid rgba(231, 76, 60, 0.3);
}

.wishlist-icon {
  font-size: 1.1rem;
}

.wishlist-label {
  font-weight: 500;
  font-size: 0.95rem;
}

.wishlist-count {
  background: #e74c3c;
  color: white;
  font-size: 0.8rem;
  font-weight: 700;
  min-width: 24px;
  height: 24px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 6px;
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.wishlist-badge.has-items .wishlist-count {
  animation: popIn 0.3s ease;
}

@keyframes popIn {
  0% {
    transform: scale(0.5);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}

@media (max-width: 600px) {
  .brand-title {
    font-size: 1.1rem;
  }
  .wishlist-label {
    display: none;
  }
  .header-content {
    padding: 0 1rem;
  }
}
</style>
