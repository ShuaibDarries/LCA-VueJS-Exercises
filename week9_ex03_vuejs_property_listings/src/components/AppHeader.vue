<template>
  <header class="app-header">
    <div class="header-content">
      <h1 class="brand">Homes & Beyond</h1>
      <p class="tagline">Find your perfect stay in Cape Town</p>
      <div class="stats">
        <span class="stat-badge">
          {{ activeCount }} Active Listing{{ activeCount !== 1 ? 's' : '' }}
        </span>
        <span class="stat-badge total">
          {{ totalCount }} Total Property{{ totalCount !== 1 ? 's' : '' }}
        </span>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    activeCount: {
      type: Number,
      required: true
    },
    totalCount: {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
.app-header {
  background: linear-gradient(135deg, #1a5f7a 0%, #159895 100%);
  color: white;
  padding: 2rem 1rem;
  text-align: center;
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
}

.brand {
  font-size: 2.5rem;
  font-weight: 700;
  margin: 0;
  letter-spacing: -0.5px;
}

.tagline {
  font-size: 1.1rem;
  margin: 0.5rem 0 1.5rem;
  opacity: 0.9;
}

.stats {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.stat-badge {
  background: rgba(255, 255, 255, 0.2);
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 500;
}

.stat-badge.total {
  background: rgba(255, 255, 255, 0.35);
}
</style>
