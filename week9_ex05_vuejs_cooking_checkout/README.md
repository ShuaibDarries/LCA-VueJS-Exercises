# Cooking Masterclass Checkout Prototype

A Vue 3 single-page shopping cart prototype for the Cooking Masterclass brand. Users can browse culinary courses, add them to a cart, adjust quantities, and view a live price summary with tax and optional coupon discounts.

## Features

- Product catalogue with 8 cooking courses
- Add to cart with live updates
- Increase / decrease / remove individual cart items
- Line totals, subtotal, 15% tax, and grand total
- Sold-out courses clearly marked and disabled
- Coupon code support (`SAVE10` for 10% off, `WELCOME15` for 15% off)
- Clear Cart button
- Empty cart message
- Cart data persisted in `localStorage`
- Responsive two-column layout (stacked on mobile)

## Tech Stack

- Vue 3 (Composition API) + Vite
- No routing, no backend, no external packages beyond Vue
- Components, props, emits, computed properties, conditional rendering, `localStorage`

## Setup Instructions

1. Make sure you have [Node.js](https://nodejs.org/) installed.
2. Open a terminal in the project folder.
3. Install dependencies:
   ```bash
   npm install
   ```
4. Run the development server:
   ```bash
   npm run dev
   ```
5. Open the provided local URL in your browser (usually `http://localhost:5173/`).

## Scripts

- `npm run dev` — start the Vite dev server
- `npm run build` — build for production
- `npm run preview` — preview the production build

## Project Structure

```
week9_ex05_vuejs_cooking_checkout/
├── index.html
├── package.json
├── vite.config.js
├── .gitignore
├── README.md
└── src/
    ├── main.js
    ├── App.vue
    ├── style.css
    ├── data.js
    └── components/
        ├── CourseCatalogue.vue
        └── CartPanel.vue
```

## Git Submission

```bash
git checkout -b week9-vuejs-ex-05
git add .
git commit -m "Add week9 ex05 cooking checkout"
git push origin week9-vuejs-ex-05
```

Remember to exclude `node_modules` and `dist` from Git (they are already in `.gitignore`).

## Screenshot

*(Add a screenshot of the checkout interface here once the app is running.)*

---

Built for the Vue.js frontend coursework assignment.
