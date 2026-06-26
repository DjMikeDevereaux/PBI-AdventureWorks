# PBI-AdventureWorks
Power BI Report, including chart, cards, maps, tables, sliders, parameters, narrative, tooltipdecomposition tree, key influencers

📦 dashboard-AdventureWorks Report/
│── README.md
│── pbix/
│     └── AdventuresWorks_Report.pbix
│── data/
│     ├── AdventureWorks Calendar Lookup.csv
│     ├── AdventureWorks Customer Lookup.csv
│     ├── AdventureWorks Product Categories Lookup.csv
│     ├── AdventureWorks Product Lookup.csv
│     ├── AdventureWorks Product Subcategories Lookup.csv
│     ├── AdventureWorks Returns Data.csv
│     └── AdventureWorks Sales Data 2020.csv
│     └── AdventureWorks Sales Data 2021.csv
│     └── AdventureWorks Sales Data 2022.csv
│     └── AdventureWorks Territory Lookup.csv
│── screenshots/
│     ├── Exec_Dashboard.png
│     ├── Map.png
│     ├── Product_deatail.png
│     └── Customer_detail.png

# 📊 Sales Dashboard 2020–2022 – Power BI

This project presents an **interactive dashboard in Power BI** based on historical sales data from **2020 to 2022**, complemented with information on **territories**, **customers**, **products**, **subcategories**, **returns**, and a **calendar table** for advanced time analysis.

The goal is to provide a clear and actionable view of business performance, allowing the identification of trends, seasonal variations, key territories, customer behavior, and product analysis.

---

## 🚀 Project Goal

Build a professional dashboard that allows you to:

- Analyze sales by year, month, territory, customer, and product.
- Compare territories and their contribution to the total.
- Evaluate customer and product behavior.
- Analyze returns and their impact on net sales.
- Detect seasonal patterns and demand peaks.
- Facilitate data-driven strategic decisions.

---

## 🧱 Tables

### **1. Sales Data (2020–2022)**:
- Order Date  
- StockDate  
- OrderNumber  
- ProductKey  
- CustomerKey  
- TerritoryKey
- OrderLineItem
- OrderQuantity

### **2. Territory Lookup**
- SalesTerritoryKey  
- Region
- Country
- Continent

### **3. Calendar Lookup**
- Date  
- Day Name  
- Start of Week  
- Start of Month  
- Start of Quarter
- Month Name
- Month
- Start of Year
- Year

### **4. Customer Lookup**
- CustomerKey  
- Prefix 
- FirstName 
- FirstName
- BirthDate
- MaritalStatus
- Gender
- EmailAddress
- AnnualIncome
- TotalChildren
- EducationLevel
- Occupation
- HomeOwner

### **5. Returns Data**
- ReturnDate  
- TerritoryKey  
- ProductKey  
- ReturnQuantity  

### **6. Product Lookup**
- ProductKey
- ProductSubcategoryKey  
- ProductSKU  
- ProductName
- ModelName
- ProductDescription
- ProductColor
- ProductStyle
- ProductCost
- ProductPrice
- SKU Type

### **7. Product Categories Lookup**
- ProductCategoryKey  
- CategoryName

### **8. Product Subcategories Lookup**
- ProductSubcategoryKey  
- SubcategoryName
- ProductCategoryKey

---

## 🧠  Data Modeling

The model was built under a semantic model:

Main relationships:
- Sales Data[OrderDate] → Calendar Lookup[Date]
- Sales Data[CustomerKey] → Customer Lookup[CustomerKey]
- Sales Data[TerritoryKey] → Territory Lookup[SalesTerritoryKey]
- Sales Data[ProductKey] → Product Lookup[ProductKey]
- Product Lookup[ProductSubcategoryKey] → Product Subcategories Lookup[ProductSubcategoryKey]
- Product Subcategories Lookup[ProductSubcategoryKey] → Product Categories Lookup[ProductCategoryKey]
- Returns Data[ProductKey] → Product Lookup[ProductKey]
- Returns Data[ReturnDate] → Calendar Lookup[Date]
- Returns Data[TerritoryKey] → Territory Lookup[SalesTerritoryKey]

