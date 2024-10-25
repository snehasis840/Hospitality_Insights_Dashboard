# Project Overview: Revenue Insights Dashboard for a Hotel Chain

## Objective:
The objective of this project is to analyze and visualize revenue data across multiple hotel locations in India, empowering the hotel chain to make informed, data-driven decisions to enhance revenue performance, identify key trends, and optimize occupancy strategies.

## Scope of Work:
The project involved gathering, transforming, and analyzing booking and revenue data from various hotel locations across India. Key insights are generated through Power BI to provide a centralized dashboard view of performance metrics and trends, catering to stakeholders' needs for real-time, actionable insights.
## Data Modelling
## Measures:
- 	Revenue:	To get the total revenue_realized
- 	Total Bookings:	To get the total number of bookings happened
-  Total Capacity:	To get the total capacity of rooms present in hotels
- 	Total Succesful Bookings:	To get the total succesful bookings happened for all hotels	
- 	Occupancy %:	Occupancy means total successful bookings happened to the 
total rooms available(capacity)		
-	Average Rating:	Get the average ratings given by the customers		
-	No of days:	To get the total number of days present in the data
-	Total cancelled bookings:	To get the"Cancelled" bookings out of all Total bookings happened		
- Cancellation %:	calculating the cancellaton percentage
- Total Checked Out:	To get the successful 'Checked out' bookings out of all Total bookings happened		
- Booking % by Platform:	To show the percentage contribution of each booking platform for bookings in hotels
- Booking % by Room class: 	To show the percentage contribution of each room class
over total rooms booked
- ADR:  Calculate the ADR(Average Daily rate). 
It is the measure of the average paid for rooms sold in a given time period
- Realisation %:	calculate  succesful ""checked out"" percentage over all bookings happened.
- RevPAR:	Calculate the revenue generated per available room, whether or not they are occupied. RevPAR helps hotels measure their revenue generating performance to accurately price rooms. RevPAR can help hotels measure themselves against other properties or brands.	

- 	DBRN: calculate DBRN(Daily Booked Room Nights). 
This metrics tells on average how many rooms are booked for a day considering a time period
- 	DSRN: 	calculate DSRN(Daily Sellable Room Nights). 
This metrics tells on average how many rooms are ready to sell for a day considering a time period
- DURN:	calculate DURN(Daily Utilized Room Nights). 
This metric tells on average how many rooms are succesfully utilized by customers for a day considering a time period
- Revenue WoW change %:	To get the revenue change percentage week over week
-	Occupancy WoW change %:	To get the occupancy change percentage week over week
- ADR WoW change %: To get the ADR(Average Daily rate) change percentage week over week
- Revpar WoW change %:	To get the RevPar(Revenue Per Available Room) change percentage week over week
- Realisation WoW change %:	To get the Realisation change percentage week over week

  
## DAX Function: 
- Revenue = SUM(fact_bookings[revenue_realized])
- Total Bookings = COUNT(fact_bookings[booking_id])	fact_bookings
- Total Capacity = SUM(fact_aggregated_bookings[capacity])
- Total Succesful Bookings = SUM(fact_aggregated_bookings[successful_bookings])
- Occupancy % = DIVIDE([Total Succesful Bookings],[Total Capacity],0)
- Average Rating = AVERAGE(fact_bookings[ratings_given])
- No of days = DATEDIFF(MIN(dim_date[date]),MAX(dim_date[date]),DAY) +1	
- Total cancelled bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="Cancelled")
- Cancellation % = DIVIDE([Total cancelled bookings],[Total Bookings])
- Total Checked Out = CALCULATE([Total Bookings],fact_bookings[booking_status]="Checked Out")
- Booking % by Platform = DIVIDE([Total Bookings],
 CALCULATE([Total Bookings], 
 ALL(fact_bookings[booking_platform])
  ))*100"
- Booking % by Room class = DIVIDE([Total Bookings],
 CALCULATE([Total Bookings], 
 ALL(dim_rooms[room_class])
  ))*100
- ADR = DIVIDE( [Revenue], [Total Bookings],0)
- Realisation % = 1- ([Cancellation %]+[No Show rate %])
- RevPAR = DIVIDE([Revenue],[Total Capacity])
- DBRN = DIVIDE([Total Bookings], [No of days]
- DSRN = DIVIDE([Total Capacity], [No of days])
- DURN = DIVIDE([Total Checked Out],[No of days])
- Revenue WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Revenue],dim_date[wn]= selv)
var revpw =  CALCULATE([Revenue],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
return
DIVIDE(revcw,revpw,0)-1
- Occupancy WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Occupancy %],dim_date[wn]= selv)
var revpw =  CALCULATE([Occupancy %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
return
DIVIDE(revcw,revpw,0)-1
- ADR WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([ADR],dim_date[wn]= selv)
var revpw =  CALCULATE([ADR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
return
DIVIDE(revcw,revpw,0)-1
- Revpar WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([RevPAR],dim_date[wn]= selv)
var revpw =  CALCULATE([RevPAR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
return
DIVIDE(revcw,revpw,0)-1
- Realisation WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Realisation %],dim_date[wn]= selv)
var revpw =  CALCULATE([Realisation %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
return
DIVIDE(revcw,revpw,0)-1




## Insights:
- Mumbai generates the highest revenue (669 M) followed by Bangalore, Hyderabad and Delhi
- AtliQ Exotica performs better compared to all 7 type of properties with 320 Million revenue, rating 3.62, occupancy percentage 57 and cancellation rate as 24.4%.
- AtliQ Bay has the highest occupancy of 66%
- Week 24 recorded the highest revenue among all, which is 139.6 Million
- Delhi tops both in occupancy and rating followed by Hyderabad, Mumbai, Bangalore
- AtliQ lost around 298 Million in cancellation
- Elite type rooms has the most booking and as well higher cancellation rate
