# Macro Tracker v2

A mobile-first macro tracking app built as a single HTML file. Zero dependencies, no frameworks, no build tools — just open `food_tracker.html` in your browser.

Built as a free Lifesum replacement for tracking macros across two people (Chris & Erica) during a 12-week cut.

## Features

### Dual Profile Support
- **Chris (Male)** and **Erica (Female)** profiles with separate daily logs
- 7 custom day types per person, one for each day of the week (e.g., `mon-run (med carb)`, `fri-legs (high carb)`)
- Auto day-type selection — the app automatically picks the right plan based on the current day of the week

### Food Tracking
- **4 meal slots**: Breakfast, Lunch, Dinner, Snack
- **Macro dashboard** with colored progress bars for calories, protein, carbs, and fat
- **Remaining macro countdown** — shows how many grams/calories left for each macro as you log food
- **Tap to edit** — tap any food item in a meal to adjust serving size after adding it

### Barcode Scanner
- Scan food barcodes using your phone camera (uses `html5-qrcode` library)
- Looks up nutrition data from **OpenFoodFacts API** (free, no account needed)
- After scanning, choose amount in **grams, ounces, or servings** with live macro preview
- Pick which meal to add it to with one tap

### Food Database
- ~30 seed foods pre-loaded (chicken, rice, egg whites, yogurt, vegetables, fruits, etc.)
- **Quick create** — add a new food inline when adding to a meal (name, serving, calories, protein, carbs, fat)
- **USDA FoodData Central** search to find and import foods
- Foods sorted by usage frequency for fast access

### Smart Meal Suggestions
- Tap the lightning bolt on any meal for a realistic meal suggestion
- **17 meal templates** organized by meal type:
  - Breakfast: Egg White Scramble, Yogurt Bowl, Protein Shake, Eggs & Toast, etc.
  - Lunch: Chicken & Rice Bowl, Protein Salad, Turkey & Quinoa Plate
  - Dinner: Grilled Protein & Sides, Salmon Dinner, Stir-Fry Style, etc.
  - Snack: Yogurt & Fruit, Protein Shake, Nuts & Fruit, Apple & PB
- Scales servings to fit your remaining macro budget for the day
- Hit "Regenerate" for a different suggestion

### Serving Size Flexibility
- Everywhere you add or edit food: **grams / ounces / servings** toggle
- Live macro preview updates as you change the amount
- Works in barcode scanner, add-food modal, and edit-meal-item modal

### History & Export
- View past days with full meal breakdowns
- CSV export per day
- JSON export/import for full data backup

### Settings
- Dark/Light theme toggle
- Edit profiles and day types with custom macro targets
- USDA API key configuration

## Tech Stack

- **Single HTML file** (~2500 lines) — all HTML, CSS, and JS inline
- **Zero dependencies** at runtime (only CDN: `html5-qrcode` for barcode scanning)
- **localStorage** for all data persistence
- **Vanilla JS** with event delegation via `data-action` attributes
- **CSS custom properties** for dark/light theming
- **Mobile-first** responsive design

## How to Use

### On Desktop
Just open `food_tracker.html` in Chrome or Edge.

### On Phone (same Wi-Fi network)
1. From your computer, run:
   ```
   npx http-server ./ -p 8080 -S -C cert.pem -K key.pem --cors -c-1
   ```
2. Find your computer's local IP (e.g., `192.168.0.7`)
3. On your phone, open: `https://192.168.0.7:8080/food_tracker.html`
4. Accept the self-signed certificate warning
5. Barcode scanning requires HTTPS, which is why the SSL cert is included

## Data Storage

All data lives in localStorage under these keys:
| Key | Contents |
|-----|----------|
| `mpt_profiles` | Profile names and day type definitions with macro targets |
| `mpt_foods` | Custom food database (name, serving, macros, barcode, category) |
| `mpt_logs` | Daily logs keyed by date, each containing meals for both profiles |
| `mpt_settings` | Theme preference, USDA API key |

## Files

| File | Purpose |
|------|---------|
| `food_tracker.html` | The entire app |
| `cert.pem` | Self-signed SSL certificate for local HTTPS server |
| `key.pem` | Private key for the SSL certificate |
| `data/foods.csv` | Original food data (reference only, seed data is in the HTML) |
| `README.md` | This file |

## Chris's Macro Targets (12-Week Cut)

| Day | Calories | Protein | Carbs | Fat |
|-----|----------|---------|-------|-----|
| Mon - Run (Med Carb) | 1950 | 200g | 190g | 45g |
| Tue - Back/Bis (Med Carb) | 1950 | 200g | 180g | 45g |
| Wed - Chest/Sh/Tri (Med Carb) | 1950 | 200g | 180g | 45g |
| Thu - HIIT (Low Carb) | 1725 | 200g | 110g | 58g |
| Fri - Legs (High Carb) | 2350 | 200g | 325g | 38g |
| Sat - Full Body (Med Carb) | 1950 | 200g | 190g | 45g |
| Sun - Rest (Low Carb) | 1725 | 200g | 100g | 58g |

## Erica's Macro Targets (12-Week Fasted Training Cut)

| Day | Calories | Protein | Carbs | Fat |
|-----|----------|---------|-------|-----|
| Mon - Run (Med Carb) | 1675 | 145g | 170g | 40g |
| Tue - Back/Bis (Med Carb) | 1675 | 145g | 160g | 40g |
| Wed - Chest/Sh/Tri (Med Carb) | 1675 | 145g | 160g | 40g |
| Thu - HIIT (Low-Mod Carb) | 1475 | 145g | 110g | 48g |
| Fri - Legs (High Carb) | 2000 | 145g | 263g | 38g |
| Sat - Full Body (Med Carb) | 1675 | 145g | 170g | 40g |
| Sun - Rest (Low Carb) | 1475 | 145g | 83g | 48g |