---

## 📈 Dashboard Visualizations

Includes:

- **KPIs**: Total Revenue, Total Profit, Total Orders, Return Rate, Monthly: Revenue, Orders and Returns
- **Time trend**: Revenue Trending.
- **Bars Orders by Category**.
- **Matrix Yop 10 Products**
- **Map Orders by territory**.
- **Gauge charts** Profit, Orders and Revenue vs targets
- **Card: Most important customers by Revenue**.
- **Returns analysis**: return rate, revenue impact.
- **Slicers**: Year, month, territory, customer, product, subcategory.

---

## 🧮 Main DAX Measures

Type	   Name	                Expression	          Description	  Location
Measure	 % of All Orders	"
                              DIVIDE(
                                  [Total Orders],
                                  [All Orders]
                              )
                              "		                                Measure Table
Measure	% of All Returns	"
                              DIVIDE(
                                  [Total Returns],
                                  [All Returns]
                              )"		                              Measure Table
Measure	10-day Rolling Reveneu	"
                              CALCULATE(
                                  [Total Revenue],
                                  DATESINPERIOD(
                                      'Calendar Lookup'[Date],
                                      MAX(
                                          'Calendar Lookup'[Date]
                                      ),
                                      -10,
                                      DAY))"		                  Measure Table
Measure	90-day Rolling Profit	"
                              CALCULATE(
                                  [Total Profit],
                                  DATESINPERIOD(
                                      'Calendar Lookup'[Date],
                                      MAX(
                                          'Calendar Lookup'[Date]
                                      ),
                                      -90,
                                      DAY))"		                 Measure Table
