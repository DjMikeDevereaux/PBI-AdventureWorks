# PBI-AdventureWorks
Power BI Report, including chart, cards, maps, tables, sliders, parameters, narrative, tooltipdecomposition tree, key influencers

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

- **KPIs**: Total sales, net sales, returns, year-over-year growth.
- **Time trend**: Monthly sales 2020–2022.
- **Map or bars by territory**.
- **Top products and subcategories**.
- **Most important customers**.
- **Returns analysis**: return rate, revenue impact.
- **Slicers**: Year, month, territory, customer, product, subcategory.

---

## 🧮 Main DAX Measures

```DAX
Total Sales = SUM(Sales[Amount])

Total Returns = SUM(Returns[AmountReturned])

Net Sales = [Total Sales] - [Total Returns]

Grow

