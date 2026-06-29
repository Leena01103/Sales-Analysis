📊 Superstore Sales Analysis with Power BI

A full-scale business intelligence report analyzing 5,009 orders across 4 years (2016–2019), uncovering the hidden cost of discounting, a Same Day shipping paradox, and a 9× profitability gap between categories.
________________________________________
🗂 Project Overview
Detail	Info
Dataset	Sample Superstore (2016–2019)
Tool	Microsoft Power BI Desktop
Report Pages	7
DAX Measures	20+ custom measures
Author	Leena A. Elsheikh
Certifications	MSc Statistics · MBA · Microsoft PL-300
________________________________________

📋 Report Pages
1	Executive Summary	Top-line KPIs and critical business alerts at a glance

2	Overview	Sales, profit, and order volume across all dimensions
3	Sales Performance	Salesperson rankings, regional breakdown, and seasonality
4	Profitability	Discount impact, category margins, and cost structure
5	Customer Analysis	Segment profitability and customer concentration risk
6	Shipping & Operations	Ship mode performance and regional delivery reliability
7	Returns Analysis	Return rate drivers by region, category, and Key Influencers
________________________________________
🔑 Key Findings
1 — The Discount Strategy Is Backfiring
52% of all orders are discounted — yet discounts have near-zero effect on sales volume (r = −0.03) and actively erode profit (r = −0.24). The business is giving away margin without gaining sales in return.
•	$157K in discounts contributed to only $133K net profit on $1.26M gross sales
•	Net profit margin: 10.6% — thin, and at risk if discounting continues unchecked
•	Cost consumes 77% of gross sales ($967K / $1,257K) — the real lever is cost management
________________________________________
2 — A 9× Profitability Gap Between Categories
Category	Profit Margin
Technology	18.4% ✅
Office Supplies	~15% ✅
Furniture	2.0% ⚠️
•	Only 3 of 17 sub-categories are unprofitable: Tables, Bookcases, and Supplies
•	Tables recorded a −$11K net loss over the full 4-year period — the single biggest drag
•	Targeting these three sub-categories alone could meaningfully lift overall margins
________________________________________
3 — The Same Day Shipping Paradox
Ship Mode	Orders	Late Rate	Profit Margin
Same Day	264	4.55% 🔴	3.05% 🔴
First Class	787	0.13% ✅	15.26% ✅
Standard Class	~3,000	0% ✅	—
Second Class	—	0% ✅	—
•	Same Day is 35× more likely to be late than First Class
•	Same Day earns 4× less profit than the company average (12%)
•	12 out of 264 Same Day orders were not shipped same day
•	First Class is the strategic opportunity: highest margin, near-perfect reliability
________________________________________
4 — Regional Performance Divergence
Region	Avg. Ship Days	Late Orders	Profit Margin
East	~3.97	Lowest	15.9% 🏆
West	3.93	8 of 13 total	~12% ⚠️
Central	4.0	Low	4.6% 🔴
South	~3.97	Low	~12%
•	East is the operational benchmark across all dimensions
•	West hides a consistency problem behind a fast average — 8 of 13 late shipments originate here
•	Central is the most urgent concern: slowest AND least profitable, at nearly 3.5× below East's margin
________________________________________
5 — Customer Concentration Risk
•	Top 10 customers = 51.3% of total revenue — losing 1–2 customers has outsized impact
•	98.49% repeat buyer rate — strong retention, but raises a critical question: 
Are customers returning because of loyalty — or because of discounts?
•	Home Office is the highest-margin segment (15.5%) despite being the smallest by order volume (909 orders)
•	Corporate has the lowest margin (10.1%) despite being second in sales — likely over-discounted to win deals
________________________________________
🛠 Technical Highlights
DAX Measures (selected)
-- Sales Last Year (Time Intelligence) 
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Calendar'[Date]))
-- Year-over-Year Growth
YoY Sales Growth % = 
DIVIDE([Total Sales] - [Sales LY], [Sales LY])


-- Profit Margin %
Profit Margin % = DIVIDE([Total Profit], [Total Sales])

-- Discount-Profit Correlation
Discount vs Profit Correlation = 
CALCULATE(... )  -- Pearson r implemented via VAR/RETURN pattern

-- Late Shipment Rate %
Late Shipment Rate % = DIVIDE( COUNTROWS(FILTER(Orders, Orders[Days to Ship] > Orders[Benchmark Days])), COUNTROWS(Orders)



Report Features
•	Time Intelligence: YTD, YoY, ETS 12-month sales forecast
•	Waterfall Chart: Profit bridge (Gross Sales → Discounts → Cost → Net Profit)
•	Scatter Plot: Discount vs Profit Margin with regression insight
•	Conditional Formatting: Margin bars color-coded by threshold
•	Cross-page Slicers: Year, Category, Region, Salesperson
________________________________________
📌 Strategic Recommendations
#	Finding	Action
1	52% discounted orders; r = −0.03 with Sales	Conduct discount audit; set category-specific caps
2	Tables: −$11K structural loss over 4 years	Review pricing and cost structure; evaluate repositioning
3	Same Day: 4.55% late rate + 3.05% margin	Reprice or tighten SLA before continuing to offer
4	Central: lowest margin (4.6%) + slowest shipping	Investigate discount depth and product mix
5	Top 10 customers = 51.3% of revenue	Launch key account retention program; diversify
6	First Class: 15.26% margin, 0.13% late rate	Incentivize customers toward First Class over Same Day
________________________________________
👤 About the Author
Leena A. Elsheikh
Data Analyst · Freelance  Lecturer· Bilingual (Arabic / English)
•	🎓 MSc in Statistics · MBA · Microsoft PL-300 (Power BI Data Analyst)
•	🛠 Stack: Power BI · SQL · R · Stata
•	🏫 10+ years university-level teaching in Statistics and Quantitative Methods
•	📍 Based in Riyadh, Saudi Arabia
 
________________________________________
📄 License
This project uses the publicly available Sample Superstore dataset for portfolio and educational purposes.
________________________________________
Built with Microsoft Power BI Desktop · 2025

