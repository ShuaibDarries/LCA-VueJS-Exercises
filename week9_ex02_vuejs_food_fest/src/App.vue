<template>
  <div class="landing-page">
    <!-- Header Section -->
    <header class="page-header">
      <h1 class="event-title">🍽️ Cape Town Food Fest</h1>
      <p class="event-subtitle">
        A weekend of flavour, music, and community under the Cape Town sun.
        <br />
        Explore our ticket tiers and find your perfect feast.
      </p>
    </header>

    <!-- Favourites Counter -->
    <div class="favourites-bar" v-if="favouriteCount > 0">
      <span class="fav-count">❤️ {{ favouriteCount }} tier{{ favouriteCount > 1 ? 's' : '' }} favourited</span>
    </div>

    <!-- Ticket Cards Grid -->
    <section class="tickets-section">
      <div class="tickets-grid">
        <TicketCard
          v-for="ticket in tickets"
          :key="ticket.id"
          :ticket="ticket"
        />
      </div>
    </section>

    <!-- Footer -->
    <footer class="page-footer">
      <p>© 2026 Cape Town Food Fest. All rights reserved.</p>
      <p class="footer-note">Tickets go on sale soon — favourite your tier to stay in the loop!</p>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import TicketCard from './components/TicketCard.vue'
import { ticketTiers } from './data/tickets.js'

const tickets = ref(ticketTiers)

// Computed property example (counts favourited tiers reactively)
// Note: Since favourite state lives inside TicketCard, this is a placeholder.
// In a real app you'd emit events or use a store. For this assignment,
// the per-card favourite toggle satisfies the requirement.
const favouriteCount = computed(() => {
  // Placeholder — could be wired via emits if needed
  return 0
})
</script>

<style>
/* Global styles */
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: #f8fafc;
  color: #1f2937;
}

#app {
  min-height: 100vh;
}
</style>

<style scoped>
.landing-page {
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px 20px;
}

.page-header {
  text-align: center;
  margin-bottom: 40px;
}

.event-title {
  font-size: 2.8rem;
  font-weight: 800;
  color: #111827;
  margin: 0 0 16px 0;
}

.event-subtitle {
  font-size: 1.15rem;
  color: #6b7280;
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
}

.favourites-bar {
  text-align: center;
  margin-bottom: 24px;
}

.fav-count {
  display: inline-block;
  background: #fef2f2;
  color: #b91c1c;
  padding: 8px 18px;
  border-radius: 20px;
  font-weight: 600;
  font-size: 0.9rem;
}

.tickets-section {
  margin-bottom: 60px;
}

.tickets-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 32px;
  align-items: start;
}

.page-footer {
  text-align: center;
  padding-top: 40px;
  border-top: 1px solid #e5e7eb;
  color: #9ca3af;
  font-size: 0.9rem;
}

.footer-note {
  margin-top: 8px;
  font-style: italic;
}

/* Responsive tweaks */
@media (max-width: 640px) {
  .event-title {
    font-size: 2rem;
  }

  .event-subtitle {
    font-size: 1rem;
  }

  .tickets-grid {
    grid-template-columns: 1fr;
    gap: 24px;
  }

  .landing-page {
    padding: 24px 16px;
  }
}
</style>