Measure	Adjusted Price	      [Average Retail Price] * 
                              ( 1 + 'Price Adjustment (%)
                              '[Price Adjustment (%) Value])	   Measure Table
Measure	Adjusted Profit  	"
                          [Adjusted Revenue] - [Total Cost]"		 Measure Table
Measure	Adjusted Revenue	"
                          SUMX('Sales Data',
                              'Sales Data'[OrderQuantity]
                              *
                               [Adjusted Price]
                              )"		                             Measure Table
Measure	All Orders	      "
                          CALCULATE(
                              [Total Orders],
                              ALL('Sales Data')
                              )"		                             Measure Table
Measure	All Returns	"
                          CALCULATE(
                              [Total Returns],
                              ALL(
                                  'Returns Data'
                              ))"		                             Measure Table
Measure	Average Retail Price	"
                          AVERAGE(
                              'Product Lookup'[ProductPrice])"	 Measure Table
Measure	Average Revenue per Customer	"
                          DIVIDE(
                              [Total Revenue],
                              [Total Customers])"		             Measure Table
Measure	Bike Returns	"
                          CALCULATE(
                              [Total Returns],
                              'Product Categories Lookup'
                              [CategoryName] = ""Bikes""
                          )"		                                 Measure Table
Measure	Bike Sales	"
                          CALCULATE(
                              [Quantity Sold],
                              'Product Categories Lookup'[CategoryName] = ""Bikes""
                          )
                          "		                                   Measure Table
Measure	Bikes Return Rate	"
                          CALCULATE(
                              [Return Rate],
                              'Product Categories Lookup
                              '[CategoryName] = ""Bikes""
                          )"		                                 Measure Table
Measure	Bulk Orders	"
                          CALCULATE(
                              [Total Orders],
                              'Sales Data'[OrderQuantity] > 1
                          )"		                                Measure Table
Measure	Full Name         (Customer Detail)	"
                          IF(
                              HASONEVALUE(
                                  'Customer Lookup'[CustomerKey]
                              ),
                              MAX(
                                  'Customer Lookup'
                                  [Customer Full Name (CC)]
                                  ),
                                  ""Multiple Customers""
                                  )"		Customer Lookup
Measure	High Ticket Orders	"
                          CALCULATE(
                              [Total Orders],
                              FILTER(
                                 'Product Lookup', 
                              'Product Lookup'[ProductPrice] 
                              > [Overall Average Price]
                          ))"		                                Measure Table
Measure	Measure 2	BLANK()		Calendar Lookup
Measure	Order Target	"
        [Previous Month Orders] * 1.1"	10% increase compared to previous month order volume	Measure Table
Measure	Order Target Gap	"[Total Orders] - [Order Target]
"		Measure Table
Measure	Overall Average Price	"
CALCULATE(
    [Average Retail Price],
    ALL(
        'Product Lookup'
    )
    )"		Measure Table
Measure	Previous Month Orders	"
    CALCULATE(
        [Total Orders],
        DATEADD(
            'Calendar Lookup'[Date],
            -1,
            MONTH
            ))"		Measure Table
Measure	Previous Month Profit	"
    CALCULATE(
        [Total Profit],
        DATEADD(
            'Calendar Lookup'[Date],
            -1,
            MONTH
            ))"		Measure Table
Measure	Previous Month Returns	"
    CALCULATE(
        [Total Returns],
        DATEADD(
            'Calendar Lookup'[Date],
            -1,
            MONTH
            ))"		Measure Table
Measure	Previous Month Revenue	"
    CALCULATE(
        [Total Revenue],
        DATEADD(
            'Calendar Lookup'[Date],
            -1,
            MONTH
        ))"		Measure Table
Measure	Price Adjustment (%) Value	SELECTEDVALUE('Price Adjustment (%)'[Price Adjustment (%)], 0)		Price Adjustment (%)
Measure	Profit Target	"
        [Previous Month Profit] * 1.1"		Measure Table
Measure	Profit Target Gap	[Total Profit] - [Profit Target]		Measure Table
Measure	Quantity Return	"
SUM(
    'Returns Data'[ReturnQuantity]
    )"		Measure Table
Measure	Quantity Sold	"
SUM(
    'Sales Data'[OrderQuantity])"		Measure Table
Measure	Return Rate	"
[Quantity Return] / [Quantity Sold]
"		Measure Table
Measure	Revenue Sparkline	"
// Static line color - use %23 instead of # for Firefox compatibility (Measure Derived from Eldersveld Modified by Kolosko)
VAR LineColour = ""%2320E2D7""
VAR PointColour = ""%23333333""
VAR Defs = ""<defs>
    <linearGradient id='grad' x1='0' y1='25' x2='0' y2='50' gradientUnits='userSpaceOnUse'>
        <stop stop-color='#20e27d' offset='0' />
        <stop stop-color='#20e27d' offset='0.3' />
        <stop stop-color='#333333' offset='1' />
    </linearGradient>
</defs>""
// ""Date"" field used in this example along the X axis
VAR XMinDate = MIN('Calendar Lookup'[Start of Month])
VAR XMaxDate = MAX('Calendar Lookup'[Start of Month])

// Obtain overall min and overall max measure values when evaluated for each date
VAR YMinValue = MINX(VALUES('Calendar Lookup'[Start of Month]),CALCULATE([Total Revenue]))
VAR YMaxValue = MAXX(Values('Calendar Lookup'[Start of Month]),CALCULATE([Total Revenue]))

// Build table of X & Y coordinates and fit to 50 x 150 viewbox
VAR SparklineTable = ADDCOLUMNS(
    SUMMARIZE('Calendar Lookup','Calendar Lookup'[Start of Month]),
        ""X"",INT(150 * DIVIDE('Calendar Lookup'[Start of Month] - XMinDate, XMaxDate - XMinDate)),
        ""Y"",INT(50 * DIVIDE([Total Revenue] - YMinValue,YMaxValue - YMinValue)))

// Concatenate X & Y coordinates to build the sparkline
VAR Lines = CONCATENATEX(SparklineTable,[X] & "","" & 50-[Y],"" "", 'Calendar Lookup'[Start of Month])

// Last data points on the line
VAR LastSparkYValue = MAXX( FILTER(SparklineTable, 'Calendar Lookup'[Start of Month] = XMaxDate), [Y])
VAR LastSparkXValue = MAXX( FILTER(SparklineTable, 'Calendar Lookup'[Start of Month] = XMaxDate), [X])

// Add to SVG, and verify Data Category is set to Image URL for this measure
VAR SVGImageURL = 
    ""data:image/svg+xml;utf8,"" & 
    --- gradient---
    ""<svg xmlns='http://www.w3.org/2000/svg' x='0px' y='0px' viewBox='-7 -7 164 64'>"" & Defs & 
     ""<polyline fill='url(#grad)' fill-opacity='0.3' stroke='transparent' 
      stroke-width='0' points=' 0 50 "" & Lines & 
      "" 150 150 Z '/>"" &
    --- Lines---
    ""<polyline 
        fill='transparent' stroke='"" & LineColour & ""' 
        stroke-linecap='round' stroke-linejoin='round' 
        stroke-width='2' points=' "" & Lines & 
      "" '/>"" &
    --- Last Point---
        ""<circle cx='""& LastSparkXValue & ""' cy='"" & 50 - LastSparkYValue & ""' r='4' stroke='"" & LineColour & ""' stroke-width='2' fill='"" & PointColour & ""' />"" &
        ""</svg>""
RETURN SVGImageURL
"		Measure Table
Measure	Revenue Target	"
        [Previous Month Revenue] * 1.1"		Measure Table
Measure	Revenue Target Gap	[Total Revenue] - [Revenue Target]		Measure Table
Measure	Revenue Target Gap with Arrow	"
var uparrow = UNICHAR(129129)
var downarrow = UNICHAR(129131)
var revenuegap = [Revenue Target Gap]

RETURN
IF(revenuegap< 0,
Format(Round(revenuegap, 0), ""#,###"")&"" ""&downarrow,

format(round(revenuegap, 0), ""#,###"")&"" ""&uparrow)"		Measure Table
Measure	Total Cost	"
SUMX(
        'Sales Data',
        'Sales Data'[OrderQuantity] *
        RELATED(
            'Product Lookup'[ProductCost]
        ))"	Multiplies each order quantity in the Sales Data table by the related product cost in the Product  Lookup table, and sums the result 	Measure Table
Measure	Total Customers	"
DISTINCTCOUNT(
    'Sales Data'[CustomerKey]
    
    )"		Measure Table
Measure	Total Orders	"
DISTINCTCOUNT(
    'Sales Data'[OrderNumber]
)"		Measure Table
Measure	Total Orders (Customer Detail)	"
IF( 
    HASONEVALUE(
        'Customer Lookup'[CustomerKey]
        ),
        [Total Orders],
        ""-"")"		Measure Table
Measure	Total Profit	"
[Total Revenue] - [Total Cost]"		Measure Table
Measure	Total Returns	"
COUNT(
    'Returns Data'[ReturnQuantity]
)"		Measure Table
Measure	Total Revenue	"
SUMX('Sales Data',
    'Sales Data'[OrderQuantity]
    *
     RELATED('Product Lookup'[ProductPrice]
    ))"		Measure Table
Measure	Total Revenue (CC)	"
SUM(
    'Sales Data'[Revenue]
)"		Measure Table
Measure	Total Revenue (Customer Detail)	"
IF(
    HASONEVALUE(
        'Customer Lookup'[CustomerKey]
    ),
    [Total Revenue],
    ""-""
)
"		Measure Table
Measure	Weekend Orders	"
CALCULATE(
    [Total Orders],
    'Calendar Lookup'[Weekend] = ""Weekend""
)"		Measure Table
Measure	YTD Revenue	"
    CALCULATE(
        [Total Revenue],
        DATESYTD(
            'Calendar Lookup'[Date]))"		Measure Table

## Insights Principales

Main Insights:

- Identification of the territories with the highest contribution to sales.
- Most profitable subcategories and products.
- Clients with the biggest impact on revenue.
- Return rate and products with the highest incidence.
- Marked seasonality in certain months

## Takeaways
The dashboard lets you:

- Analyze net sales, including returns.
- Identify key products and subcategories.
- Check performance by territory and customer.
- Spot time patterns that affect business performance.
- Make strategic decisions based on real data.

## Credits
Project developed as part of the Microsoft Power BI Desktop for Business Intelligence
by Maven Analytics (Chris Dutton & Aaron Parry)



                
