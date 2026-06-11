<template>
  <div class="class-card">
    <div class="card-header">
      <h3>{{ classItem.name }}</h3>
      <button
        class="delete-btn"
        @click="$emit('delete-class')"
        title="Delete session"
      >
        &times;
      </button>
    </div>

    <div class="card-body">
      <div class="detail-row">
        <span class="detail-icon">👤</span>
        <span class="detail-label">Coach:</span>
        <span class="detail-value">{{ classItem.coach }}</span>
      </div>

      <div class="detail-row">
        <span class="detail-icon">📅</span>
        <span class="detail-label">Date:</span>
        <span class="detail-value">{{ formatDate(classItem.date) }}</span>
      </div>

      <div class="detail-row">
        <span class="detail-icon">🕐</span>
        <span class="detail-label">Time:</span>
        <span class="detail-value">{{ classItem.time }}</span>
      </div>

      <div class="detail-row">
        <span class="detail-icon">👥</span>
        <span class="detail-label">Capacity:</span>
        <span class="detail-value">{{ classItem.capacity }} spots</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ClassCard',
  props: {
    classItem: {
      type: Object,
      required: true
    }
  },
  emits: ['delete-class'],
  setup() {
    // Helper to format date nicely
    const formatDate = (dateStr) => {
      const date = new Date(dateStr + 'T00:00:00')
      return date.toLocaleDateString('en-US', {
        weekday: 'short',
        year: 'numeric',
        month: 'short',
        day: 'numeric'
      })
    }

    return {
      formatDate
    }
  }
}
</script>

<style scoped>
.class-card {
  background: #fafbfc;
  border: 1px solid #e8e8e8;
  border-radius: 10px;
  padding: 18px;
  transition: box-shadow 0.3s, transform 0.2s;
}

.class-card:hover {
  box-shadow: 0 4px 16px rgba(0,0,0,0.1);
  transform: translateY(-2px);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 14px;
  padding-bottom: 12px;
  border-bottom: 1px solid #eee;
}

.card-header h3 {
  font-size: 1.1rem;
  color: #333;
  font-weight: 600;
}

.delete-btn {
  background: #ff6b6b;
  color: white;
  border: none;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  font-size: 1.3rem;
  line-height: 1;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.2s, transform 0.2s;
}

.delete-btn:hover {
  background: #ee5a5a;
  transform: scale(1.1);
}

.card-body {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.detail-row {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 0.95rem;
}

.detail-icon {
  font-size: 1rem;
}

.detail-label {
  color: #888;
  font-weight: 500;
}

.detail-value {
  color: #333;
  font-weight: 500;
}
</style>
