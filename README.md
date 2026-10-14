# AtliQ Hardware – Sales & Market Analysis

> Codebasics Data Analytics Bootcamp · Excel module · End-to-end project
> **Author:** Shantanu Dhara

## 1. Problem
AtliQ Hardware sells PCs, peripherals, storage and networking products (a Dell/HP-style business) through three channels: **Retailer** (Croma, Amazon, Best Buy…), **Direct** (AtliQ e-Store, AtliQ Exclusive) and **Distributor** (e.g. China, South Korea). After a costly expansion into LATAM, driven by surveys and intuition, management wants **data-backed decisions**. Basic Excel analysis no longer scales, and Dell competes hard with a large analytics team. This project answers five business questions:

1. Top 10 products by % net-sales growth, 2020 → 2021
2. Division-level net sales and growth
3. Top 5 and bottom 5 products by quantity sold
4. New products launched in 2021
5. Top 5 countries by net sales in 2021

## 2. Data
| Table | Type | Description |
|---|---|---|
| `fact_sales_monthly` | Fact | Monthly `date, product_code, customer_code, Qty, net_sales_amount` (from Sep 2018). Too large for GitHub, so only a sample is included. |
| `dim_customer` | Dimension | customer, market, platform (Brick & Mortar / E-Commerce), channel |
| `dim_product` | Dimension | division, segment, category, product, variant |
| `dim_market` | Dimension | market → sub_zone → region |
| `ns_targets_2021` | Target | Monthly net-sales target per market, Sep 2020 – Aug 2021 |

## 3. Approach
1. **Load and model**: star schema in Power BI. The fact table joins to the product and customer dimensions on codes, and customers join to markets.
2. **Clean**: fix encoding (`Elkj�p`), the `Philiphines` typo, `nan` sub-zone/region for Canada and USA, and negative `Qty` (returns).
3. **Measures**: Net Sales, Qty, Net Sales LY, YoY % (`21 vs 20`).
4. **Reports**: one sheet per question, each with region / division / customer filters. Values are in USD.
5. **New products**: products with no 2020 sales (blank or 0 in 2020) but sales in 2021.

## 4. Results
| Question | Finding |
|---|---|
| Overall | Net sales grew **$196.7M → $598.9M (+204.5%)** |
| Top-10 growth | Led by **AQ Mx NB** (+5,624%), **AQ LION x1/x2/x3** (~+1,600–1,700%) and **AQ Smash 2** (+2,490%, $11.2M). The top 10 total $6.4M → $52.0M. |
| Divisions | **P & A** $105.2M → $338.4M (+221%) · **PC** $40.1M → $165.8M (+314%) · **N & S** $51.4M → $94.7M (+84%) |
| Qty – top 5 | AQ Master wired x1 Ms (4.2M), AQ Master wireless x1 Ms (4.1M), AQ Gamers Ms (4.0M), AQ Gamers (3.4M), AQ Master wireless x1 (3.4M): 19.0M units in total |
| Qty – bottom 5 | AQ HOME Allin1 Gen 2 (8.9K), AQ Home Allin1 (15.2K), AQ Smash 2 (36.0K), AQ Gamer 1 (51.7K), AQ GEN Z (63.1K): 174.9K units in total |
| New in 2021 | 16 products worth **$176.2M**. Top sellers: AQ Qwerty ($22.0M), AQ Trigger ($20.7M), AQ Gen Y ($19.5M), AQ Trigger Ms ($17.9M), AQ Wi Power Dx3 ($17.2M). |
| Top 5 countries, 2021 | **India $161.3M**, USA $87.8M, South Korea $49.0M, Canada $35.1M, UK $34.2M. Together $367.2M. |

## 5. Insights
- **P & A (peripherals and accessories) drives the business**: about 56% of 2021 sales, and the top-5 volume list is all keyboards and mice.
- **New launches matter**: the 16 new products contribute about 29% of 2021 sales.
- **Growth is concentrated in a few markets**: the top 5 countries make up about 61% of sales, and India alone about 27%.
- **High-ticket PCs sell in low volume**: all bottom-5 products except AQ Smash 2 are low-unit items. AQ Smash 2 and AQ Home Allin1 appear in both the top-10 growth list and the bottom-5 quantity list, so their growth comes from a small base.
- **N & S is the slowest division** (+84% against +204% overall).

## 6. Recommendations
1. Keep investing in **P & A**, with more variants and bundles of the keyboard, mouse and battery lines that are growing fastest.
2. Repeat the **new-product playbook**: launch regularly and track each launch's first-year sales.
3. **Scale carefully into new markets.** Use market data such as sales against `ns_targets` before expanding, not surveys alone (the LATAM lesson). Reduce dependence on India by growing the USA, Canada and Europe.
4. **Review the weak products** (AQ Home Allin1 family, AQ Gamer 1, AQ GEN Z) and decide whether to reprice, promote or retire them.
5. **Look into N & S** to see why growth lags: pricing, channel mix or product range.

## 7. Folder structure
```
atliq-hardware-sales-analysis/
├── README.md
├── datasets/
│   ├── raw/        # dim_customer, dim_market, dim_product, ns_targets_2021 (CSV)
│   └── sample/     # fact_sales_monthly_sample.csv (the full file is too large)
├── reports/        # assignment_solution.xlsx (5 report sheets)
└── business_problem/           # problem_statement.pdf and report.pdf
```

## 8. Tools
Excel (Data model, DAX measures, Reports, Data Transformation, Data Cleaning).

## 9. Notes
- All values are in USD, taken from the Excel solution file.
- The fiscal year appears to run **September to August**. The targets file covers Sep 2020 – Aug 2021, so "2021" is read as FY2021. 
- Negative `Qty` and `net_sales_amount` rows are returns and are included in the totals.
