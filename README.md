# Late Deliveries and Customer Satisfaction – Olist (Power BI)

Power BI dashboard that answers one question: **do late deliveries hurt customer satisfaction, and if they do, where and why do they happen?**

Course project – Business Intelligence (M1, UPEC) – Bernardo Gomes

**Power BI file and PDF:** [Google Drive folder](https://drive.google.com/drive/folders/1YvnLJ1apRmql1Z-cSamve3dp-_qZjIqE)

## The case

[Olist](https://olist.com) is a Brazilian marketplace that connects small shops to large online stores. The public dataset contains about 99,000 real, anonymized orders placed between 2016 and 2018, split into 9 CSV tables.

- Dataset: [Brazilian E-Commerce Public Dataset by Olist (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- Period analyzed: January 2017 to August 2018 (96,203 delivered orders)

## Main results

| Finding | Value |
| --- | --- |
| Share of orders delivered late | 6.8% |
| Average review, on-time vs late orders | 4.3 vs 2.3 |
| Worst month | March 2018 (19% late) |
| Worst customer state | Alagoas (21% late) |
| Days with the carrier, late vs on-time orders | 27 vs 7.5 |
| Late rate when the seller ships after the deadline | 21% (vs 5%) |
| Late orders that started with a late shipment by the seller | 28% |

## Dashboard pages

1. **Overview** – the problem: late rate over time and its impact on the review score.
2. **Where** – late rate by customer state, seller state, product category and top sellers.
3. **Why and what to do** – causes (carrier time, late shipping by sellers) and four recommendations.

## How it was built (summary, full details in [BUILD_GUIDE.pdf](BUILD_GUIDE.pdf))

1. Imported 7 of the 9 CSV files into Power BI Desktop (Get data → Text/CSV, locale English US).
2. Power Query:
   - Orders: kept only delivered orders with a delivery date; added `DelayDays`, `DeliveryStatus` (Late / On time) and `DeliveryDays`.
   - Reviews: grouped by order and averaged the score (some orders had several reviews).
   - Category translation: promoted the first row to headers.
3. Model: star schema with **Orders** in the center, many-to-one relationships, single filter direction.
4. DAX measures: Total Orders, Late Orders, Late %, Avg Review, Avg Delivery Days, and "(Items)" versions for the seller and category analysis (using `CROSSFILTER`).
5. DAX columns: Purchase Month, Seller, CarrierDays, SellerShipping.
6. Report filter: purchases from January 2017 (2016 had too few orders).

## Files

| File | Content |
| --- | --- |
| `INSTALL.pdf` | How to install Power BI Desktop and get the data |
| `BUILD_GUIDE.pdf` | Step-by-step guide to rebuild the dashboard (Power Query, model, DAX, pages) |
| `Olist_Dashboard.pdf` | The three dashboard pages as PDF |
| `README.pdf` | This page as PDF |

**The Power BI file (`Projeto_BI_Olist_Atrasos.pbix`) is larger than GitHub's 25 MB upload limit, so it is shared on Google Drive: [download the .pbix file](https://drive.google.com/drive/folders/1YvnLJ1apRmql1Z-cSamve3dp-_qZjIqE).**

The CSV files are not included: download them from the Kaggle link above.

## How to open the project

1. Install Power BI Desktop (see [INSTALL.pdf](INSTALL.pdf)).
2. Download the `.pbix` file from the [Google Drive folder](https://drive.google.com/drive/folders/1YvnLJ1apRmql1Z-cSamve3dp-_qZjIqE) and open it.
3. To refresh the data from your own copy of the CSVs: Home → Transform data → Data source settings → Change Source, and point each table to your folder.
