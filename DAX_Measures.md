# DAX Measures — Superstore Sales Analysis

All measures are stored in the `Orders` table unless noted otherwise.
Organized by display folder as built in Power BI Desktop.

---

## KPIs

```dax
-- Total Sales
Total Sales = SUM(Orders[Sales])

-- Total Profit
Total Profit = SUM(Orders[Profit])

-- Total Orders
Total Orders = COUNTROWS('Orders')

-- Profit Margin %
Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)

-- Average Discount %
Average Discount % = AVERAGE(Orders[Discount])

-- % Orders Discounted
% Orders Discounted =
DIVIDE(
    COUNTROWS(FILTER('Orders', 'Orders'[Discount] > 0)),
    COUNTROWS('Orders'),
    0
)

-- Total Customers
Total Customers = DISTINCTCOUNT(Orders[Customer ID])

-- Avg Sales per Customer
Avg Sales per Customer = DIVIDE([Total Sales], [Total Customers], 0)

-- Avg Profit per Customer
Avg Profit per Customer = DIVIDE([Total Profit], [Total Customers], 0)

-- Avg Orders per Customer
Avg Orders per Customer = DIVIDE(DISTINCTCOUNT(Orders[Order ID]), [Total Customers], 0)

-- Repeat Customers
Repeat Customers =
SUMX(
    VALUES('Orders'[Customer ID]),
    IF(CALCULATE(DISTINCTCOUNT('Orders'[Order ID])) > 1, 1, 0)
)

-- % Repeat Customers
% Repeat Customers = DIVIDE([Repeat Customers], [Total Customers], 0)

-- Total Returns
Total Returns =
CALCULATE(
    DISTINCTCOUNT(Returns[Order ID]),
    FILTER(
        Returns,
        Returns[Order ID] IN VALUES(Orders[Order ID])
    )
)

-- Return Rate %
Return Rate % = DIVIDE([Total Returns], [Total Orders], 0)
```

---

## Time Intelligence

```dax
-- YTD Sales
YTD Sales = TOTALYTD([Total Sales], 'Date'[Date])

-- MTD Sales
MTD Sales = TOTALMTD([Total Sales], 'Date'[Date])

-- QTD Sales
QTD Sales = TOTALQTD([Total Sales], 'Date'[Date])

-- Same Period Last Year Sales
SPLY Sales = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))

-- YoY Growth %
YoY Growth % = DIVIDE([Total Sales] - [SPLY Sales], [SPLY Sales], 0)

-- Rolling 12M Sales
Rolling 12M Sales =
CALCULATE(
    [Total Sales],
    DATESINPERIOD('Date'[Date], MAX('Date'[Date]), -12, MONTH)
)
```

---

## Profitability

```dax
-- Gross Sales
Gross Sales =
SUMX('Orders', 'Orders'[Sales] + ('Orders'[Sales] * 'Orders'[Discount]))

-- Total Discount Amount
Total Discount Amount = SUMX('Orders', 'Orders'[Sales] * 'Orders'[Discount])

-- Total Cost
Total Cost = SUMX('Orders', 'Orders'[Sales] - 'Orders'[Profit])

-- Margin Color by Category
-- Returns green if margin >= 0, red if negative
Margin Color by Category =
IF([Profit Margin %] >= 0, "#1D9E75", "#C0384B")
```

---

## Correlations (Pearson r — calculated in DAX)

