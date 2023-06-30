**Case Study: Cyclistic Bike Share Analysis**

**Author: @Nuzhat Shaikh** 
![cyclist](https://github.com/Shaikhnuzhat/cyclistic/blob/main/cyc.jpg)
## **About the company**
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs
## **Business Task**
The goal of this case study is to provide clear insights for designing marketing strategies aimed at converting casual riders into annual members. The expectation with me was to find out how the two riders, casual and member, use cyclistic bikes differently, and why would a casual rider buy a membership. Based on the insights the marketing team will design a marketing program.
## **The Stakeholders**
**Lily Moreno**: The director of marketing and my manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program.

**Cyclistic executive team**: A notoriously detail-oriented team which will decide whether to approve the recommended marketing program.
## **Data Exploration**
For this project, I have used **12 months** (Jan 2022 to Dec 2022) of data which is located in the [cyclistic database](https://divvy-tripdata.s3.amazonaws.com/index.html). I followed the guidelines according to the terms and conditions under [Data License Agreement](https://ride.divvybikes.com/data-license-agreement).

The data is unbiased, credible and is organized as yearly, half-yearly, quarterly, and monthly. The data is reliable, original, and current as it is internally collected and stored safely by Cyclistic. The data is also comprehensive and it contained all the information required for descriptive analysis. Personally identifiable information such as credit card numbers has been removed because of data-privacy issues.
## **Data Issues**
The attributes provided were sufficient but not complete. It could have contained gender and age information as collected in the earlier dataset (2013-2019) which would help in gaining some additional insights.
## **Data Cleaning**
Since the data is organized into 12 different worksheets, one for each month, I decided to use Microsoft Excel for monthly analysis and SQL for yearly analysis by using a union. Total number of records for the year 2022 turned out to be 5.6M which is out of scope of Microsoft Excel. For visualizing yearly statistics I used Tableau.

Steps taken for data cleaning

1) Identified the source of error in ride\_length column which turned out to be negative time values that gave !VALUE error. I rectified the problem by using the MOD() function.
1) ` `Formatted the date and time correctly
1) Removed extra spaces using the TRIM() function
1) No duplicates were found using the DISTINCT() function
1) No mismatched data was found 
1) Data aligned perfectly with the business logic

## **Data Transformation**
Next, I seperated the date and time into individual columns using the text to column wizard and formatted accordingly.

I renamed the column 'member-casual' to 'rider\_type' to specify the two rider types.

Additionally, I created 3 columns as follows:

\1) start\_day\_number: By using WEEKDAY() function on the date column

\2) start\_day: By using TEXT() function on the start\_day\_number column

\3) ride\_length: By subtracting start\_time from end\_time under the MOD() function

After performing the above mentioned steps I uploaded the 12 CSVs on the Microsoft SQL Server Management Studio and combined them using UNION ALL function in Transact-SQL.

The free public version of Tableau could not be linked to SQl, so I exported the combined 12 months data into a CSV . Although the maximum number of records a CSV can process is 1048576, but it can store any number of records. The total turned out to be 5.6M which I uploaded onto Tableau as a text file.

After cleaning and tranforming the data into a proper format it was ready for analysis.
## **Analyzing The Data**
This part of the analysis aims at discovering any surprises, trends, or relationships, and as such, I created 3 pivot tables in each of the 12 CSVs to find out how the usage of annual member riders differ from that of the casual riders **over a week**.

1. First table calculates the number of bikes leased by each rider type. The goal was to find out whether casual riders preferred certain days as compared to the member riders.
1. Second table calculates the average length of ride by each rider type. The goal here was to compare which rider type leased the bikes for longer periods on what days.
1. Third pivot table was created to determine whether casual or member riders preferred a certain bike type over others on certain days.

