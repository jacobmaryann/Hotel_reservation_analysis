# Hotel_reservation_analysis
Analyzing dataset using SQL queries


CREATE TABLE HOTEL_DETAILS(
Booking_ID VARCHAR(20),
no_of_adults INT,
no_of_children INT,
no_of_weekend_nights INT,
no_of_week_nights INT,	
type_of_meal_plan VARCHAR	(20),
room_type_reserved	VARCHAR(20),
lead_time INT,
year INT,
month VARCHAR,
arrival_date DATE,
market_segment_type	VARCHAR(20),
avg_price_per_room	FLOAT,
booking_status VARCHAR(20)
);

SHOW datestyle; -- ISO, MDY
SET datestyle = "ISO, DMY";
ALTER DATABASE "HOTEL RESERVATION" SET datestyle TO "ISO, DMY";

-- QUESTION 1
SELECT * FROM HOTEL_DETAils
select distinct(count( booking_id))as Total_reservation from hotel_details

-- QUESTION 2
select type_of_meal_plan,
count(type_of_meal_plan) as most_popular_meal_plan from hotel_details
group by type_of_meal_plan 
order by most_popular_meal_plan desc
limit 1

--QUESTION 3
SELECT round(avg(AVG_PRICE_PER_ROOM)) AS avg_price_involving_children FROM HOTEL_DETAILS
where no_of_children > 0

-- QUESTION 4
SELECT count(arrival_date) AS reservations_for_2018 from hotel_details
where YEAR = '2018'

--QUESTION 5
select room_type_reserved,
count(room_type_reserved) as most_commonly_booked_room from hotel_details
group by room_type_reserved 
order by most_commonly_booked_room desc
limit 1

--QUESTION 6
SELECT COUNT(no_of_weekend_nights) AS TOTAL_reservations_on_a_weekend FROM hotel_details
where no_of_weekend_nights > 0

--QUESTION 7
SELECT MAX(lead_time) AS highest_lead_time, MIN(lead_time) 
AS lowest_lead_time from hotel_details

--QUESTION 8
select market_segment_type,
count(market_segment_type) as most_common_market_segment_type from hotel_details
group by market_segment_type 
order by most_common_market_segment_type desc
limit 1

--QUESTION 9
SELECT COUNT(booking_status) AS booking_confirmed FROM hotel_details
WHERE booking_status = 'Not_Canceled'

--QUESTION 10
SELECT SUM(no_of_adults) AS total_adults, SUM(no_of_children) AS Total_children
from hotel_details

--QUESTION 11
SELECT AVG(no_of_weekend_nights) AS avg_weekend_nights_involving_children from hotel_details
where no_of_children > 0

--QUESTION 12
select month, count(booking_id) as total_reservations_2017
 from hotel_details
 where year ='2017'
 group by month

-- QUESTION 13
SELECT room_type_reserved as room_type, round(AVG(no_of_weekend_nights + no_of_week_nights)) as avg_nights_spent_by_guests from hotel_details
group by room_type_reserved

-- QUESTION 14
SELECT ROOM_type_reserved as common_room_type_involving_children, round(avg(avg_price_per_room)) AS AVG_PRICE_PER_ROOM from hotel_details
where no_of_children >0
group by room_type_reserved

-- QUESTION 15
SELECT market_segment_type, round(sum(avg_price_per_room)) as highest_price_per_room from hotel_details
group by market_segment_type
