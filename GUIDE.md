# Build guide: North-East Nigeria food prices (R data cleaning)

**Business question:** how much did staple food prices rise in North-East Nigeria after the naira float in June 2023, did they follow the currency, and where do they stand now?

**Result:** a Quarto report (`food_prices.html`), a clean reusable dataset (`data/clean/ne_retail_prices_clean.csv`) and three charts. Time: about two sessions.

---

## 1. Put the folder in place

Unzip `nigeria-food-prices` into your `Project Portfolio` folder.

## 2. Get the data (5 minutes)

1. Open <https://data.humdata.org/dataset/wfp-food-prices-for-nigeria>.
2. Under **Data and Resources**, download **wfp_food_prices_nga.csv** (about 11 MB).
3. Move it into the project's `data/raw` folder. Keep the name exactly `wfp_food_prices_nga.csv` (turn on file name extensions first).

Do not open or save it in Excel. The raw file stays out of GitHub (see `.gitignore`); anyone can download it from HDX.

WFP updates this file every month, and sometimes revises or removes older prices. The numbers below come from the file downloaded on 31 October 2026 (88,391 rows). The analysis stops at August 2026, the last complete month; a later download may differ slightly.

## 3. Open the project

Double-click `nigeria-food-prices.Rproj`, then open `food_prices.qmd` from the **Files** panel. No new packages are needed: everything comes with the tidyverse.

## 4. Run the chunks in order and check your numbers

| Chunk | Check | Expected |
| --- | --- | --- |
| `import` | HXL rows removed | 0 or 1 |
| `import` | Rows, columns, dates | 88,391, 16, 2002-01-15 to 2026-10-15 |
| `inspect` | Duplicates | 0 |
| `inspect` | Different units | 20 |
| `coverage` | States still monitored after January 2023 | Borno, Yobe, Adamawa only |
| `filter` | Records, markets, foods | 44,802, 52, 38 |
| `units` | Per kg / litre / piece | 38,705 / 4,213 / 1,884 |
| `outliers` | Outliers flagged | 152 (0.34%), most for fish, spinach and powdered milk |
| `save` | Rows saved | 44,802 |
| `index` | Base price per kg, Feb to May 2023 | Local rice 650.5, beans 406.8, maize flour 281.0, millet 258.1, sorghum 223.4 naira |
| `index` | Basket index: May 2023 / Sep 2024 / Jan 2026 / Aug 2026 | 111 / 394 / 144 / 214 |
| `index` | Naira index: Sep 2024 / Jan 2026 / Aug 2026 | 354 / 310 / 294 |
| `index` | Basket in dollar terms: Sep 2024 / Jan 2026 / Aug 2026 | 112 / 46 / 73 |

## 5. Write your reading

One place says **Your reading**. Replace the line with three or four sentences in your own words (no `>` at the start, no `_` at the end).

Points to think about:

- At the peak, did food prices rise more or less than the price of the dollar?
- What does a basket index of 145 in January 2026, when the naira index was 310, mean for someone who earns in naira? And for an aid agency that buys food with dollars?
- Which cleaning step would have changed the answer most if you had skipped it?

## 6. Render and publish

1. Click **Render**. It creates `food_prices.html`.
2. On GitHub, create a public repository `nigeria-food-prices` (README off). Description: *Cleaning WFP market price data in R: how staple food prices in North-East Nigeria moved after the 2023 naira float.*
3. Upload `food_prices.qmd`, `food_prices.html`, `README.md`, `GUIDE.md`, `nigeria-food-prices.Rproj`, and the `charts` and `data/clean` folders. Do not upload `data/raw` or `.Rproj.user`. Add `.gitignore` by hand.
4. Topics: `r`, `tidyverse`, `data-cleaning`, `data-wrangling`, `food-prices`, `nigeria`, `quarto`.
5. **Settings > Pages**: branch `main`, folder `/ (root)`, Save. The report will be at `https://ayanfedara.github.io/nigeria-food-prices/food_prices.html`.
