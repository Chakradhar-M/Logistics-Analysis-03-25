# Logistics Analysis Data Dictionary

This table provides descriptions for each column in the logistics dataset.

| Column Name                                      | Description |
|--------------------------------------------------|-------------|
| **GpsProvider**                                  | GPS service provider tracking the vehicle. |
| **BookingID**                                    | Unique identifier for each booking. |
| **Shipment Type**                                | Indicates whether the shipment is a Market (spot booking) or Regular (contract-based) trip. |
| **BookingID_Date**                               | The date and time when the booking was created. |
| **Vehicle Registration**                         | The unique registration number of the vehicle used for transportation. |
| **Origin_Location**                              | The initial point from which the shipment starts. |
| **Destination_Location**                         | The final destination where the shipment is to be delivered. |
| **Origin_loc_latitude**                          | Latitude of the origin location. |
| **Origin_loc_longitude**                         | Longitude of the origin location. |
| **Destination_loc_latitude**                     | Latitude of the destination location. |
| **Destination_loc_longitude**                    | Longitude of the destination location. |
| **Data_Ping_time**                               | The timestamp of the last recorded GPS data ping from the vehicle. |
| **Planned_ETA**                                  | The expected time of arrival at the destination as per the trip plan. |
| **Current_Location**                             | The most recent known location of the vehicle. |
| **actual_eta**                                   | The actual time of arrival at the destination. |
| **Current_loc_latitude**                         | The latitude of the vehicle’s current location. |
| **Current_loc_longitude**                        | The longitude of the vehicle’s current location. |
| **ontime**                                       | Indicates whether the vehicle arrived on time (Yes/No). |
| **trip_start_date**                              | The actual start date and time of the trip. |
| **trip_end_date**                                | The estimated date and time of arrival. |
| **TRANSPORTATION_DISTANCE_IN_KM**               | The total distance covered by the vehicle during the trip in kilometers. |
| **vehicleType**                                  | The type of vehicle used for the shipment (e.g., 32 FT Truck, Tata Ace, Multi-Axle). |
| **Minimum_kms_to_be_covered_in_a_day**           | The minimum distance the vehicle is expected to cover in a single day. |
| **Driver_Name**                                  | The name of the driver assigned to the trip. |
| **Driver_MobileNo**                              | The contact number of the driver. |
| **customerNameCode**                             | The name of the customer receiving the shipment. |
| **supplierNameCode**                             | The name of the supplier sending the shipment. |
| **Material Shipped**                             | A description of the materials being transported in the shipment. |

