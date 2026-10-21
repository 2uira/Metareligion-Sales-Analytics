<!-- DRAFT — rewrite the prose in your own words before publishing. Structure matches your Instagram-engagement repo's README. Swap the image paths once you've exported chart PNGs from the notebook/dashboard, and update the Files links to your actual repo paths. Delete this comment before publishing. -->

# Metareligion Sales Analysis (Feb 2023 - Oct 2026)

Metareligion is an archive-fashion resale business I've run since February 2023, trading across Depop, Grailed, Vinted and private sales. This notebook cleans and analyses 111 sales I logged over that period, covering purchase cost, sale price, fees, shipping and realised profit per item.

**Questions**
1. Which channel actually protects margin once price tier is accounted for, and why?
2. Which categories and price tiers should Metareligion source more of, based on profit, margin and resale speed?

## Key findings

![Average margin % by platform](dashboard/platform_margin.png)

- **The Depop-Grailed margin gap is mostly a price-tier illusion.** Raw numbers put Grailed 5 points ahead on margin, but 71% of Grailed sales are over £200 versus only 16% of Depop's — it's not the same stock being compared. Once margin is compared within the same price band, the gap almost disappears (1-3 points in every tier).
- **Grailed's fees run roughly double Depop's, but its audience pays enough of a premium to absorb it.** Cost drag is consistently ~2x higher on Grailed at every price tier (e.g. 34.6% vs 17.8% under £100). Margins still come out roughly even, which means it's willingness to pay for archive pieces protecting margin, not the platform's fee structure.
- **Jacket and Jeans are the backbone of the business** — 68% of sales and roughly 86% of total profit, with solid margins (46-48%) and quick turnover (9-11 days).
- **The channel mix flipped in 2026.** Depop fell from 100% share in 2023-2024 to 26% by 2026, while Grailed rose to 48% — the same year the business hit its best-ever profit and margin (£3,281.5 profit, 51.4% average margin). Depop traffic has genuinely dried up and Vinted only works while physically in the UK, so this is as much "what's still available to me" as a deliberate platform choice.

![Total profit by category](dashboard/category_profit.png)

## Recommendations

- **Keep Jacket and Jeans as the core of sourcing** — the most proven part of the business by volume, profit and speed.
- **Lean further into Grailed for higher-value pieces** — not because its fee structure is better, but because its audience's willingness to pay absorbs the extra cost. Not the right channel for lower-value stock.
- **Treat Bag and Shoes as hypotheses, not strategy** — Bag shows the best margin (65.8%) and Shoes sells fastest (6.8 days), but n=2 and n=5 are too small to act on yet.
- **Watch how 2026 closes out** before treating this year's margin jump as the new normal — it's a partial year (10 months) being compared against full years.

## Data cleaning

Before touching the numbers, I ran `.info()`, `.value_counts()` and `.describe()` to see what I was actually working with:

- `Days to Sell` was stored as text ("5 Days") — converted to a numeric column, with "30+ Days"/"30 Days+" flagged separately as censored rather than treated as a real value.
- `Date` was month/year only, so the dataset is monthly-resolution.
- `Category`, `Platform` and `Brand` had case-inconsistent duplicates ("T-Shirt" vs "T-shirt", "GINZI" vs "Ginzi") — standardised to one casing.
- `"No Brand"` and `"Unknown"` were logged separately for the same thing — merged into one.
- No missing values anywhere in the 111 rows, and `Profit (£)` ties out exactly to Sale − Purchase − Shipping − Fee for every row.

## Limitations

Vinted (n=7), Private Sale (n=8), Bag (n=2) and Shoes (n=5) all have small samples, so their averages can move a lot on one unusual sale. 2026 data only runs through October, so it isn't directly comparable to the full years before it. Dates are logged at month resolution, so day-of-week or exact selling-window analysis isn't possible. Platform and time are also tangled together — the Depop→Grailed shift happened over the same period the business matured generally, so the margin improvement can't be fully separated from the platform mix changing versus the business simply getting better at pricing and sourcing over time.

## Files

| File | Contents |
| --- | --- |
| [Analysis notebook](notebooks/MG_Sales.ipynb) | Python/pandas cleaning and analysis |
| [Dashboard](dashboard/Metareligion_Sales_Dashboard.pbix) | Power BI dashboard — Power Query (M) rebuild of the same cleaning pipeline |

## Tools

Python (pandas) · Google Colab · Power BI (Power Query M)

---

*Raw data is not included for confidentiality.*
