# 🏅 Olympic Medal Data Analysis | Microsoft Azure + Power BI

This project presents an analytical solution for exploring Olympic medal data using **Microsoft Azure (Serverless SQL Pools)** and **Power BI**. The dataset is stored in Azure Data Lake and queried using `OPENROWSET`, with insights visualized through an interactive Power BI dashboard.


## 🔍 Project Overview

This solution demonstrates:
- Querying structured CSV data from Azure Data Lake using T-SQL
- Analyzing medal counts by **country**, **gender**, and **medal type**
- Computing total medals using **window functions**
- Visualizing key insights using **Power BI charts & graphs**


## 🛠️ Technologies Used

| Technology     | Purpose                                   |
|----------------|-------------------------------------------|
| Microsoft Azure | Data Storage + SQL Querying via Synapse |
| Serverless SQL (OPENROWSET) | Directly read CSV from Blob Storage |
| Power BI       | Visualizing Medal Trends and Distributions |
| T-SQL          | Data filtering, aggregation & analysis     |


## 📂 Project Structure

olympic-medal-analytics/
├── sql/
│ └── azure_medal_query.sql # Main SQL query
├── powerbi/
│ └── olympic_dashboard.pbix # (Optional) Power BI file
│ └── dashboard-screenshot.png # Dashboard preview
├── assets/
│ └── demo-video-link.txt # Link to video demo (optional)
├── sample-data-link.txt # Azure Blob CSV link
├── README.md # This file

## 📈  Query (Azure SQL)

SELECT 
    Country, 
    medal_type, 
    gender,
    COUNT(*) AS TotalRecords,
    SUM(COUNT(*)) OVER (PARTITION BY Country) AS TotalMedals
FROM 
    OPENROWSET(
        BULK 'https://hammad.dfs.core.windows.net/project2/find medals/medallists.csv',
        FORMAT = 'CSV',
        PARSER_VERSION = '2.0'
    )
    WITH (
        medal_date VARCHAR(50),
        medal_type VARCHAR(50),
        medal_code VARCHAR(50),
        name VARCHAR(255),
        gender VARCHAR(50),
        country VARCHAR(50),
        country_code VARCHAR(50),
        nationality VARCHAR(50),
        team VARCHAR(255)
    ) AS [result]
GROUP BY 
    Country, 
    medal_type, 
    gender
ORDER BY 
    Country, 
    medal_type, 
    gender;


##📊 Power BI Dashboard Preview

Dashboard contains:
Country-wise medal totals
Gender distribution
Medal type breakdown (Gold, Silver, Bronze)
Interactive slicers for exploration

##🧾 How to Use This Project

Clone or download the repository
Run sql/azure_medal_query.sql in Azure Synapse Studio
Open the .pbix file in Power BI Desktop
Customize visuals or filters as needed

##📌 Author
👨‍💻 Hammad Ali
Data Analyst | Azure & Power BI Enthusiast
