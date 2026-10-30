# Airport Data Warehouse

A data warehouse for airline flight data, built as the final project for the **Data Integration and Warehousing** course (College of Computing, Umm Al-Qura University). The project integrates three airline-related datasets into a **star schema**, loads them with an **ETL** process, and answers business questions with **SQL (MySQL)** and a dashboard.

## Project Overview

The goal is to integrate airline datasets and build a warehouse for analyzing flights, airports, passenger traffic, and airline performance.

| Source | Format | Records | Purpose |
|---|---|---|---|
| Flight Delay Data | CSV | 171,667 | Airline delay information for performance analysis |
| 2015 Flight Delays and Cancellations | CSV | 323 airports | Airport-level information for US airports |
| Air Traffic Passenger Trends (USA) 1999-2024 | CSV | 38,197 | Passenger traffic trends across US airports |

## Tools

- **MySQL / MySQL Workbench**: warehouse tables and analysis queries
- **SQL**: joins, aggregation, OLAP-style queries
- **Excel**: dashboard charts

## Star Schema

One fact table connected to three dimension tables:

- `FACT_FLIGHT`: Flight_ID (PK), Airline_ID, Airport_ID, Date_ID, Passenger_Count, arr_flights, arr_delay, arr_cancelled, arr_diverted
- `DIM_AIRLINE`: Airline_ID (PK), carrier, carrier_name
- `DIM_AIRPORT`: Airport_ID (PK), IATA_CODE, AIRPORT, CITY, STATE, COUNTRY, LATITUDE, LONGITUDE
- `DIM_DATE`: Date_ID (PK), year, month, Activity_Period


## ETL Process

- **Extract:** collected the three airline datasets (flight delays, passenger trends, delays and cancellations).
- **Transform:** data cleaning, schema matching, schema mapping, selecting relevant attributes, and organizing the data into the star schema (for example `Carrier_Name` to `Operating Airline`).
- **Load:** loaded the transformed data into `FACT_FLIGHT`, `DIM_AIRLINE`, `DIM_AIRPORT`, and `DIM_DATE`.

## Business Questions and Findings

SQL queries on the warehouse answered these questions:

| Business Question | Finding |
|---|---|
| Which airline has the highest number of flights? | Southwest Airlines |
| Which airport has the highest passenger count? | Hartsfield Jackson Atlanta International Airport |
| Which airline has the highest average delay? | Delta Air Lines |
| Which month has the highest passenger activity? | Month 1 |

Example query:

```sql
-- Which airport has the highest passenger count?
SELECT ap.AIRPORT,
       SUM(ff.Passenger_Count) AS total_passengers
FROM FACT_FLIGHT ff
JOIN DIM_AIRPORT ap
  ON ff.Airport_ID = ap.Airport_ID
GROUP BY ap.AIRPORT;
```

## Dashboard

Four visualizations: total flights by airline, total passengers by airport, average delay by airline, and monthly passenger activity.


## Key Insights

- Southwest Airlines recorded the highest number of flights among the analyzed airlines.
- Hartsfield Jackson Atlanta International Airport had the highest passenger traffic.
- Delta Air Lines showed the highest average delay.
- Passenger activity peaked in Month 1, suggesting a higher demand period.

## Recommendations

- Increase resources during periods of high passenger activity.
- Monitor airlines with high delays to improve operational performance.
- Keep updating the warehouse with new flight data.
- Use dashboard analytics to support data-driven decisions.

## Lessons Learned

- Data cleaning is essential for data quality.
- Schema matching and mapping are key for successful integration.
- ETL organizes and loads data efficiently into the warehouse.
- Star schema design improves analytical performance and reporting.

## Team

- Dana Hadi
- Shouq Aldosari
- Zahraa Alhaythami

**Instructor:** Ebtisam Alharbi

### My Contribution

I worked on the final part of the project: the star schema design and ETL documentation, the SQL implementation, the OLAP analysis of the business questions, the dashboard and key insights, and the recommendations and lessons learned.

## Repository Contents

```
airport-data-warehouse/
├── README.md
├── report/        # project report (PDF)
```
