# SQL_AIRLINES


1.
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


2.

```

SELECT airline.airline_id, airline_name, SUM (flight.delay_duration_minutes) AS total_delay_minutes
FROM airline
JOIN flight ON airline.airline_id = flight.airline_id 
GROUP BY airline.airline_id, airline_name  
ORDER BY total_delay_minutes DESC

```
<img width="545" height="411" alt="Screenshot 2025-11-06 at 10 24 49 AM" src="https://github.com/user-attachments/assets/d590ebaf-d338-4fad-acac-437ac2fcebea" />


Sunrise Airways had the highest total delay time (14,382 minutes), followed closely by Navigator Air and Sky High — suggesting these airlines may need to review operational efficiency or scheduling.
