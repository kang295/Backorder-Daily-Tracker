# SVC-Backorder Daily Tracker System

## ✨**Dashboard Preview**
![Monitoring Dashboard](Backorder%20Dashboard%20Default.JPG)  

## 💬 **Project Background**
-------
In service operations, resolving back-orders and ensuring timely delivery of service parts are critical performance metrics. However, I discovered that managing back-ordered parts was largely manual—relying on time-consuming data consolidation from multiple Excel files and complex filtering to identify unresolved issues. This process not only delayed response times but also introduced errors, limiting the team’s ability to proactively manage part shortages and maintain service quality.

-------
## 📝 **Objective**

To develop an automated system that streamlines the monitoring and analysis of back-ordered service parts by filtering out already addressed or in-transit items—eliminating manual, repetitive tasks, reducing human error, and enabling the team to operate more efficiently through immediate identification and resolution of critical shortages.

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
## 📈 Key Features & Insights

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
## 🛠️ Tools Used
- Python (Pandas, Numpy), BigQuery (GCP), Tableau

-------
## 📁 Datasets Used

* `Daily Backorder Report`: Daily back order quantity lists per part (Back order quantity per parts and Inventory status)
* `Original Parts Inventory`: Part Inventory data that includes open PO quantity (order) for each part by shipment category: AIR, TRK, and SEA
* `GERP Master`: Detailed information on parts such as sales model, part grade, first_receipt_date
* `Accesorries`: Accesory parts are dealt separately from regular GBU
* `BER`: Parts list that are under BER review (BER parts are reviewed separately)
* `Sub Master Inventory`: Substitute parts inventory (on-hand) quantity per original part
* `EDW Demand`: Enterprise data warehous contains demand history for each part
* `Parts RA`: RA history per parts
* `Supplier`: Supplier information for each part
* `Part Category`: This contains part class code, division code, category and description

-------
## ⚙️ Process

1. **Data Extraction & Cleaning using Python (Pandas)**  
   - Aggregating, joining, filtering, and dropping unnecessary fields

2. **Data Transformation using Python Programming**  
   - Creating new fields
     * Part Age: Determines how old the part is from its registered date (for new part checking - highest risk)
     * Streak: Count the number of orders received on specific parts within 2 weeks (14 days)
     * Category: Finding part category using division code and part class code
     * Desc: Finding part description using part class code
     * Flag: This column contains if the parts are currently back-ordered but solved within a week or two , or enough on-hand (just system error), or No ETA at all (high risk)

3. **Data Loading from BigQuery to Tableau**  
   - Export processed data as a CSV file and update Big Query database as notebook runs the code
   - Connect GCP database to **Tableau** for visualization

-------
## ✅ Business Impact

1. Automated data processing and reduced daily manual work by 30+ minutes per team member and eliminated errors from Excel-based tasks.

2. Developed a real-time dashboard enabling leadership to track back-order issues and monitor resolution ownership with just a few clicks.

3. Enhanced customer satisfaction by streamlining part delivery, resulting in a 25% reduction in Return Authorization requests.

-------
## Final Dataframe Schema for Data Visualization

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
| 10                   | INTEGER   | NOT NULL |
| 11                   | INTEGER   | NOT NULL |
| 12                   | INTEGER   | NOT NULL |
| 01                   | INTEGER   | NOT NULL |
| 02                   | INTEGER   | NOT NULL |
| 03                   | INTEGER   | NOT NULL |
| 04                   | INTEGER   | NOT NULL |
| Streak               | INTEGER   | NOT NULL |
| RA                   | INTEGER   | NOT NULL |
| Supplier             | OBJECT    | NULLABLE |
| Category             | OBJECT    | NOT NULL |
| Desc                 | OBJECT    | NOT NULL |
| Flag                 | OBJECT    | NOT NULL |

------
## 💡 **Use Case Scenario: Customized Backorder Monitoring**

![Monitoring Dashboard](Usecase%20example.JPG)

1. A supply planner responsible for CVT, DVT, and CDT divisions was unable to manage backorders for the past 4 days.

2. Set the date range to April 26–30 and filtered by Division Code for CVT, DVT, and EVT.

3. Since all suppliers except China and Korea are on holiday during that period, filtered the data to show only backorders supplied from China and Korea.

4. Applied flag filter to display items that either have no ETA or have backorder quantities exceeding expected shipping volume.

5. The result showed 103 backorder cases across 29 unique parts, with many being A-grade items—indicating high customer demand or potential Return Authorization (RA) risk.

6. This quick, customized dashboard enables immediate visibility into critical issues and serves as a practical tool for supplier communication and issue resolution.
