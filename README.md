# SVC-Backorder Daily Tracker System

### 📌 Project Background
-------
The management of back-ordered service parts has historically been a labor-intensive process. Personnel were required to manually consolidate data from various Excel files and apply intricate filters to pinpoint back-ordered parts lacking proper corrective measures. This manual approach was time-consuming, prone to errors, and hindered the ability to promptly address critical part shortages. The lack of an automated system resulted in delayed identification of problematic backorders and potentially impacted service operations due to the inability to proactively manage part availability.

-------
### 🎯 Objective

The primary objective of this project is to **develop an automated system for the monitoring and analysis of back-ordered service parts**.   

This system aims to:
1. Automate Data Integration: Eliminate the manual merging of multiple Excel files by automatically integrating relevant datasets into a unified platform.
2. Intelligent Filtering: Automatically filter out back-ordered parts that have already been addressed through corrective actions such as Air shipments, Free of Charge (FOC) orders, or the presence of sufficient In Transit stock.
3. Minimize Manual Effort: Significantly reduce the manual effort required by personnel to identify and analyze critical back-ordered parts.
4. Enable Data-Driven Decision-Making: Provide readily available and filtered data to facilitate informed decision-making regarding the management of back-ordered parts.
5. Enhance Efficiency and Proactivity: Streamline the identification of critical part shortages, enabling more efficient and proactive management of essential service parts and communication with suppliers, ultimately improving service operations.

-------
### 📈 Key Features & Insights

- **Return Authorization (RA) & Supply Delay Monitoring**  
  Identify parts with a history of frequent return authorizations or delivery delays.

- **6-Month Demand Trend (Per Part)**  
  Analyze individual part demand patterns to detect abnormal behavior or anticipate restocking needs.

- **Division-Level Demand Trend (Per GBU)**  
  Aggregate demand trends by Division such as refregirator, Washing Machine, or Cooking for broader strategic insights.

- **Turnover Rate Analysis**  
  Evaluate inventory efficiency using on-hand quantity, in-transit volume, and turnover rate metrics.

- **Demand Pattern Classification**  
  Automatically classify demand trends as **Normal**, **Surge**, or **Drop** to detect potential risks.

-------
### 🔧 Tools Used
- Python (Pandas, Numpy), BigQuery, Tableau

-------
### 📁 Data Structure & Initial Checks 

* `Raw Data`: Each PIC updates the shared Excel file monthly for Rep Part, category, division, forecasted demand, RA History, and Supply Delay Status. This Excel file also includes the Rep Part Master sheet.
* `Inventory`: Part Inventory data that includes on-hand (have), in-transit (move), and open quantity (order) for each part
* `Daily BO`: Daily back order quantity lists per part
* `Supplier`: Supplier information for each part
* `Bulky Parts`: This data contains the bulky status per part

-------
### ⚙️ Process

1. **Data Extraction & Cleaning**  
   - Aggregating, joining, filtering, and dropping unnecessary fields

2. **Data Transformation**  
   - Creating new fields (e.g., turnover rate adjusted for bulky parts)  
   - Restructuring data into long-format for Tableau compatibility  
   - Detecting demand trends (Normal / Surge / Drop)

3. **Data Loading**  
   - Store processed data in a **BigQuery** table  
   - Connect BigQuery to **Tableau** for visualization

-------
### ✅ Business Impact

- Reduced **manual reporting time by over 80%** by automating the data pipeline and dashboard generation
- Enabled **weekly monitoring** of 330+ key service parts, improving visibility and early issue sensing across divisions
- Helped executives **proactively address supply chain risks** by providing timely insights

-------
### Final Dataframe Schema for Data Visualization
| Field name     | Type    | Mode     |
|----------------|---------|----------|
| rep\_part      | STRING  | NULLABLE |
| category       | STRING  | NULLABLE |
| division       | STRING  | NULLABLE |
| ra\_history\_yn | BOOLEAN | NULLABLE |
| sd\_yn         | BOOLEAN | NULLABLE |
| inventory      | INTEGER | NULLABLE |
| transit        | INTEGER | NULLABLE |
| open           | INTEGER | NULLABLE |
| BO qty         | INTEGER | NULLABLE |
| description    | STRING  | NULLABLE |
| supplier\_code | STRING  | NULLABLE |
| current\_TO    | FLOAT   | NULLABLE |
| demand\_trend  | STRING  | NULLABLE |
| bulky          | BOOLEAN | NULLABLE |
| Review         | BOOLEAN | NULLABLE |
| month          | STRING  | NULLABLE |
| demand         | INTEGER | NULLABLE |

-------
### Dashboard Preview
![Monitoring Dashboard](Key%20Parts%20Monitoring%20Dashboard.JPG)  

![Monitoring Dashboard](Key%20Parts%20Monitoring%20Filtered.JPG)
-------
### **Recommendation** 

- **Target Turnover Benchmarks per Part/Category**  
  Establish target turnover rates for each part or category to help identify gaps between current turnover and the target.
  This would allow for more precise monitoring of underperforming items and provide executives with actionable insights to improve stock movement.

- **Minimum Stock Level Status (Safety Stock)**  
  Implement minimum stock level Status for key parts. This will help assess if PICs are utilizing safety stock effectively and ensure that critical parts are not understocked during high-demand periods.

- **Part Registration Date**  
  This provides insight into whether a low current turnover rate is due to its new part status or a recent surge in demand unlike the normal period.

These additions could help executives better contextualize performance, improve inventory management, and make more informed decisions regarding procurement and replenishment strategies.
