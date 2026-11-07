---
name: meal-prep-adaptation
description: Adapt recipes into this repo's calorie- and protein-targeted meal-prep ingredient logs. Use whenever a user provides a recipe URL, recipe ingredients, or asks to scale/adapt a breakfast, lunch, or dinner for their meal plan. Preserve the recipe's character, use the user's fixed portions and substitutions, calculate nutrition from product labels or USDA data, and write the repo's seven-day ingredient table.
---

# Meal prep recipe adaptation

Turn the provided recipe into a practical lower-calorie meal while keeping its recognizable ingredients and flavor. The goal is not to produce cooking instructions or arbitrarily shrink ingredients. Do the serving math first, make the smallest justified substitutions, calculate the nutrition, and then write the ingredient log.

## Project format and targets

Follow the repository `AGENTS.md` rules:

- Create one file in `breakfast/`, `lunch/`, or `dinner/`, named after the meal.
- The file contains only the standard ingredient table. Its columns are `Item / Ingredient`, `Weight 1 Serving`, `Weight 7 Days`, `Calories 1 Serving`, `Calories 7 Days`, `Protein 1 Serving`, and `Protein 7 Days`.
- End with `Combined Meal Total`. Seven-day quantities and nutrients are exactly the per-serving values multiplied by seven.
- Use raw/as-purchased weights unless the name says otherwise. Put units in cells. Use oz for larger portions and g for small/precise weights; preserve volume measures (tsp, tbsp, cups) where the recipe measures by volume.
- Include only ingredients that are eaten. Do not add cooking directions, prose, carbs, or fat columns.
- Link the recipe source and nutrition references in ingredient names where useful.

Targets:

- Breakfast: **under 400 kcal per serving**.
- Lunch and dinner: **under 700 kcal per serving**.
- Aim for **at least 60 g protein per meal** when feasible. Respect any different target the user gives.
- If the named foods and fixed portions cannot meet a target, do not pretend they can. Show the closest honest calculation and clearly explain what constraint prevents the target.

## User's standing food choices

Apply these defaults unless the user says otherwise:

- **Pasta/spaghetti:** replace with the user's designated pasta. Count **4 oz dry as 220 kcal and 14 g protein** per serving. Do not use the original recipe's pasta nutrition. If the user specifies another quantity or label, follow that.
- **Chicken:** prefer boneless, skinless chicken thighs over breast. The user's Amazon thigh label is **130 kcal per 4 oz**; use **260 kcal per 8 oz**. For protein, use the user's supplied label value (the working value given was **44 g per 8 oz**). Chicken breast is not the default; use it only when explicitly requested.
- Treat 8 oz chicken thighs as the usual per-meal amount when adapting a chicken meal, unless the user gives a different amount.
- Preserve explicitly requested ingredients, quantities, brands, and label data over these defaults.

## Workflow

### 1. Read the recipe and identify its yield

Open the source recipe and extract its ingredient amounts and stated yield. Distinguish recipe batch amounts from per-serving amounts. Record which items are measured by volume, weight, count, or label serving.

Do not assume the website's default serving size is the user's meal portion. Follow the user's serving instructions exactly:

- If they ask to scale a recipe from (for example) four servings to three, scale the recipe batch by 3/4 first.
- If they then explicitly say the resulting three-serving ingredient list is what they consider **one serving for them**, use those scaled amounts as their per-meal basis. Do not divide by three again. This correction matters: a scaled recipe can be one unusually large personal meal.
- If they say to use a scaled recipe's amounts for the other ingredients while changing the meat or pasta to their fixed portions, keep those provided amounts as the reference and make only the requested fixed-portion substitutions. Don't silently rescale every item a second time.
- If it remains unclear whether listed weights are a whole batch or one personal serving, ask before finalizing; the difference can radically change the calorie total.

When scaling ingredients, preserve ratios from the selected source version. If the user anchors a scaled recipe to a particular meat amount (e.g. the three-serving version lists 9 oz chicken, while their meal uses 8 oz), use that to understand their intended scale. Do not apply an additional global scale factor if the user has already told you to keep that version's other ingredient quantities.

### 2. Apply fixed portions and substitutions

Use the user's chosen meal portions first. Typical anchors are 4 oz dry of the user's designated pasta and 8 oz chicken thighs, but an explicit instruction for this recipe overrides them.

Make lower-calorie substitutions while retaining the ingredient's role and, where practical, its amount/volume:

- Replace sugar with the same volume of zero-calorie sweetener when requested or suitable. Verify the product is actually labeled zero-calorie; don't assume all substitutes are calorie-free.
- Replace oil with cooking spray when requested. Count spray calories based on the user's label/amount; spray is not automatically calorie-free. Do not include the removed oil.
- Prefer lower-fat yogurt or similar lower-calorie versions when relevant, keeping the recipe amount unless it would violate a user constraint.
- Prefer chicken thighs as above unless chicken breast is specifically requested.
- Keep original amounts of sauces, aromatics, and vegetables as close as practical. Don't cut ingredients arbitrarily to make the numbers look good.
- Remove ingredients only if the user says to omit them, says they do not have them, or they are not eaten. If the user limits vegetables to those on hand, list only those vegetables.
- If the user asks for separate cooking components (for example, chicken marinade and noodle sauce), list the same ingredient as separate rows labeled by its use. This makes the table actionable. Do not combine amounts into a single ambiguous row.
- Water that is only used for soaking, boiling, steaming, or a marinade and is not eaten need not be listed. Include it only if the user wants a complete recipe list or it remains in the meal.

### 3. Verify nutrition and calculate before writing

Use the exact product label supplied by the user when available. Otherwise use USDA FoodData Central or the actual manufacturer/product label. Search for a specific product when brand matters. Do not use unsourced guesses where a label or USDA value is available.

For each ingredient:

1. Convert the selected recipe amount to the user's one-serving amount, respecting the scaling rules above.
2. Convert units carefully (including raw vs cooked weights, dry vs prepared pasta, and volume-to-weight where nutrition data requires it).
3. Calculate calories and protein from the chosen label/USDA serving, then round reasonably for display.
4. Multiply displayed one-serving calories, protein, and amounts by seven for the seven-day columns. Ensure the totals equal the row sums and seven-day totals equal seven times the per-serving totals.

Check the fixed portions first. For example, the user's pasta (4 oz, 220 kcal) plus chicken thighs (8 oz, 260 kcal) already uses **480 kcal** of a lunch/dinner limit. Calculate the remaining sauces, vegetables, seasonings, and cooking fat rather than assuming they fit. Keep a realistic margin below the calorie ceiling when possible; a meal at 699 kcal is fragile to label rounding or an extra spray.

Protein is a target, not a reason to invent nutrition facts. If the fixed food portions provide less than 60 g protein, calculate the shortfall honestly and determine whether it can be solved within the calorie target using foods already in the recipe or a user-approved addition. Do not add ingredients without permission.

### 4. Save and report

Write only the table to the meal file. Check that:

- The last row is `Combined Meal Total`.
- There is one row per distinct ingredient/use where separation matters.
- Units are present in weight/amount cells and sensible for the size.
- Every seven-day number is exactly the displayed one-serving number times seven.
- Total calories and protein equal the ingredient rows.
- The recipe respects requested omissions and substitutions.

In the chat, summarize the file path, calories and protein per serving, and any constraint that could not be met. Be direct about uncertainty or label assumptions; don't call an estimate exact.
