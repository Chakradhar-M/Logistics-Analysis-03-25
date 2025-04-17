
# **Power Query Transformation Documentation**


This document outlines the data transformation process followed in Power Query to clean, normalize, and structure the raw logistics data into analytical data models. The final data model consists of a central fact table and supporting dimension tables, created from the raw dataset named `Primary Data` sourced from the Excel workbook:  `Logistics_Tracking_Dataset.xlsx`.

From the raw data, the following tables were created:

- **fact_logistics** (Fact Table)  
- **dim_origin** (Dimension Table)  
- **dim_destination** (Dimension Table)  
- **dim_route** (Dimension Table)

Each table's transformation steps are detailed below.

---

## **1. fact_logistics**

This table serves as the central fact table for analysis and contains shipment-level records with associated metadata for tracking and performance insights.

### **Transformations Applied**

1. **Source Import and Header Promotion**
   - Imported data from `Primary Data` worksheet.
   - Promoted the first row to headers.

2. **Data Type Assignment**
   - Applied appropriate data types for all columns including:
     - Dates: `Booking Date`, `Trip Start Date`, `Trip End Date`, `Planned ETA`, `Actual ETA`
     - Text: Shipment type, customer/supplier names, vehicle registration, etc.
     - Number: Distance (km), GPS coordinates

3. **Route Column Creation**
   - Created a new column `Route` by concatenating `Origin Location` and `Destination Location` using `" → "` as a separator.

4. **Removal of Redundant Columns**
   - Removed the following columns which were not required in the final fact table:
     - `Origin Location Latitude`, `Origin Location Longitude`
     - `Destination Location Latitude`, `Destination Location Longitude`
     - `Live Location`, `GPS Ping Time`, `Planned ETA`, `Actual ETA`
     - `Mobile Number`, `Minimum KM per Day`

5. **Merge with dim_origin**
   - Performed a left join with `dim_origin` on the `Origin Location` field.
   - Extracted `Origin_ID` from the joined table.
   - Removed the `Origin Location` column after the merge.

6. **Merge with dim_destination**
   - Performed a left join with `dim_destination` on `Destination Location`.
   - Extracted `Destination_ID` and removed `Destination Location`.

7. **Merge with dim_route**
   - Joined with `dim_route` using the created `Route` column.
   - Extracted `Route_ID` and dropped the `Route` column.

8. **Handling Invalid Date Ranges**
   - Identified and corrected records where `Trip End Date` was earlier than `Trip Start Date`.
   - Swapped values where necessary.
   - Created two new columns: `New Start Date` and `New End Date`.

9. **Trip Duration Calculation**
   - Created a column `Trip Duration (Hours)` as the difference in hours between `Trip End Date` and `Trip Start Date` using the corrected date columns.

10. **Cleaning Categorical Columns**
    - Replaced `"Yes"` with `"On-Time"` and `"No"` with `"Delayed"` in the `Ontime` column.
    - Standardized or removed invalid values such as `"NA"`, `"NULL"` in `Driver Name` and `Vehicle Type`.

11. **Final Column Cleanup and Renaming**
    - Renamed `New Start Date` and `New End Date` back to `Trip Start Date` and `Trip End Date`.
    - Removed intermediate columns used for transformation (e.g., `Trip Start Date`, `Trip End Date`, `Planned ETA`, `Actual ETA`).
    - Retained only relevant columns needed for analysis.

---

## **2. dim_origin**

This dimension table standardizes and uniquely identifies each origin location.

### **Transformations Applied**

1. **Column Selection**
   - Extracted the following columns:
     - `Origin Location`
     - `Origin Location Latitude`
     - `Origin Location Longitude`

2. **Remove Duplicates**
   - Removed duplicate rows based on all selected columns to ensure uniqueness.

3. **Surrogate Key Addition**
   - Added an index column starting from 1.
   - Created a new column `Origin_ID` by prefixing the index with `ORILOC` (e.g., `ORILOC001`, `ORILOC002`, etc.).

4. **Column Cleanup**
   - Removed the index column after generating the surrogate key.
   - Reordered columns as: `Origin_ID`, `Origin Location`, `Latitude`, `Longitude`.

---

## **3. dim_destination**

This dimension follows the same process as `dim_origin`, but for destination locations.

### **Transformations Applied**

1. **Column Selection**
   - Chose:
     - `Destination Location`
     - `Destination Location Latitude`
     - `Destination Location Longitude`

2. **Remove Duplicates**
   - Ensured uniqueness of destination locations by removing duplicate rows.

3. **Surrogate Key Addition**
   - Added an index column and generated `Destination_ID` using prefix `DESLOC`.

4. **Column Cleanup**
   - Removed the index column and retained the final structure:
     - `Destination_ID`, `Destination Location`, `Latitude`, `Longitude`.

---

## **4. dim_route**

This dimension captures all unique routes derived from origin and destination pairs.

### **Transformations Applied**

1. **Route Generation**
   - Extracted distinct combinations of `Origin Location` and `Destination Location` from the source data.
   - Created a `Route` column by concatenating the two locations using `" → "`.

2. **Remove Duplicates**
   - Removed any duplicate routes from the list.

3. **Surrogate Key Addition**
   - Added an index column.
   - Created `Route_ID` by prefixing the index with `ROUTE`.

4. **Final Cleanup**
   - Removed intermediate columns and retained:
     - `Route_ID`, `Route`.

---
