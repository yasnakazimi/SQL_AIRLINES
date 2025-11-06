# SQL_airlines_Project 


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



3. 

```
SELECT passenger.passenger_id, passenger.first_name, passenger.last_name, SUM (price) AS total_amount_spent
FROM booking 
JOIN passenger on booking.passenger_id = passenger.passenger_id
GROUP BY passenger.passenger_id, passenger.first_name, passenger.last_name
ORDER BY total_amount_spent DESC
LIMIT 1;
```
<img width="664" height="72" alt="Screenshot 2025-11-06 at 10 36 52 AM" src="https://github.com/user-attachments/assets/79dc9a7e-87bb-4ece-a7f8-a215bd8c1735" />


This query identifies the highest-spending passenger based on total booking price.

4. 
```
SELECT flight_id, flight_number, COUNT(delayreason.delay_reason_id) AS delay_reason_ids
FROM flight
JOIN delayreason ON flight.delay_reason_id = delayreason.delay_reason_id
WHERE status = 'Delayed'
GROUP BY flight.flight_id, flight_number
HAVING COUNT(delayreason.delay_reason_id) = 1 


```

<img width="580" height="558" alt="Screenshot 2025-11-06 at 10 39 50 AM" src="https://github.com/user-attachments/assets/91f856d7-1103-4f94-9dfd-7b8c7113f877" />

It joins the flight table with the delayreason table to match each flight to its delay cause, then filters the results to include only flights where the status is 'Delayed'.
The results are grouped by each flight’s ID and number, and the HAVING clause ensures only flights with one delay reason are included.



5.
```
SELECT ticket_class, AVG (price) AS average_price
FROM booking
GROUP BY ticket_class
ORDER BY ticket_class
```

<img width="387" height="228" alt="Screenshot 2025-11-06 at 10 56 12 AM" src="https://github.com/user-attachments/assets/b160994e-6d0d-4751-81fe-6cdeada33109" />


This SQL query calculates the average ticket price for each ticket class (e.g., Business, Economy, First Class) from the booking table.
It groups all records by their ticket class, computes the average price per group, and then orders the results alphabetically by the ticket class.

6. 
```
SELECT flight_id, flight_number, status
FROM flight
JOIN airport ON destination_airport_id = airport_id
where NOT status = 'Cancelled' AND airport_name = 'Heathrow'
```

<img width="458" height="497" alt="Screenshot 2025-11-06 at 10 58 15 AM" src="https://github.com/user-attachments/assets/610ba433-1bf4-4872-a278-f02a2ecef936" />

This query retrieves a list of flights arriving at Heathrow Airport that have not been cancelled.
It joins data from the flight and airport tables, filters out cancelled flights, and shows the flight ID, flight number, and flight status.


7. 
```
SELECT airline.airline_id, airline_name, COUNT (*) AS number_of_flights
FROM flight
JOIN airline on flight.airline_id = airline.airline_id
GROUP BY airline.airline_id, airline.airline_name
ORDER BY number_of_flights DESC
```

<img width="515" height="415" alt="Screenshot 2025-11-06 at 11 00 35 AM" src="https://github.com/user-attachments/assets/a822b033-20e8-4d19-b2da-076acbe3c5d5" />


This SQL query finds the total number of flights operated by each airline.
It joins the flight table with the airline table using the airline ID, counts the number of flights per airline, and sorts the results from the highest to lowest number of flights.


8. 
```
SELECT airport_id, airport_name, COUNT (flight_id) AS number_of_flights
FROM airport
JOIN flight ON origin_airport_id = airport.airport_id 
GROUP BY airport_id, airport_name
ORDER BY number_of_flights DESC
```

<img width="596" height="593" alt="Screenshot 2025-11-06 at 11 01 59 AM" src="https://github.com/user-attachments/assets/45e1a41b-6b25-4805-93da-c63a831c29cf" />

This SQL query finds the airports with the highest number of departing flights.
It joins the airport table with the flight table using the origin airport ID, counts the total number of flights departing from each airport, and sorts them in descending order by flight count.


9. 
```
SELECT booking_id, price, flight_id, passenger_id
FROM booking
WHERE price =
  (SELECT MIN (price)
FROM booking)
```
<img width="586" height="137" alt="Screenshot 2025-11-06 at 11 03 53 AM" src="https://github.com/user-attachments/assets/50d4db8a-e76d-4243-b334-a15b2ac14c20" />

This SQL query retrieves the booking with the lowest price from the booking table.
It uses a subquery to find the minimum price in the entire table, then returns the booking record(s) that match that minimum value.



10. 
```
SELECT f.flight_number, f.origin_airport_id, f.destination_airport_id
FROM flight f
JOIN airport ON f.origin_airport_id = airport.airport_id
```
<img width="600" height="534" alt="Screenshot 2025-11-06 at 11 06 14 AM" src="https://github.com/user-attachments/assets/978abd94-3a7d-41ee-a6a8-757c506bfb6f" />

This SQL query retrieves details about each flight’s origin and destination airports.
It joins the flight table with the airport table to link flights to their corresponding origin airport IDs.