```dax
-- Correlation: Discount vs Profit (r = -0.24)
Correlation: Discount vs Profit =
VAR AvgDiscount = AVERAGE(Orders[Discount])
VAR AvgProfit   = AVERAGE(Orders[Profit])
VAR CovarianceSum =
    SUMX(Orders, (Orders[Discount] - AvgDiscount) * (Orders[Profit] - AvgProfit))
VAR DiscountVarianceSum =
    SUMX(Orders, (Orders[Discount] - AvgDiscount) ^ 2)
VAR ProfitVarianceSum =
    SUMX(Orders, (Orders[Profit] - AvgProfit) ^ 2)
VAR Denominator = SQRT(DiscountVarianceSum * ProfitVarianceSum)
RETURN DIVIDE(CovarianceSum, Denominator, 0)

-- Correlation: Discount vs Sales (r = -0.03)
Correlation: Discount vs Sales =
VAR AvgDiscount = AVERAGE(Orders[Discount])
VAR AvgSales    = AVERAGE(Orders[Sales])
VAR CovarianceSum =
    SUMX(Orders, (Orders[Discount] - AvgDiscount) * (Orders[Sales] - AvgSales))
VAR DiscountVarianceSum =
    SUMX(Orders, (Orders[Discount] - AvgDiscount) ^ 2)
VAR SalesVarianceSum =
    SUMX(Orders, (Orders[Sales] - AvgSales) ^ 2)
VAR Denominator = SQRT(DiscountVarianceSum * SalesVarianceSum)
RETURN DIVIDE(CovarianceSum, Denominator, 0)

-- Correlation: Sales vs Profit (r = 0.52 full dataset)
Correlation: Sales vs Profit =
VAR AvgSales  = AVERAGE(Orders[Sales])
VAR AvgProfit = AVERAGE(Orders[Profit])
VAR CovarianceSum =
    SUMX(Orders, (Orders[Sales] - AvgSales) * (Orders[Profit] - AvgProfit))
VAR SalesVarianceSum =
    SUMX(Orders, (Orders[Sales] - AvgSales) ^ 2)
VAR ProfitVarianceSum =
    SUMX(Orders, (Orders[Profit] - AvgProfit) ^ 2)
VAR Denominator = SQRT(SalesVarianceSum * ProfitVarianceSum)
RETURN DIVIDE(CovarianceSum, Denominator, 0)

-- Correlation: Quantity vs Profit (r = 0.07)
Correlation: Quantity vs Profit =
VAR AvgQuantity = AVERAGE(Orders[Quantity])
VAR AvgProfit   = AVERAGE(Orders[Profit])
VAR CovarianceSum =
    SUMX(Orders, (Orders[Quantity] - AvgQuantity) * (Orders[Profit] - AvgProfit))
VAR QuantityVarianceSum =
    SUMX(Orders, (Orders[Quantity] - AvgQuantity) ^ 2)
VAR ProfitVarianceSum =
    SUMX(Orders, (Orders[Profit] - AvgProfit) ^ 2)
VAR Denominator = SQRT(QuantityVarianceSum * ProfitVarianceSum)
RETURN DIVIDE(CovarianceSum, Denominator, 0)
```

---

## Shipping & Operations

```dax
-- Avg Days to Ship
Avg Days to Ship =
AVERAGEX('Orders', DATEDIFF('Orders'[Order Date], 'Orders'[Ship Date], DAY))

-- Late Shipments
-- Benchmark: Same Day > 0, First Class > 3, Second Class > 5, Standard Class > 7
Late Shipments =
COUNTROWS(
    FILTER(
        'Orders',
        VAR DaysToShip = DATEDIFF('Orders'[Order Date], 'Orders'[Ship Date], DAY)
        VAR Benchmark =
            SWITCH(
                'Orders'[Ship Mode],
                "Same Day",       0,
                "First Class",    3,
                "Second Class",   5,
                "Standard Class", 7
            )
        RETURN DaysToShip > Benchmark
    )
)

-- Late Shipment Rate %
Late Shipment Rate % = DIVIDE([Late Shipments], [Total Orders], 0)

-- Same Day Shipments
Same Day Shipments = CALCULATE([Total Orders], Orders[Ship Mode] = "Same Day")

-- Same Day Ship Rate %
Same Day Ship Rate % = DIVIDE([Same Day Shipments], [Total Orders], 0)

-- Ship Mode Order Share %
Ship Mode Order Share % =
DIVIDE(
    COUNTROWS('Orders'),
    CALCULATE(COUNTROWS('Orders'), ALL('Orders'[Ship Mode])),
    0
)

-- Profit Margin by Ship Mode %
Profit Margin by Ship Mode % = DIVIDE([Total Profit], [Total Sales], 0)

-- Late Rate Bar Color
-- Red if late rate > 1%, green if below
Late Rate Bar Color =
IF([Late Shipment Rate %] > 0.01, "#C0384B", "#1D9E75")

-- Margin Bar Color
-- Green if margin >= company average (12.05%), red if below
Margin Bar Color =
IF([Profit Margin by Ship Mode %] >= 0.1205, "#1D9E75", "#C0384B")
```

---

## Returns

```dax
-- Returned Sales
Returned Sales =
CALCULATE(
    [Total Sales],
    FILTER('Orders', RELATED(Returns[Returned]) = "Yes")
)

-- Returned Profit
Returned Profit =
CALCULATE(
    [Total Profit],
    FILTER('Orders', RELATED(Returns[Returned]) = "Yes")
)

-- Return Rate Bar Color
-- Red if above overall average (5.91%), green if below
Return Rate Bar Color =
IF([Return Rate %] > 0.0591, "#C0384B", "#1D9E75")
```

---

## Waterfall Chart
*Measure stored in the `Waterfall_Stages` calculated table*

```dax
-- Waterfall Value
-- Bridging measure — returns correct signed value per stage
Waterfall Value =
SWITCH(
    SELECTEDVALUE('Waterfall_Stages'[Stage]),
    "Gross Sales",  [Gross Sales],
    "Discount",     -[Total Discount Amount],
    "Cost",         -[Total Cost],
    "Net Profit",   [Total Profit],
    BLANK()
)
```

---

*38 measures total | Built in Microsoft Power BI Desktop | Leena A. Elsheikh*
