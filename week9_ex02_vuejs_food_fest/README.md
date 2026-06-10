# Cape Town Food Fest — Vue.js Landing Page

A modern, responsive Vue 3 single-page landing page showcasing ticket tiers for the Cape Town Food Fest.

## Project Overview

This project displays three ticket tiers (Bronze, Silver, Gold) as reusable card components. The **Silver** tier is highlighted as the featured option. Users can "favourite" any tier via a heart toggle to simulate e-commerce engagement.

## Tech Stack

- Vue 3 (Composition API + `<script setup>`)
- Vite
- No external plugins or router

## Installation & Run Instructions

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Run the development server:**
   ```bash
   npm run dev
   ```

3. **Build for production:**
   ```bash
   npm run build
   ```

## Project Structure

```
week9_ex02_vuejs_food_fest/
├── index.html
├── package.json
├── vite.config.js
├── .gitignore
├── README.md
└── src/
    ├── main.js
    ├── App.vue
    ├── components/
    │   └── TicketCard.vue
    └── data/
        └── tickets.js
```

## Key Features

- **Reusable TicketCard component** — renders dynamically from data using props
- **Featured tier styling** — Silver tier is visually highlighted with a gold border, gradient background, and "Featured" badge
- **Favourite toggle** — click the heart icon (🤍 → ❤️) on any card
- **Responsive grid** — adapts from 3 columns on desktop to 1 column on mobile
- **Slots** — the CTA button area uses a slot for flexible layout
- **Computed property** — `favouriteCount` placeholder demonstrates computed usage
- **No hard-coded duplicate HTML** — all tiers rendered via `v-for`

## Screenshot

Open `http://localhost:5173` after running `npm run dev` to view the interface.

## GitHub Submission

Branch: `week9-vuejs-ex-02`

```bash
git checkout -b week9-vuejs-ex-02
git add .
git commit -m "Add week9 ex02 food fest landing"
git push origin week9-vuejs-ex-02
```
