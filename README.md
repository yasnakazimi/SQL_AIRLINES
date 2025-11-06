# SQL_AIRLINES



```
SELECT passenger.passenger_id, passenger.first_name, passenger.last_name, COUNT (DISTINCT airline.airline_id) AS airline_count
FROM passenger
JOIN booking ON passenger.passenger_id = booking.passenger_id
JOIN flight ON booking.flight_id = flight.flight_id
JOIN airline ON flight.airline_id = airline.airline_id 
GROUP BY passenger.passenger_id, passenger.first_name, passenger.last_name
ORDER BY airline_count DESC
Limit 15;
```
<img width="636" height="570" alt="Screenshot 2025-11-06 at 10 18 13 AM" src="https://github.com/user-attachments/assets/508e66d2-0feb-4f80-b48c-6692514fea18" />

This query returns the list of passengers who have flown with the most different airlines.
The results below show that Justin Underwood, Chase Pittman, and Jennifer Davidson each flew with 5 unique airlines — making them the most frequent and diverse travelers in the datase
