# Homes & Beyond - Property Listings

A lightweight Vue 3 single-page application that displays curated property listings for a Cape Town short-term rental startup. Users can search, sort by price, and bookmark their favourite properties.

## Project Overview

This mini web app showcases property listings in a responsive, card-based layout. It simulates a real property-finder interface with smooth interactivity and clean presentation — all powered by local data, no backend required.

## Features

- **Dynamic Listings** — Properties rendered from a local data array
- **Search** — Filter listings by title or location in real time
- **Sort** — Toggle between low-to-high and high-to-low price ordering
- **Availability Badges** — Visual "Not Available" ribbon and status indicator
- **Bookmarks** — Star/unstar properties; favourites persist in `localStorage`
- **Responsive Grid** — Adapts from mobile to desktop seamlessly
- **Header Stats** — Shows total and active property counts dynamically

## Tech Stack

- Vue 3 (Composition API style with Options API)
- Vite
- No external libraries, router, or API calls

## Project Setup

```bash
# Install dependencies
npm install

# Start the development server
npm run dev

# Build for production
npm run build
```

## File Structure

```
week9_ex03_vuejs_property_listings/
├── index.html
├── package.json
├── vite.config.js
├── .gitignore
├── README.md
└── src/
    ├── main.js
    ├── App.vue
    ├── data/
    │   └── properties.js
    └── components/
        ├── AppHeader.vue
        ├── SearchBar.vue
        ├── SortToggle.vue
        ├── PropertyCard.vue
        └── PropertyList.vue
```

## Screenshot

*(Add a screenshot of your running app here before zipping)*

## Author

Built as part of the LCA Vue.js weekly exercises.
