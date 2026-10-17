# Recipe project

This repo is a meal-prep **ingredient log**, not a cookbook. Do not write cooking instructions, stories, or prose recipes unless the user asks.

## Layout

- Folders: `breakfast/`, `lunch/`, `dinner/`
- One Markdown file per meal, named after the food (e.g. `breakfast/steak and eggs.md`)
- Create the meal folder if it is missing

## File format

Each recipe is only a Markdown table with these columns:

| Item / Ingredient | Weight 1 Serving | Weight 7 Days | Calories 1 Serving | Calories 7 Days | Protein 1 Serving | Protein 7 Days |
|---|---|---|---|---|---|---|

- Last row is `Combined Meal Total`
- 7-day values are 1 serving × 7
- Weights are raw / as-purchased unless the ingredient name says otherwise
- Only list ingredients that are eaten; cooking fat counts if used
- Calories and protein from USDA or the product label; round like `130 kcal`, `19.0g`
- Do not include carbs or fat columns

## Weight units

Put the unit on each cell, not in the column header. Use **oz** for large/heavy items (beef, chicken, potatoes, egg whites, milk, bagels, fruit portions). Use **g** for small or precise amounts (sugar, spices, oil, extracts, powders). Convert protein from grams using 1 oz = 28.35g.

## Targets

Honor calorie/protein constraints in the request (example: breakfast under 400 kcal and ~60g protein). If a constraint cannot be hit with the named foods, say so and show the closest table.

## Example

| Item / Ingredient | Weight 1 Serving | Weight 7 Days | Calories 1 Serving | Calories 7 Days | Protein 1 Serving | Protein 7 Days |
|---|---|---|---|---|---|---|
| Hero Plain Bagel (1 bagel) | 2.6 oz | 18.5 oz | 130 kcal | 910 kcal | 19.0g | 133.0g |
| Sugar | 5g | 35g | 19 kcal | 133 kcal | 0.0g | 0.0g |
