# Airbnb in Sydney data cleaning and exploratory analysis
This project use the public data from Inside Airbnb (a non-commercial website that has scraping data of Airbnb listing in some cities).
I choose Sydney dataset for this particular project with 2 datasets I have collected from 2021 and 2024 to have some comparison over time.

## Dataset overview
The dataset include 3 main csv files and 1 geojson file for map illustration:

1. **Listing data:** contains all scraped data about listings in Sydney with listing_id as primary key
2. **Reviews data**: contains all scraped available comments about listing_id with comment id as primary key and listing_id as foreign key referencing to listing table
3. **Calendar data:** contains data about the price and availability of listing in the next 365 days with listing_id as foreign key referencing to listing table

## Problem statement
What is the landscape of Airbnb listing in Sydney, Australia? What are the factors that affect the revenue of listings?

## Project outline
### Data cleaning

The data cleaning process takes the longest time for this project with a lot of back and forth for the cleaning to transform, clean, drop and extract correct data.
As the dataset is web-scraping data, it contains many outliers that create inconsistencies for analysis. The detailed mark down and notebook of data cleaning process can be find here:

**Summary of cleaning process:**

1. **Setting the requirements**:
   
   Indentify how revenue of the listing can be evaluated through the dataset:

            Revenue = Price per night * Occupancy rate (average L12Ms) * Capacity

    - The occupacny rate is determined as the percentage that the listing got booked in the L12Ms. For example, a lisiting is open for leasing 180 days per year and in the L12Ms, there were 90 days that it got booked which make the occupancy of this listing 50% (90/180)
    - The capacity is the number of days that hosts have their property for leasing. Some property may or may not be available for all year round so it depends on hosts to set their availability for leasing.
  
   Indentify the factors affect or can help to determine price, occupancy, capacity?

2. **Data cleaning:**
    
    A- Droping unecessary columns

    B- Transform data into correct format, datatype

    C- Handle outliers and missing values

    D- Draft check with calculation of some metrics

    E- Save the clean file

### Data modeling and dashboard building in Power BI:

The data model of this project contains 3 tables which are connected through the key of listing_id. 

The dashboard with interactive mode is uploaded here: [ ]

#### The estimation of occupancy in L12Ms for listing: 

This is also the hardest challenge for this project as there is no available data on how many nights each listing had been booked over the last 12 months. Hence there are several proxy measures have been taken with some key assumption as below:

1. The nights booked:
        
        Number of nights booked L12Ms = Number of booking tickets L12Ms * Number of average stay/ticket

2. The number of booking tickets is estimated throught the number of reviews last 12 months with the assumption that about 70% of guests leaving reviews after their stay

        Number of booking tickets = Number of reviews / 0.7

3. The number of nights per each stay: it is estimated that each stay will be about 3 nights, considering the fact that each listing have different number of minimum nights to book. The number of average stay will be set to minimum nights for listing that have minimum requirement higher than 3, for the rest the minimum will be 3 nights.
   
        Number of average stay = Minimum nights required (lower bound at 3)

4. For those that has 0 reviews in the last 12 months but still have booking in the next 365 days. The number of nights L12Ms will be deemed to equal to the number of nights that the listing is currenly booked in the next 90 days and accounting for the availability of each listing.

### Insights presentation:
The presentation can be found at: [ ]
