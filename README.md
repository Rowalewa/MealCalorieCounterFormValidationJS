# Meal Calorie Counter (Form Validation JS)

A browser-based calorie counter based on freeCodeCamp's "Build a Calorie Counter" project. Users set a daily calorie budget, log calories consumed across breakfast/lunch/dinner/snacks plus calories burned through exercise, and get a running surplus/deficit. It also includes a small kilocalorie → Calorie unit converter.

## Features

- **Daily calorie budget** input
- **Dynamic entry fields** — click "Add Entry" to add a new name/calorie input pair to Breakfast, Lunch, Dinner, Snacks, or Exercise
- **Calculate Remaining Calories** — sums all entries and reports a calorie surplus or deficit against the budget, accounting for calories burned through exercise
- **Input validation** — strips `+`, `-`, and whitespace from numeric input and rejects scientific-notation-style values (e.g. `1e3`) with an alert
- **Clear** button to reset the whole form
- **kCal → Cal converter** — a small standalone utility that converts a kilocalorie value to Calories (kCal ÷ 1000)

## Tech stack

Plain HTML, CSS, and vanilla JavaScript — no framework, build step, or dependencies.

## Running locally

No build step or server required — just open `index.html` directly in a browser:

```bash
open index.html   # macOS
# or
xdg-open index.html   # Linux
```

Or serve it locally if you prefer:

```bash
npx serve .
```

## Project structure

```
MealCalorieCounterFormValidationJS-main/
├── index.html
├── style.css
└── script.js
```

## How it works

- `addEntry()` inserts a new name/calorie input pair into the selected meal/exercise `<fieldset>`, numbered incrementally.
- `calculateCalories()` reads every numeric input across all fieldsets plus the budget, validates each value via `cleanInputString()` and `isInvalidInput()`, then computes `budget - (breakfast + lunch + dinner + snacks) + exercise` and renders it as a surplus or deficit.
- `convert_kcal_to_cal()` reads the kCal input, validates it the same way, and displays the Calorie equivalent.
- `clearForm()` empties all fieldsets and resets the budget and output.

## Known issue

`converter_output_cl` is looked up with `document.getElementById('.converter_output_cl')` — `getElementById` doesn't accept CSS selector syntax, and there's no element with that literal ID (with the leading dot) in the page, so this always resolves to `null`. In practice this means the red "please enter a value" error background/text-color styling in `convert_kcal_to_cal()` silently fails (it throws when `kCal === 0`, since it calls `.style` on `null`), even though the calorie counter's other validation works fine. Fixing it means either querying by the actual ID (`document.getElementById('convert_output')`, i.e. the same element as `convert_output`) or by class (`document.querySelector('.converter_output_cl')`) — depending on which selector was intended.

## License

Not specified.
