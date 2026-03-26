# Multi-Echelon Supply Chain Network Optimization

## 📌 Executive Summary
In complex supply chain networks, relying on manual routing decisions or simple heuristics often leads to inflated freight costs and warehouse bottlenecks. 

This project is a **Python-based Linear Programming (LP) model** designed to automate and optimize distribution routing. By evaluating a multi-echelon network (Plants → Ports → Customers), the model identifies the absolute lowest "Landed Cost" for fulfilling orders while strictly adhering to real-world business constraints such as daily warehouse capacities and Vendor Managed Inventory (VMI) rules.

## 🎯 The Business Problem
A global logistics network needs to route thousands of orders from 19 manufacturing plants to various destination ports. The challenge is balancing two competing cost centers:
1. **Warehousing Costs:** Varies significantly depending on the plant fulfilling the order.
2. **Freight Costs:** Varies based on the shipping lane (Origin Port to Destination Port) and weight.

Simply picking the cheapest warehouse might result in exorbitant shipping fees, and vice versa. 

## 🛠️ The Solution
I developed an optimization engine using **Pandas** for data pipeline engineering and **Pyomo** for operations research modeling. 

### 1. Data Engineering Phase
The dataset consisted of 7 disparate tables (Orders, Freight Rates, Warehouse Costs, Capacities, Product-Plant mappings, VMI Customers, and Plant-Port mappings). 
* Engineered a relational pipeline to perform sequential `inner` and `left` merges, identifying all *mathematically feasible* fulfillment paths.
* Calculated a unified **Total Landed Cost** feature: `(Weight × Freight Rate) + (Units × Storage Cost)`.
* Handled messy, real-world data artifacts (e.g., typecasting large Order IDs from scientific notation floats to standard strings, standardizing trailing spaces in API-extracted column names).

### 2. Operations Research Phase (LP Model)
* **Decision Variables:** Binary (1 if an order is assigned to a specific plant, 0 otherwise).
* **Objective Function:** Minimize the sum of the Total Landed Cost across all fulfilled orders.
* **Constraints Applied:**
  * **Absolute Fulfillment:** Every order must be assigned to exactly one capable plant.
  * **Capacity Limits:** A plant cannot process more orders than its defined daily maximum threshold.
  * **Business Logic:** VMI rules dictate that certain plants can only serve specific contracted customers.

## 💻 Tech Stack
* **Language:** Python
* **Data Manipulation:** Pandas
* **Mathematical Modeling:** Pyomo
* **Solver Engine:** CBC (Coin-or branch and cut)
* **Data Source:** [Kaggle: Supply Chain Logistics Problem](https://www.kaggle.com/datasets/anisseezzebdi/supply-chain-logistics-problem) via `kagglehub` API.

## 🚀 How to Run the Project
1. Clone this repository.
2. Ensure you have the required libraries installed:
   ```bash
   pip install pandas pyomo idaes-pse kagglehub
