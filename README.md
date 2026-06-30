📊 **Sales Performance Analysis with Power BI**

<img width="709" height="329" alt="Image" src="https://github.com/user-attachments/assets/f0268fba-2b23-49e8-93e7-a8f267237efa" />


A full-scale business intelligence report analyzing 5,009 orders across 4 years (2016–2019), uncovering the hidden cost of discounting, a Same Day shipping paradox, and a 9× profitability gap between categories.
________________________________________
🗂 **Project Overview**

**Background**

This project was built as a demonstration of end-to-end business intelligence work — from raw data to executive-ready insights. The dataset used is the Sample Superstore, a widely recognized retail dataset covering four years of order transactions (2016–2019) across the United States, spanning three product categories, four sales regions, and multiple customer segments.

The goal was not simply to visualize sales figures, but to answer real business questions: Why is profit margin thin despite strong revenue growth? Is the discounting strategy actually working? Which shipping mode is truly profitable? Where are the hidden losses?

**What This Project Demonstrates**


This report goes beyond surface-level dashboarding. It applies statistical thinking — correlation analysis, time intelligence, and segmentation — to surface findings that a standard report would miss:


-The discount–sales relationship (r = −0.03) reveals that discounting is not driving volume — a finding that challenges a common business assumption
  
-The Same Day shipping paradox exposes how a customer-facing feature can be simultaneously the most failure-prone and least profitable mode

-Salesperson-level margin analysis shows how top-line revenue rankings can be misleading when profitability is factored in
A Waterfall profit bridge traces the exact path from $1.26M gross sales down to $133K net profit, step by step
________________________________________

## 📋 **Report Pages**


**Page (1)**	Executive Summary	Top-line KPIs and critical business alerts at a glance

<img width="640" height="336" alt="Image" src="https://github.com/user-attachments/assets/ea0afe2b-05b8-4ab1-abd3-8cdcfe0d5ffd" />

**Page (2)**	Overview	Sales, profit, and order volume across all dimensions

 
<img width="709" height="329" alt="Image" src="https://github.com/user-attachments/assets/6492e659-e4e1-4081-a234-891b24f95c05" />

**Page (3**)	Sales Performance	Salesperson rankings, regional breakdown, and seasonality



<img width="824" height="329" alt="Image" src="https://github.com/user-attachments/assets/43933ea0-5291-4603-bbe2-3c045bec30f8" />

**Page (4)**	Profitability	Discount impact, category margins, and cost structure


<img width="707" height="330" alt="Image" src="https://github.com/user-attachments/assets/beac06d4-78f2-4c49-92b6-203a8f872cdf" />


**Page (5**)	Customer Analysis	 and customer concentration risk

<img width="708" height="327" alt="Image" src="https://github.com/user-attachments/assets/5683b884-b666-4866-af74-a8bc11e7db7e" /> 


**page (6)**	Shipping & Operations	Ship mode performance and regional delivery reliability

 
<img width="709" height="330" alt="Image" src="https://github.com/user-attachments/assets/62a9827a-40e6-4501-a82b-c31f9226d18e" />

**Page (7)**	Returns Analysis	Return rate drivers by region, category, and Key Influencers
 
<img width="704" height="329" alt="Image" src="https://github.com/user-attachments/assets/4423f681-5870-40a6-922b-3ec8bcc76b2e" />





________________________________________
## 🔑 **Key Findings**


### 1 — The Discount Strategy Is Backfiring


52% of all orders are discounted — yet discounts have near-zero effect on sales volume (r = −0.03) and actively erode profit (r = −0.24). The business is giving away margin without gaining sales in return.

•	$157K in discounts contributed to only $133K net profit on $1.26M gross sales

•	Net profit margin: 10.6% — thin, and at risk if discounting continues unchecked

•	Cost consumes 77% of gross sales ($967K / $1,257K) — the real lever is cost management
________________________________________

### 2 — Technology is 9 times more profitable than Furniture per dollar of sales.

| Category | Profit Margin |
| --- | --- |
| Technology | 18.4% (BEST) |
| Office Supplies | ~15% |
| Furniture | 2.0% (LOWEST) |

•	Only 3 of 17 sub-categories are unprofitable: Tables, Bookcases, and Supplies