Grand totals of the respective pivot tables gave an idea about the total numbers over each month which was then pulled into a common pivot table for a yearly overview.
## **Sharing The Analysis**
### Ride Count
## [**https://public.tableau.com/views/RideCountDistribution/RideCount?:language=en-GB&:display_count=n&:origin=viz_share_link**](https://public.tableau.com/views/RideCountDistribution/RideCount?:language=en-GB&:display_count=n&:origin=viz_share_link)
Total bikes leased in the year 2022 were 5.66M out of which 3.34M were leased by member riders and 2.32M by casual riders. Member rides and casual rides constitute 59.03% and 40.97% of the total respectively. The fact that the number of casual riders is significant supports the idea of converting casual riders to member riders instead of focusing on adding new member riders.

<https://public.tableau.com/views/RideCountDistribution/RideCountDistribution?:language=en-GB&:display_count=n&:origin=viz_share_link>

For casual riders, the number of bikes leased starts increasing from the month of february and peaks in the month of july. After that, the ride count starts decreasing and is lowest in the month of january.

For member riders, the number of bikes leased starts increasing from the month of february and peaks in the month of august. After that, the ride count starts decreasing and is lowest in the month of january.

It is observed that the number of rides leased by casual riders surpasses member riders in the months of june, july, and august. The reason I suspect is the increase in tourism in Chicago during this period. Also, the lowest number of rides are in the month of january for both casual and member riders, the reason might be freezing weather conditions. After carefully observing the monthly data, I found out that casual riders hire maximum number of bikes on weekends and member riders on weekdays in each month consistently. From the data it seems that member riders use the bikes for commute purposes which could be office/school/college.
### Ride Length
Pic ayega excel wala chart

On average, casual riders spend approximately twice as much time on their bikes as compared to member riders, even though the number of rides leased by casual riders is 10% less than member riders.

Pic ayega chart no 2 excel ki

The average ride length for casual riders is comparable between february-may and starts declining further until january. It is observed that there is a significant increase in the average ride length for casual riders between january and february.

The average ride length for member riders is comparable between march-september and starts declining further until january. The increase in average ride length between january and february is moderate as compared to casual riders.

The average ride length for casual riders is higher than member riders throughtout the year. Also, it is observed that both casual and member riders ride for the longest periods on sundays.
### Ride Preference
<https://public.tableau.com/views/RidePreferenceCyclisticBikeShareAnalysis2022/RidePreferenceTotal?:language=en-GB&:display_count=n&:origin=viz_share_link>

Both casual and member riders prefer classic bikes as well as electric bikes more than other bike types with docked bikes being the least preferred. Interestingly, docked bikes are almost used negligibly by casual riders. The difference in classic bike usage of member and casual riders is considerable and that of electric bike usage is almost comparable.

Casual Ride Preference

<https://public.tableau.com/views/CasualRidePreference/CasualRidePreference?:language=en-GB&:display_count=n&:origin=viz_share_link>

Classic bike usage for casual riders starts increasing from february with the highest rise between may and june, and it peaks in the month of june. After that it starts declining with the largest drop between october and november

Electric bike usage for casual riders starts increasing from february with the highest rise between april and may, and it peaks in the month of august. After that it starts declining with the largest drop between october and november. Number of electric bike rides is almost comparable between june-october. Docked bikes are never used by casual riders.

On comparison, classic and electric bike usage is similar in the month of january. Casual riders have preferred classic bike throughout the year except for october, novermber, and december. During these months electric bikes are more preferred, and I suspect the reason to be the start of winter season. Usage of all bike types by both rider is the lowest in the month of January and February which are the coldest in Chicago.

Member Ride Preference

<https://public.tableau.com/views/MemberRidePreference/MemberRidePreference?:language=en-GB&:display_count=n&:origin=viz_share_link>

Classic bike usage for member riders starts increasing from february with the highest rise between March and April, and it peaks in the month of June. After that it starts declining with the largest drop between October and November. Classic bikes leased by member riders is comparable between July-September.

