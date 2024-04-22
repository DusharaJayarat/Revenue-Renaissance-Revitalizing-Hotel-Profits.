Revenue Renaissance: Revitalizing Hotel Profits.


## Problem Statement

Amal Grands owns multiple five-star hotels across country. They have been in the hospitality industry for the past 20 years. Due to strategic moves from other competitors and ineffective decision-making in management, Amal Grands are losing its market share and revenue in the luxury/business hotels category. As a strategic move, the managing director of Amal Grands wanted to incorporate “Business and Data Intelligence” to regain their market share and revenue. However, they do not have an in-house data analytics team to provide them with these insights.

provided with sample data and a mock-up dashboard to work

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Then go to Tranform data to expand each and every dataset.
- Step 3 : Now, duplicate the data source 4 times and in each one, expand one dataset by clicking on "Binary" option. also, rename the tables accordingly.
- Step 4 : In dim_rooms table, The column names are not captured here. We need to select "Use First Row as Headers" option .
- Step 5 : calculated column.week Num to get week number from the   corresponding date. daytype is for mean confirm it's weekday or weekend
              
            week Num = WEEKNUM(dim_date[date]).
            day type = 
            var wkd = WEEKDAY(dim_date[date],1)
            return
             IF( wkd>5,"Weekend","Weekday")


- Step 6 : Visual filters (Slicers) were added for two fields named "Filter by Room name " and "Filter by city". 

- Step 7  : two Visual filters (Slicers) were added for represent week number and month of year.

- Step 8 : Card visuals were added to the canvas for representing, 

   1.Revenue.

   2.RevPAR - Revnue Per Available Room.
 
   3.DSRN - Daily Sellable Room Night.

   4.ADR -Average Daily rate.

   5.Occupancy.

   6.Realisation.
         
- Step 9 : A donut chart categories under luxury and business categories. 
- Step 10 : Using line chart repesent trends in weekly according to occupancy, ADR,RevPAR key matrix. in order to weeks.

- Step 11 : Line and stacked column chart give the variation of realisation according to ADR.
- Step 12 : Table represent the lot of data in report , looking that table we user can directly identify revenue chnges clearly. 
- Step 13 : Calculated revenue o get the total revenue_realized

for calculate revenue following DAX expression was written;
       
        Revenue = SUM(fact_booking[revenue_realized])
        
Snap of revenue,

![Screenshot 2024-04-21 224014](https://github.com/DusharaJayarat/Power-BI-project/assets/161212159/ff3d876a-85de-46e0-aa63-ecc24c550f97)

        
- Step 14 : Calculate the RevPAR(Revenue Per Available Room)
RevPAR represents the revenue generated per available room, whether or not they are occupied. RevPAR helps hotels measure their revenue generating performance to accurately price rooms. RevPAR can help hotels measure themselves against other properties or brands.

Following DAX expression was written for the same,
        
        RevPAR = DIVIDE([Revenue],[Total Capacity])
        
A card visual was used to represent count of customers.

![revpar](https://github.com/DusharaJayarat/Power-BI-project/assets/161212159/9a20e6d6-0009-4310-917f-b30a3ec56710)

        
 - Step 15 :calculate DSRN(Daily Sellable Room Nights)

This metrics tells on average how many rooms are ready to sell for a day considering a time period

 
        DSRN = DIVIDE([Total Capacity], [No of days])
 

 
![dsrn](https://github.com/DusharaJayarat/Power-BI-project/assets/161212159/2548fcd5-8881-4cba-b5e3-7dc015a08c4a)

 
 - Step 16 : Occupancy means total successful bookings happened to the 
total rooms available(capacity)
 
 Following DAX expression was written to find occupancy%,
 
         Occupancy % = DIVIDE([Total Succesful Bookings],[Total Capacity],0)
    
 A card visual was used to represent this occupancy%.
 
 
 ![occupancy](https://github.com/DusharaJayarat/Power-BI-project/assets/161212159/04c2fbca-3ff3-4680-978a-f3b33ded5768)
 
 - Step 17 : Calculate the ADR(Average Daily rate)

It is the ratio of revenue to the total rooms booked/sold. 
It is the measure of the average paid for rooms sold in a given time period
       
        ADR = DIVIDE( [Revenue], [Total Bookings],0)
 
![ADR](https://github.com/DusharaJayarat/Power-BI-project/assets/161212159/1488d007-72e5-43a4-abe9-9d2e4712e1d4)

- Step 18 : calculate  the realisation percentage.

It is nothing but the succesful "checked out" percentage over all bookings happened.

       
       Realisation % = 1- ([Cancellation %]+[No Show rate %])
 
![realisation](https://github.com/DusharaJayarat/Power-BI-project/assets/161212159/06cf2ff1-fd39-4565-9d8c-7a8f1425c2bd)

Week-on-Week (WoW) is a type of business metric that measures changes in a specific variable 
over a period of one week compared to the previous week. It is a common way of tracking 
business performance over time and is particularly useful for analyzing trends and identifying 
areas where improvements can be made.
Here are the metrics for which we found the WoW change% in this dashboard:

1. Revenue WoW change %: To get the revenue change percentage week over week.
2. Occupancy WoW change %: To get the occupancy change percentage week over week.
3. ADR WoW change %: To get the ADR (Average Daily rate) change percentage week over week.
4. RevPAR WoW change %: To get the RevPAR (Revenue Per Available Room) change percentage week over week.
5. Realisation WoW change %: To get the Realisation change percentage week over week.
6. DSRN WoW change %: To get the DSRN (Daily Sellable Room Nights) change percentage 
week over week.

understand WoW change% for Revenue metric as an example:

        Revenue WoW change % = 
        Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVAL(dim_date[wn]),MAX(dim_date[wn]))
        var revcw = CALCULATE([Revenue],dim_date[wn]= selv)
        var revpw =  CALCULATE([Revenue],FILTER(ALL(dim_date),          
        dim_date[wn]= selv-1))

        return
        DIVIDE(revcw,revpw,0)-1

 
 # Snapshot(Power BI )

 
![db](https://github.com/DusharaJayarat/Power-BI-project/assets/161212159/925b02bf-e512-4a2d-83c2-bbacf0537b11)

