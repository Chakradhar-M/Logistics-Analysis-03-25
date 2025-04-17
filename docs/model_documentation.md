
## **Data Model Documentation**

The data model consists of four tables: one fact table and three dimension tables. These tables are derived from raw flat data in Power Query, providing a structured and optimized setup for analysis. The tables are linked through specific relationships that ensure consistency and allow for in-depth analysis across various dimensions. 


### **Data Model Structure:**

- **Fact Table:**
  - `fact_logistics`
  
- **Dimension Tables:**
  - `dim_origin`
  - `dim_destination`
  - `dim_route`

The tables are connected as follows:
- `fact_logistics.Origin ID` → `dim_origin.Origin ID`
- `fact_logistics.Destination ID` → `dim_destination.Destination ID`
- `fact_logistics.Route ID` → `dim_route.Route ID`

![Data Model Screenshot](https://github.com/Chakradhar-M/Logistics-Analysis-03-25/blob/main/resources/Data_Model_Screenshot.png?raw=true)