Electric bike usage for member riders starts increasing from february with the highest rise between May and June, and it peaks in the month of July. After that it starts declining with the largest drop between December and January. The number of electric bike rides is almost comparable between June-September. Docked bike usage for member riders start increasing in February with the highest rise in May, and it peaks in the month of June and July. After that, it starts declining. Very few member riders prefer docked bikes

Member riders have also preferred classic bikes. throughout the year except for November and December. During these months electric bikes are more preferred reason being the same. Usage of all bike types by both riders is the lowest in the month of January and February which are the coldest in Chicago.

<https://public.tableau.com/views/MemberRidePreference/BikeType?:language=en-US&:display_count=n&:origin=viz_share_link>

Upon monthly comparison, it is observed that classic and electric bikes are used by casual riders more than member riders throughout the year. Casual electric rides exceeded member electric rides between May-September.

For member riders, classic bike usage is evenly distributed between Tuesday-Saturday and electric bike usage is maximum on Friday. Both classic and electric bikes are used lowest on Sunday and Monday. For casual riders, every bike type is used maximum on Saturday.
### Casual: Weekdays Peak Hours
<https://public.tableau.com/views/weekdayspeakhoursofstarttime/WeekdaysStartTime2?:language=en-US&:display_count=n&:origin=viz_share_link>

<https://public.tableau.com/views/weedaysendtimepeakhourscasual/WeekdaysEndTime?:language=en-US&:display_count=n&:origin=viz_share_link>

Casual riders seem to be hiring maximum number of bikes in the evening between 4:00 P.M. - 7:00 P.M. during weekdays probably for leisure activities after office hours.

Member: Weekday Peak hours

<https://public.tableau.com/views/weekdaypeakhoursofstarttime/WeekdaysStartTime?:language=en-US&:display_count=n&:origin=viz_share_link>

<https://public.tableau.com/views/weekdayspeakhoursofendtimemember/WeekdaysEndTime2?:language=en-US&:display_count=n&:origin=viz_share_link>

Member riders are hiring maximum number of bikes during peak commute hours that is between 7:00 A.M. - 9:00 A.M. in the morning and between 4:00 P.M. - 6:00 P.M. in the evening. Also, member riders seem to be using the bikes to travel towards station since some of the peak cyclistic docking stations are near train stations.

Casual: Weekends Peak Hours

<https://public.tableau.com/views/weekendstarttimepeakhoursofcasual/WeekendStartTime2?:language=en-GB&:display_count=n&:origin=viz_share_link>

<https://public.tableau.com/views/weekendendtimepeakhourscasual/WeekendEndTime?:language=en-GB&:display_count=n&:origin=viz_share_link>

During weekends, casual riders hire maximum number of bikes between 12:00 P.M. - 5:00 P.M. The trend for weekends is a normal distribution unlike weekdays which was spiked during peak commute hours.

Member: Weekends Peak Hours

<https://public.tableau.com/views/weekendstarttimepeakhours/WeekendStartTime?:language=en-GB&:display_count=n&:origin=viz_share_link>

<https://public.tableau.com/views/weekendendtimemember/WeekendEndTimemember?:language=en-GB&:display_count=n&:origin=viz_share_link>

Bike hiring trend for member riders on weekends is comparable to that of casual riders, however a bit more consistent between 12:00 P.M. - 3:00 P.M. It seems that both riders types hire bikes for leisure and fun purposes during weekends.
### Recommendations
To convert casual riders into annual members, marketing campaigns should be targeted towards summer when riders are more likely to patronise Cyclistic services.

The marketing team should also consider reaching out to riders during the weekends, as casual riders are most likely using Cyclistic’s services for recreational services while annual members use it for their daily commute.

1. Design Half-Yearly and Quarter- Yearly membership plans
1. Slash the annual membership rates from June-September when casual rider traffic is maximum
1. Design flash sale of membership plans near top 20 busiest stations on weekends during peak hours






##
##
##
##
##

