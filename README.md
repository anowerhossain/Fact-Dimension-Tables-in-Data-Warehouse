# Fact Table and Dimension Table 📊

In data warehousing, **Fact Tables** and **Dimension Tables** are fundamental components used to organize and analyze data efficiently.

## 1. Fact Table 📈
A **Fact Table** stores measurable, quantitative data related to business processes. It contains **numerical values (facts)** and **foreign keys** referencing related dimension tables.

### **Benefits of a Fact Table ✅**
- **Efficient Data Storage**: Stores large volumes of transactional data.
- **Supports Aggregation**: Enables SUM, AVG, COUNT, MIN, MAX operations for reporting.
- **Optimized for Analysis**: Helps in business intelligence and performance tracking.
- **Fast Query Performance**: Well-structured fact tables improve query speed when indexed properly.

### **Example: Sales Fact Table** 🛒
| Date_Key  | Product_Key | Customer_Key | Store_Key | Sales_Amount | Quantity |
|-----------|------------|--------------|-----------|--------------|----------|
| 20240101  | 101        | 5001         | 301       | 200.00       | 2        |
| 20240101  | 102        | 5002         | 302       | 150.00       | 1        |

---
## 2. Dimension Tables 📋
A **Dimension Table** stores descriptive, categorical data that provides context to the facts. Each row in a dimension table represents an attribute related to business entities.

### **Benefits of a Dimension Table ✅**
- **Enhances Data Readability**: Provides meaningful business context.
- **Reduces Data Redundancy**: Stores textual data separately from numerical facts.
- **Facilitates Filtering & Grouping**: Enables slicing and dicing data for reporting.
- **Improves Query Performance**: Helps in efficient data retrieval.

### **Example: Product Dimension Table** 🏷️
| Product_Key | Product_Name | Category     | Price  |
|------------|-------------|-------------|--------|
| 101        | Laptop      | Electronics | 1000.00 |
| 102        | Phone       | Electronics | 700.00  |

### **Example: Customer Dimension Table** 👥
| Customer_Key | Customer_Name | Location   |
|-------------|--------------|-----------|
| 5001        | John Doe     | USA       |
| 5002        | Jane Smith   | Canada    |

### **Example: Store Dimension Table** 🏬
| Store_Key | Store_Name  | City    |
|----------|------------|--------|
| 301      | Tech Hub   | New York |
| 302      | Gadget World | Toronto  |

---
## 3. How to Implement Fact and Dimension Tables 🛠️

### **Step 1: Design the Schema**
- Identify business processes requiring data analysis (e.g., Sales, Orders, Inventory).
- Determine the **facts (metrics)** and **dimensions (contextual data)**.
- Define relationships using foreign keys in the **fact table**.

### **Step 2: Create Tables in SQL**
#### **Creating a Fact Table**
```sql
CREATE TABLE Fact_Sales (
    Date_Key DATE,
    Product_Key INT,
    Customer_Key INT,
    Store_Key INT,
    Sales_Amount DECIMAL(10,2),
    Quantity INT,
    PRIMARY KEY (Date_Key, Product_Key, Customer_Key, Store_Key)
);
```

#### **Creating Dimension Tables**
```sql
CREATE TABLE Dim_Product (
    Product_Key INT PRIMARY KEY,
    Product_Name VARCHAR(100),
    Category VARCHAR(50),
    Price DECIMAL(10,2)
);

CREATE TABLE Dim_Customer (
    Customer_Key INT PRIMARY KEY,
    Customer_Name VARCHAR(100),
    Location VARCHAR(50)
);

CREATE TABLE Dim_Store (
    Store_Key INT PRIMARY KEY,
    Store_Name VARCHAR(100),
    City VARCHAR(50)
);
```

### **Step 3: Load Data**
- Use **ETL (Extract, Transform, Load)** tools to populate tables.
- Ensure **data integrity** with foreign key relationships.

### **Step 4: Query Data for Reporting**
```sql
SELECT p.Product_Name, c.Customer_Name, s.Store_Name, SUM(f.Sales_Amount) AS Total_Sales
FROM Fact_Sales f
JOIN Dim_Product p ON f.Product_Key = p.Product_Key
JOIN Dim_Customer c ON f.Customer_Key = c.Customer_Key
JOIN Dim_Store s ON f.Store_Key = s.Store_Key
GROUP BY p.Product_Name, c.Customer_Name, s.Store_Name;
```

---
## Conclusion 🎯
Fact and Dimension tables help businesses structure their data for **efficient analytics, reporting, and decision-making**. Implementing a well-designed data model ensures **scalability, performance, and accuracy** in business intelligence solutions.
