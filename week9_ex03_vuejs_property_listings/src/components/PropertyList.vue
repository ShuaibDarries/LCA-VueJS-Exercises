<template>
  <div class="property-list">
    <div v-if="properties.length > 0" class="grid">
      <PropertyCard
        v-for="property in properties"
        :key="property.id"
        :property="property"
        :is-bookmarked="bookmarkedIds.includes(property.id)"
        @toggle-bookmark="$emit('toggle-bookmark', $event)"
      />
    </div>
    <div v-else class="empty-state">
      <p class="empty-icon">&#128269;</p>
      <h3>No properties found</h3>
      <p>Try adjusting your search or sort criteria.</p>
    </div>
  </div>
</template>

<script>
import PropertyCard from './PropertyCard.vue'

export default {
  name: 'PropertyList',
  components: {
    PropertyCard
  },
  props: {
    properties: {
      type: Array,
      required: true
    },
    bookmarkedIds: {
      type: Array,
      default: () => []
    }
  },
  emits: ['toggle-bookmark']
}
</script>

<style scoped>
.property-list {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

.empty-state {
  text-align: center;
  padding: 4rem 1rem;
  color: #888;
}

.empty-icon {
  font-size: 3rem;
  margin: 0 0 1rem;
}

.empty-state h3 {
  color: #555;
  margin: 0 0 0.5rem;
}

.empty-state p {
  margin: 0;
}
</style>
