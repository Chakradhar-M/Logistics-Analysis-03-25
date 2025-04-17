
### 📊 Measures Used in the Project

| Measure Name                    | Measure Function (What it Does)                                                  | DAX Formula                                                                 |
|-----------------------------------|----------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Avg Trip Distance (Km)**       | Calculates the average transportation distance (in kilometers) for all trips    | `Avg Trip Distance (Km) = AVERAGE(fact_logistics[Transportation Distance (KM)])` |
| **Avg Trip Duration (Hours)**    | Calculates the average trip duration (in hours) for all trips                   | `Avg Trip Duration (Hours) = AVERAGE(fact_logistics[Trip Duration (Hours)])` |
| **Total Shipments**              | Counts the total number of shipments (based on Booking ID) in the dataset       | `Total Shipments = COUNT(fact_logistics[Booking ID])`                        |
