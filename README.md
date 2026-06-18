# PBI-AdventureWorks
Power BI Report, including chart, cards, maps, tables, sliders, parameters, narrative, tooltipdecomposition tree, key influencers
# 📊 Dashboard de Ventas 2020–2022 – Power BI

Este proyecto presenta un **dashboard interactivo en Power BI** basado en datos de ventas históricas entre **2020 y 2022**, complementado con información de **territorios**, **clientes**, **productos**, **subcategorías**, **devoluciones** y una **tabla calendario** para análisis temporal avanzado.

El objetivo es ofrecer una vista clara y accionable del desempeño comercial, permitiendo identificar tendencias, variaciones estacionales, territorios clave, comportamiento de clientes y análisis de productos.

---

## 🚀 Objetivo del Proyecto

Construir un dashboard profesional que permita:

- Analizar ventas por año, mes, territorio, cliente y producto.  
- Comparar territorios y su contribución al total.  
- Evaluar el comportamiento de clientes y productos.  
- Analizar devoluciones y su impacto en ventas netas.  
- Detectar patrones estacionales y picos de demanda.  
- Facilitar decisiones estratégicas basadas en datos.

---

## 🧱 Tablas Utilizadas

### **1. Sales Data (2020–2022)**
Incluye:
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
Generada con DAX para análisis temporal:
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

### **5. Devoluciones**
Permite analizar ventas netas y comportamiento postventa:
- ID de devolución  
- Fecha  
- Producto  
- Cliente  
- Cantidad devuelta  
- Monto devuelto  

### **6. Productos**
- ID de producto  
- Nombre del producto  
- Subcategoría  
- Categoría (si aplica)  
- Precio unitario  

### **7. Subcategoría de Productos**
- ID de subcategoría  
- Nombre de subcategoría  
- Categoría asociada  

---

## 🧠 Modelado de Datos

El modelo se construyó bajo un esquema **estrella (star schema)**:

