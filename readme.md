# Ford GoBike System Data
<hr></hr>

## by (Hany Y Wasef)
<hr></hr>

## Dataset
<hr></hr>

>In August 2013 the Bay Area Bike Share system began operating in the San Francisco Bay Area of California. The system >allocated half of its 700 bicycle fleet in San Francisco, and the rest along the Caltrain corridor in Redwood City, Palo Alto, >Mountain View and San Jose. In 2015, it was announced that the scheme would expand to 7,000 bikes, over 2016–2017, and would >include the East Bay Area communities of Berkeley, Emeryville, and Oakland. <a href='https://en.wikipedia.org/wiki/List_of_bicycle-sharing_systems'>wikipedia.org/wiki</a> <br>
>``In this project I will focus on information about individual rides made in a bike-sharing system covering the greater San >Francisco Bay area (In February 2019).``<a href='https://video.udacity-data.com/topher/2020/October/5f91cf38_201902-fordgobike-tripdata/201902-fordgobike-tripdata.csv'>Fordgobike-Tripdata/201902</a>
<hr></hr>

## Wrangling Steps
<hr></hr>

<ul>
    <li><b>Gathering and Assessing Data</b></li>
    <li><b>Cleaning Data</b></li>
        <ul>
            <li>Delete unrequired columns
                (`stastart_station_latitude, start_station_longitude, end_station_latitude, end_station_longitude`)</li>
            <li>Missing values (`member_birth_year, member_gender`)</li>
            <li>Convert datatypes<li>
                <ul>
                    <li>Convert data type of (start_time, end_time)to (datetime)</li>
                    <li>Convert data type of (start_station_id , end_station_id, bike_id) to (str)</li>
                    <li>Convert data type of (member_birth_year) to (int) to create age column</li>
                    <li>Convert data type of (user_type, member_gender) to (category)</li>
                </ul>
            <li>Fix outlier in column (member_birth_year) replace member_birth_year from 1878 to 1978</li>
            <li>Create new columns</li> 
                <ul>
                    <li>duration_min in minutes instead of duration_sec in seconds</li>
                    <li>column for start_day and start_hour from start_time</li>
                    <li>column for member_age from member_birth_year</li>
                </ul>
        </ul>
</ul>

<hr></hr>

#### Structure of my dataset
<hr></hr>

In my new data there are 174952 individual rides made in bike-share system with 18 features that represent:
<ul>
    <li>Duration of trip [duration_sec, duration_min, start_time, end_time, start_day, end_day, start_hour, end_hour]</li>
    <li>Station info [start_station_id, start_station_name, end_station_id, end_station_name]</li>
    <li>Bike info [bike_id, bike_share_for_all_trip]</li>
    <li>User info [user_type, member_birth_year, member_gender, member_age]</li>   
</ul>

<hr></hr>

#### Feature(s) of Interest 
<ul>
    <li>The duration of trip [duration_min] is my main feature of interest.</li>
    <li>I expect that the weekdays and the hours of day [start_day, start_hour] will have effect on the duration of trip</li>
    <li>I also think that the user info [user_type, member_gender, member_age] will help find out the main target users.</li>
</ul>

<hr></hr>

## Summary of Findings
<hr></hr>

#### My Questions
<ul>
    <li><b>How long does the average trip take in minutes?</b></li>
        <ul>
           <li>I can observe that the trip duration in mintutes has a long-tailed distribution skewed to right, where the long time(more than 30 minutes) has few trips, and more than 90% of the trips have less than 1 hour long. so I use scale transformation. now I can easily interpret that a majority of users have a tendency towards using the bikes for a short-time duration trip.Most trips take between 4 to 15 minutes</li> 
        </ul>
    <li><b>When are most trips taken in weekdays?</b></li>
        <ul>
            <li>The most trips were taken on thursday while the least on saturday and sunday.</li>
        </ul>
    <li><b>When are most trips taken in terms of time of day?</b></li>
        <ul>
            <li>The most trips were taken at 5 PM and 8 AM, while the number of trips decreases after midnight.</li>
        </ul>
    <li><b>What is the most common type of bike share user? Is Male members more than females use the bike share?</b></li>
        <ul>
            <li>The Subscriber type is the most common.</li>
            <li>Male members more than females use the bike share.</li>
        </ul>
    <li><b>What is the average of members age?</b></li>
        <ul>
            <li>Most members are around 25 to 45 years old</li>
        </ul>
    <li><b>How long does the average trip take for each day of the week?</b></li>
        <ul>
            <li>All week days have short trips, except weekend (saturday and sunday) has long trips.</li>
        </ul>
    <li><b>How long is the trip in minutes per hour during the day?</b></li>
        <ul>
            <li>The most hours of the day have short trips except 2 am and 3 am have long trips.</li>
        </ul>
    <li><b>What is the trip duration in minutes according to the type of user, and the gender of members?</b></li>
        <ul>
            <li>The Customers use long trips more, while the Subscribers use shorts more.</li>
            <li>It seems that male and female members with same trip duration, no big difference between them.</li>
        </ul>
    <li><b>Is there a relationship between the age of the member and the duration of the trip?</b></li>
        <ul>
            <li>the relation between age and trip duration is negative as expected, as when the age increases, the duration of the trips                  decreases.</li>
        </ul>
    <li><b>When are most trips taken hourly during the day depending on the type of user?</b></li>
        <ul>
            <li>Subscriber of bike share clearly peaks out on typical rush hours when people go to work in the morning and getting off work                  in the afternoon, while customer of bike share tend to ride most in the afternoon or early evening. It is clear that the                    number of trips for subscribers is twice the number of trips for the customer during the day.</li>
        </ul>
    <li><b>When are most trips taken for each day of the week depending on the type of user?</b></li>
        <ul>
            <li>There was much more subscriber usage than casual customers overall. We note that the subscriber has more bike trips most                      days of the week except on weekends (Saturday, Sunday), while customers have bike trips every day of the week including                      weekend (Saturday, Sunday).</li>
        </ul>
    <li><b>Do male members use more bikes than females by user type?</b></li>
        <ul>
            <li>The Male Subscriber more than female, and also the male Customer more than the Female.</li>
        </ul>
    <li><b>How long does the average trip take for each day of the week depending on the type of user?</b></li>
        <ul>
            <li>it appears that subscribers are riding much shorter rides compared to customers every day of the week. Both types of users                    have a clear increase in trip duration on Saturdays and Sundays during the weekends, especially for regular customers. The                use of subscribers appears to be more efficient than clients in general and has maintained a very constant average duration                  from Monday to Friday.</li>
        </ul>
    <li><b>When are most trips taken hourly during the day for each day depending on the type of user?</b></li>
        <ul>
            <li>Subscribers use the system heavily on working days, ie from Monday to Friday.</li>
            <li>Customers use a bikeshare a lot on weekends(saturday,sunday), especially in the afternoon.</li>
            <li>For Subscriber Most trips concentrate around 7-9 a.m. and 4-6 p.m.</li>  
        </ul>
    <li><b>When are most trips taken hourly during the day for each day depending on the type of user and the gender of member?</b></li>
        <ul>
            <li>For customer and subscriber user the male user for both has more trips than female.</li>
        </ul>    
</ul>

<hr></hr>

## Key Insights for Presentation

- I found out  the key factor affecting trip duration is the user type.
- user type does have an impact on trip duration.
- Subscriber of bike share clearly peaks out on typical rush hours when people go to work in the morning and getting off work in the afternoon, while customer of bike share tend to ride most in the afternoon or early evening. It is clear that the number of trips for subscribers is twice the number of trips for the customer during the day.
- subscribers are riding much shorter rides compared to customers every day of the week. Both types of users have a clear increase in trip duration on Saturdays and Sundays during the weekends, especially for regular customers. The use of subscribers appears to be more efficient than clients in general and has maintained a very constant average duration from Monday to Friday.
- Subscribers use the system heavily on working days, ie from Monday to Friday.
Customers use a bikeshare a lot on weekends(saturday,sunday), especially in the afternoon.
For Subscriber Most trips concentrate around 7-9 a.m. and 4-6 p.m.

