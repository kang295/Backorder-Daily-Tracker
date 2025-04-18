# SVC-Backorder Daily Tracker System

### 📊 Default Dashboard Preview
![Monitoring Dashboard](Backorder%20Dashboard%20Default.JPG)  

### 🔍 Project Background
-------
The management of back-ordered service parts has historically been a labor-intensive process. Personnel were required to manually consolidate data from various Excel files and apply intricate filters to pinpoint back-ordered parts lacking proper corrective measures. This manual approach was time-consuming, prone to errors, and hindered the ability to promptly address critical part shortages. The lack of an automated system resulted in delayed identification of problematic backorders and potentially impacted service operations due to the inability to proactively manage part availability.

-------
### 🎯 Objective

The primary objective of this project is to **develop an automated system for the monitoring and analysis of back-ordered service parts**.   

**This system aims to**:
1. **Automate Data Integration**:
   Eliminate the manual merging of multiple Excel files by automatically integrating relevant datasets into a unified platform.
2. **Intelligent Filtering**:
   Automatically filter out back-ordered parts that have already been addressed through corrective actions such as Air shipments, Free of Charge (FOC) orders, or the presence of sufficient In Transit stock.
3. **Minimize Manual Effort**:
   Significantly reduce the manual effort required by personnel to identify and analyze critical back-ordered parts.
4. **Enable Data-Driven Decision-Making**:
   Provide readily available and filtered data to facilitate informed decision-making regarding the management of back-ordered parts.
5. **Enhance Efficiency and Proactivity**:
    Streamline the identification of critical part shortages, enabling more efficient and proactive management of essential service parts and communication with suppliers, ultimately improving service operations.

-------
### 📈 Key Features & Insights

- **Real-Time Backorder & SKU Tracking**
Provides a daily snapshot of backorders and SKU levels to monitor operational health and quickly flag urgent issues.

- **Strategic Parts Distribution Analysis**
Analyzes parts by key attributes like registration date and grade to identify new part rollout issues or importance of current situation.

- **Proactive Critical Parts Management**
Flags parts with high RA rates or frequent supply delays, enabling early intervention to minimize impact and improve customer satisfaction.

- **Demand Trend Insights from Backorder Data**
Visualizes daily backorder trends to quickly spot bottlenecks or demand spikes—helping adjust inventory before issues escalate.

- **Comprehensive Parts Overview**
Consolidates supplier info, model links, shipment type volumes, inventory levels, and recent demand to support smarter procurement and planning decisions.

-------
### 🔧 Tools Used
- Python (Pandas, Numpy), BigQuery, Tableau

-------
### 📁 Data Structure & Initial Checks 

* `Daily Backorder Report`: Daily back order quantity lists per part (Back order quantity per parts and Inventory status)
* `Original Parts Inventory`: Part Inventory data that includes open PO quantity (order) for each part by shipment category: AIR, TRK, and SEA
* `GERP Master`: Detailed information on parts such as sales model, part grade, first_receipt_date
* `Accesorries`: Accesory parts are dealt separately from regular GBU
* `BER`: Parts list that are under BER review (BER parts are reviewed separately)
* `Sub Master Inventory`: Substitute parts inventory (on-hand) quantity per original part
* `EDW Demand`: Enterprise data warehous contains demand history for each part
* `Parts RA`: RA history per parts
* `Supplier`: Supplier information for each part
* `Bulky Parts`: This data contains the bulky status per part
* `Part Category`: This contains part class code, division code, category and description

-------
### ⚙️ Process

1. **Data Extraction & Cleaning**  
   - Aggregating, joining, filtering, and dropping unnecessary fields

2. **Data Transformation**  
   - Creating new fields
     * Part Age: Determines how old the part is from its registered date (for new part checking - highest risk)
     * Streak: Count the number of orders received on specific parts within 2 weeks (14 days)
     * Category: Finding part category using division code and part class code
     * Desc: Finding part description using part class code
     * Flag: This column contains if the parts are currently back-ordered but solved within a week or two , or enough on-hand (just system error), or No ETA at all (high risk)

3. **Data Loading**  
   - Export processed data as a CSV file
   - Connect CSV file to **Tableau** for visualization

-------
### ✅ Business Impact


-------
### Final Dataframe Schema for Data Visualization

| Field name           | Type      | Mode     |
|----------------------|-----------|----------|
| Part Age             | OBJECT    | NOT NULL |
| Order Date           | DATETIME  | NOT NULL |
| Delay                | INTEGER   | NOT NULL |
| Parts No             | OBJECT    | NOT NULL |
| Parts Class Code     | OBJECT    | NOT NULL |
| Key Parts            | OBJECT    | NOT NULL |
| Functionality        | OBJECT    | NOT NULL |
| Customer             | OBJECT    | NOT NULL |
| Company Code         | OBJECT    | NOT NULL |
| Division Code        | OBJECT    | NOT NULL |
| BO                   | INTEGER   | NOT NULL |
| OH                   | INTEGER   | NOT NULL |
| IS                   | INTEGER   | NOT NULL |
| WH                   | INTEGER   | NOT NULL |
| IT                   | INTEGER   | NOT NULL |
| ETA                  | OBJECT    | NOT NULL |
| OPEN                 | FLOAT     | NULLABLE |
| AIR                  | FLOAT     | NULLABLE |
| TRK                  | FLOAT     | NULLABLE |
| SEA                  | FLOAT     | NULLABLE |
| Model                | OBJECT    | NULLABLE |
| first_receipt_date   | DATETIME  | NULLABLE |
| grade                | OBJECT    | NULLABLE |
| Sub                  | INTEGER   | NOT NULL |
| 09                   | INTEGER   | NOT NULL |
| 10                   | INTEGER   | NOT NULL |
| 11                   | INTEGER   | NOT NULL |
| 12                   | INTEGER   | NOT NULL |
| 01                   | INTEGER   | NOT NULL |
| 02                   | INTEGER   | NOT NULL |
| 03                   | INTEGER   | NOT NULL |
| Streak               | INTEGER   | NOT NULL |
| RA                   | INTEGER   | NOT NULL |
| Supplier             | OBJECT    | NULLABLE |
| Category             | OBJECT    | NOT NULL |
| Desc                 | OBJECT    | NOT NULL |
| Flag                 | OBJECT    | NOT NULL |

------
### Use case Preview
- PIC who is in charge of CVT (Cooking) Division will select division code as CVT
- Select Flag (No ETA and Flag) to only see the back ordered parts that have no upcoming ETA or quantity we order is not enough to cover back order
- Only interested in New parts (High risk) since we cannot forecast the demand afterwards
![Monitoring Dashboard](Usecase%20example.JPG)

-------
### **Recommendation** 


These additions could help executives better contextualize performance, improve inventory management, and make more informed decisions regarding procurement and replenishment strategies.
