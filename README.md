# Metareligion Sales Analysis (Feb 2023 - Oct 2026)

Metareligion is an archive-fashion resale business I've run since February 2023, selling on Depop, Grailed, Vinted and through private sales. This project cleans and analyses 111 sales I logged over that period, covering purchase cost, sale price, fees, shipping and realised profit per item.

**Questions**
1. Which channel actually protects margin once price tier is accounted for, and why?
2. Which categories and price tiers should Metareligion source more of, based on profit, margin and resale speed?

![Average margin by platform](MG%20Margin%20by%20Platform.png)
![Total profit by category](MG%20Profit%20by%20Category.png)

## Key findings

- **The Depop-Grailed margin gap is mostly a price-tier illusion.** Raw numbers put Grailed about 5 points ahead on margin (48.0% vs 43.2%), but 71% of Grailed sales are over £200 against only 16% of Depop's. Within the same price band, the gap shrinks to 1-3 points in every tier.
- **Grailed's fees run roughly double Depop's, but its buyers pay enough extra to cover them.** Cost drag (fees + shipping as a share of sale price) is about 2x higher on Grailed at every price tier, e.g. 34.6% vs 17.8% under £100. Margins still come out roughly even, so what protects margin is buyers' willingness to pay for archive pieces, not the platform.
- **Jacket and Jeans are the backbone of the business.** They make up 68% of sales and about 86% of total profit, with margins of 46-48% and turnover of 9-11 days.
- **The channel mix flipped in 2026.** Depop went from 100% of sales in 2023-2024 to 26% in 2026, while Grailed rose to 48%. In the same year the business had its best profit and margin yet (£3,281.5 profit, 51.4% average margin). Depop traffic has dried up, and Vinted only works while I'm physically in the UK, so the shift is as much about which channels I can still use as about a deliberate choice.

## Recommendations

- **Keep Jacket and Jeans at the core of sourcing.** They are the most proven part of the business on volume, profit and speed.
- **Use Grailed more for higher-value pieces.** Its fees aren't better, but its buyers pay enough extra to absorb them. It is not the right channel for lower-value stock.
- **Treat Bag and Shoes as hypotheses, not strategy.** Bag has the best margin (65.8%) and Shoes sell fastest (6.8 days), but samples of 2 and 5 are too small to act on.
- **Wait for 2026 to close out** before treating this year's margin jump as the new normal. It is a 10-month year being compared against full years.

## Data cleaning (Python and Power Query)

Before touching the numbers, I ran `.info()`, `.value_counts()` and `.describe()` to see what I was working with:

- `Days to Sell` was stored as text ("5 Days"). I converted it to a number, and flagged "30+ Days"/"30 Days+" as censored instead of treating 30 as the real value.
- `Date` was logged as month/year only, so the dataset is monthly-resolution.
- `Category`, `Platform` and `Brand` had case-inconsistent duplicates ("T-Shirt" vs "T-shirt", "GINZI" vs "Ginzi"), which I standardised.
- "No Brand" and "Unknown" meant the same thing, so I merged them.
- There were no missing values, and `Profit (£)` matched Sale/Purchase/Shipping/Fee exactly on every row.
- I added three ratio metrics: **margin %** (profit ÷ sale price), **ROI %** (profit ÷ purchase price) and **cost drag %** ((shipping + fees) ÷ sale price). One gifted item with a £0 purchase price is excluded from ROI averages only.
- In the Power BI dashboard, I rebuilt the same cleaning steps in Power Query (M) instead of loading the cleaned output from Python.

## Limitations

Vinted (n=7), Private Sale (n=8), Bag (n=2) and Shoes (n=5) have small samples, so one unusual sale can move their averages a lot. 2026 only runs through October, so it can't be compared directly with full years. Dates are logged by month, so day-of-week or exact selling-window analysis isn't possible. Platform and time also overlap: the Depop to Grailed shift happened while the business was maturing, so I can't fully separate the effect of the platform mix from simply getting better at pricing and sourcing over time.

## Files

| File | Contents |
| --- | --- |
| [Analysis notebook](MG_Sales.ipynb) | Python (pandas) cleaning and analysis |
| [Power BI dashboard](MG_Resell_Analytics.pbix) | KPI cards, profit by category and average margin by platform, with cleaning rebuilt in Power Query (M) |

## Tools

Python (pandas) · Google Colab · Power BI (Power Query M)

---

*Raw data is not included for confidentiality.*
