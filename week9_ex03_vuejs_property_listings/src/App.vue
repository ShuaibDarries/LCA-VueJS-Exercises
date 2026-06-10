<template>
  <div class="app">
    <AppHeader :active-count="activeCount" :total-count="totalCount" />

    <div class="controls">
      <SearchBar v-model="searchQuery" />
      <SortToggle v-model="sortOrder" />
    </div>

    <PropertyList
      :properties="filteredProperties"
      :bookmarked-ids="bookmarkedIds"
      @toggle-bookmark="toggleBookmark"
    />
  </div>
</template>

<script>
import { properties } from './data/properties.js'
import AppHeader from './components/AppHeader.vue'
import SearchBar from './components/SearchBar.vue'
import SortToggle from './components/SortToggle.vue'
import PropertyList from './components/PropertyList.vue'

export default {
  name: 'App',
  components: {
    AppHeader,
    SearchBar,
    SortToggle,
    PropertyList
  },
  data() {
    return {
      allProperties: properties,
      searchQuery: '',
      sortOrder: 'default',
      bookmarkedIds: []
    }
  },
  computed: {
    filteredProperties() {
      let result = [...this.allProperties]

      // Search filter
      const query = this.searchQuery.toLowerCase().trim()
      if (query) {
        result = result.filter(
          p =>
            p.title.toLowerCase().includes(query) ||
            p.location.toLowerCase().includes(query)
        )
      }

      // Sort
      if (this.sortOrder === 'low-to-high') {
        result.sort((a, b) => a.price - b.price)
      } else if (this.sortOrder === 'high-to-low') {
        result.sort((a, b) => b.price - a.price)
      }

      return result
    },
    activeCount() {
      return this.allProperties.filter(p => p.available).length
    },
    totalCount() {
      return this.allProperties.length
    }
  },
  methods: {
    toggleBookmark(id) {
      const index = this.bookmarkedIds.indexOf(id)
      if (index > -1) {
        this.bookmarkedIds.splice(index, 1)
      } else {
        this.bookmarkedIds.push(id)
      }
      this.saveBookmarks()
    },
    saveBookmarks() {
      localStorage.setItem('hb_bookmarks', JSON.stringify(this.bookmarkedIds))
    },
    loadBookmarks() {
      const saved = localStorage.getItem('hb_bookmarks')
      if (saved) {
        try {
          this.bookmarkedIds = JSON.parse(saved)
        } catch (e) {
          this.bookmarkedIds = []
        }
      }
    }
  },
  mounted() {
    this.loadBookmarks()
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: #f5f7fa;
  color: #333;
}

.app {
  min-height: 100vh;
  padding-bottom: 3rem;
}

.controls {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1.5rem 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
}

@media (max-width: 600px) {
  .controls {
    flex-direction: column;
    align-items: stretch;
  }
}
</style>
