# Hotel Revenue and Guest Trends Analysis

This project aims to analyze hotel revenue trends over the years, explore the necessity of increasing parking lot sizes, and identify notable data trends using Power BI.

## Business Questions:

1. **Is our hotel revenue growing by years?**
   - Segmented revenue analysis by hotel type.
  
2. **Should we increase our parking lot size?**
   - Understanding trends in guests with personal cars.

3. **What trends can we see in the data?**
   - Focus on average daily rate (ADR) and guest trends to explore seasonality.

## Data Analysis Project Pipeline:

1. **Build a Database**
2. **Develop the SQL Query**
3. **Import the Data to Power BI**
4. **Visualize Data**
5. **Summarize Findings**

## Dataset Overview:

This project consolidates five datasets:
- `hotel_revenue_historical2018`
- `hotel_revenue_historical2019`
- `hotel_revenue_historical2020`
- `hotel_revenue_historical_market_segment`
- `hotel_revenue_historical_meal_cost`

## Data Merging:

Two methods are used to create one merged dataset:
1. Using provided SQL queries.

```My SQL Workbench
WITH hotels AS (
SELECT * FROM hotel_revenue_historical2018
UNION
SELECT * FROM hotel_revenue_historical2019
UNION
SELECT * FROM hotel_revenue_historical2020)

SELECT * FROM hotels
LEFT JOIN hotel_revenue_historical_market_segment
ON hotel_revenue_historical_market_segment.market_segment = hotels.market_segment
LEFT JOIN hotel_revenue_historical_meal_cost
ON hotel_revenue_historical_meal_cost.meal = hotels.meal;
```
2. Exporting the result to import into Power BI.


## Data Transformation:

- **Revenue Calculation:**
  - New column named 'Revenue' is created using the formula:
    `Revenue = ([stays_in_week_nights] + [stays_in_weekend_nights]) * ([adr]) * [Discount]`
- **Total Nights Measure:**
  - New measure named 'Total Nights' is created using the formula:
    `Total Nights = SUM(hotelrevenue_merged[stays_in_week_nights]) + SUM(hotelrevenue_merged[stays_in_weekend_nights])`
- **Parking Percentage Measure:**
  - New measure named 'Parking Percentage' is created using the formula:
    `Parking Percentage = SUM(hotelrevenue_merged[required_car_parking_spaces]) / [Total Nights]`

## Findings:

1. **Revenue Trend:**
   - Revenue increased from 2018 to 2019 but experienced a decline from 2019 to 2020.
2. **Parking Analysis:**
   - Parking percentage shows a steady trend, suggesting no immediate need to increase parking lot sizes.
3. **Seasonal Revenue Trends:**
   - Notable increase in revenue during summers across the analyzed years.
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")
