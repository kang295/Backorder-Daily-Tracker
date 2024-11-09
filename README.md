# 📦 Automated Back-Order Parts Tracker for Supply Chain Optimization

**Description**  
This project automates the manual data aggregation and management of back-ordered parts, a critical component in supply chain stability. Effective service part management ensures optimal inventory levels, efficient warehouse space usage, and minimized storage costs. However, unexpected events—such as supply delays, demand surges, and pre-emptive bulk purchases before price increases—often lead to back orders. Addressing these promptly is essential to maintain customer satisfaction and prevent increases in return authorization rates.

Through this automated daily back-order tracking system per GBU, the team can monitor real-time back orders with detailed status updates indicating whether each part is handled or requires urgent action. The system has already reduced return authorization rates by **30%** and enhanced customer satisfaction. Integrated into a Tableau dashboard, it enables intuitive, real-time tracking, making it easy for team members to check parts status and act efficiently.

---

## ⚙️ Technologies

- **Python**: Data processing and analysis
  - **Pandas**: Data cleaning and manipulation
  - **GCSFS**: Integration with Google Cloud Storage
- **Google Cloud Platform (GCP)**: Data import and storage
- **Tableau**: Real-time dashboard visualization

---

## 📊 Dataset

The dataset used in this project is internal to the organization, containing real-time back-order, transportation, and inventory status data.

---

## ✅ Task List

1. **Obtain the current back-ordered parts list with inventory stage and ETA**
   - Includes back order hold type with no picking release date & active part status.
2. **Merge real-time transportation status of parts**
3. **Merge detailed part information** 
   - Includes model, first receipt date, and part grade.
4. **Identify accessory or BER parts**
   - As these are managed with different criteria.
5. **Merge substitute parts data with original parts**
   - Service parts may have substitute parts for flexible management.
6. **Merge demand history data**
   - Allows buyers to understand demand-related reasons behind back orders.
7. **Add new features** 
   - Including "New Part Check," "Streak," "RA history," and "Flag" (based on ETA).
8. **Import the final DataFrame to Tableau** 
   - For a user-friendly real-time tracker.