•	Tables recorded a −$11K net loss over the full 4-year period — the single biggest drag


•	Targeting these three sub-categories alone could meaningfully lift overall margins
________________________________________

### 3 — The Same Day Shipping Paradox

| Ship Mode | Orders | Late Rate | Profit Margin |
| --- | --- | --- | --- |
| Same Day | 264 | 4.55% HIGH | 3.05% LOW |
| First Class | 787 | 0.13% OK | 15.26% BEST |
| Standard Class | ~3,000 | 0.00% OK | — |
| Second Class | — | 0.00% OK | — |

- Same Day is **35× more likely to be late** than First Class
- Same Day earns **4× less profit** than the company average (12%)
- 12 out of 264 Same Day orders were **not shipped same day**
- First Class is the strategic opportunity: highest margin, near-perfect reliability
________________________________________
   ### 4 — Regional Performance Divergence


| Region | Avg Ship Days | Late Orders | Profit Margin |
| --- | --- | --- | --- |
| East | 3.97 days | Lowest | 15.9% (BEST) |
| West | 3.93 days | 8 of 13 total | 12% |
| Central | 4.0 days | Low | 4.6% (LOWEST) |
| South | 3.97 days | Low | 12% |

East is the operational benchmark across all dimensions
West hides a consistency problem behind a fast average — 8 of 13 late shipments originate here
Central is the most urgent concern: slowest AND least profitable, at nearly 3.5x below East's margin
________________________________________

 ###  5 — Customer Concentration Risk


•	Top 10 customers = 51.3% of total revenue — losing 1–2 customers has outsized impact

•	98.49% repeat buyer rate — strong retention, but raises a critical question: 

Are customers returning because of loyalty — or because of discounts?

•	Home Office is the highest-margin segment (15.5%) despite being the smallest by order volume (909 orders)

•	Corporate has the lowest margin (10.1%) despite being second in sales — likely over-discounted to win deals

________________________________________


 ###  6 — The forecast projects

 
The forecast projects a seasonal Q4 2020 peak of approximately $50–55K. While this aligns with historical trends, the widening confidence interval suggests slowing growth and increasing uncertainty.

________________________________________

##   🛠 **Technical Highlights**


Data Model

The report is built on a clean star schema with a dedicated Calendar table enabling full time intelligence support. Relationships are managed with single-direction cross-filtering to prevent ambiguity, and a Returns table is joined to the Orders table to enable return rate analysis at the order level.


 ##     **Report Features**


•	Time Intelligence: YTD, YoY, ETS 12-month sales forecast

•	Waterfall Chart: Profit bridge (Gross Sales → Discounts → Cost → Net Profit)

•	Scatter Plot: Discount vs Profit Margin with regression insight

•	Conditional Formatting: Margin bars color-coded by threshold

•	Cross-page Slicers: Year, Category, Region, Salesperson
________________________________________

 ##  📌 **Strategic Recommendations**




(1) 	52% discounted orders; r = −0.03 with Sales	Conduct discount audit; set category-specific caps

(2)	 Tables: −$11K structural loss over 4 years	Review pricing and cost structure; evaluate repositioning

(3)	 Same Day: 4.55% late rate + 3.05% margin	Reprice or tighten SLA before continuing to offer

(4) 	Central: lowest margin (4.6%) + slowest shipping	Investigate discount depth and product mix

(5) 	Top 10 customers = 51.3% of revenue	Launch key account retention program; diversify

(6)	   First Class: 15.26% margin, 0.13% late rate	Incentivize customers toward First Class over Same Day
________________________________________
##    👤 **About the Author**


Leena A. Elsheikh

Data Analyst · Freelance  Lecturer· Bilingual (Arabic / English)

•	🎓 MSc in Statistics · MBA · Microsoft PL-300 (Power BI Data Analyst)

•	🛠 Stack: Power BI · SQL · R · Stata

•	🏫 10+ years university-level teaching in Statistics and Quantitative Methods

•	📍 Based in Riyadh, Saudi Arabia
 
________________________________________
## 📄 **License**


This project uses the publicly available Sample Superstore dataset for portfolio and educational purposes.
________________________________________

Built with Microsoft Power BI Desktop · 2025

