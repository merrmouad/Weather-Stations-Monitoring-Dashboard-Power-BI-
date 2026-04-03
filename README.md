# Weather Stations Monitoring Dashboard (Power BI)

## Project Overview

This project is a **Power BI dashboard** designed to monitor and analyze the activity of weather stations worldwide.

The goal is to provide clear insights into:

* Station activity (reporting vs non-reporting)
* Data transmission performance
* Geographic distribution of stations
* Monthly evolution of station activity (focus on France)

This project follows **best practices in data modeling**, including a **Star Schema architecture** for performance and scalability.

---

## Key Features

* KPI indicators:

  * Total number of stations
  * Stations reporting data
  * Stations not reporting data
  * Data received / transmitted

* Interactive map:

  * Visualization of stations by geographic location (latitude/longitude)
  * Filtering by country

* Monthly analysis:

  * Evolution of reporting vs non-reporting stations
 

* Dynamic filters:

  * Country
  * Station name
  * Data type (Daily / Monthly)
  * Date

---

## Data Model (Star Schema)

The project is built using a **Star Schema**, ensuring high performance and clear relationships.

### Fact Table

#### `FactMeteo`

Contains all measured data:

* Date
* Station ID (`wigosid`)
* Country code (ISO3)
* Parameter (temperature, pressure, etc.)
* Value
* Type (Daily / Monthly)
* Received 
* Expected 
* Station name
* Longitude
* Latitude   
...


---

### Dimension Tables

#### `DimPays`

* Code country (ISO3)
* Country name

#### `DimDate`

* Date

#### `DimParametre`

* Weather parameters (temperature, pressure, etc.)

#### `DimType`

* Data type (Daily / Monthly)

#### `DimStation`

* Station ID (`wigosid`)
* Station name
* Country (ISO3)
* Latitude
* Longitude

---

### Schema Overview

* Fact table at the center
* Dimensions used for filtering and slicing
* One-to-many relationships (* → 1)

---

## Data Preparation

Data transformation was performed using **Power Query**:

* Unpivoting wide tables into a normalized format
* Merging multiple datasets (daily & monthly)
* Adding calculated columns:

  * Parameter
  * Type (Daily / Monthly)
* Cleaning and validating geographic coordinates

---

## DAX Measures

Key measures include:

* Total stations:

```DAX
NbStations = COUNTROWS(DimStation)
```

* Reporting stations:

```DAX
Stations_Reporting =
CALCULATE(
    DISTINCTCOUNT(FactMeteo[wigosid]),
    FactMeteo[received] <> 0
)
```

* Non-reporting stations:

```DAX
Stations_Not_Reporting =
CALCULATE(
    DISTINCTCOUNT(FactMeteo[wigosid]),
    FactMeteo[received] = 0
)
```
---

## Monthly Analysis (France)

A dedicated table (`France_Mensuel_Stations`) was created using simulated data to analyze:

* Monthly variation of station activity
* Fixed total of 175 stations
* Example:

  * March 2026 → 175 reporting / 0 non-reporting

---

## Dashboard Design

The dashboard follows a **modern SaaS-style design**:

* Clean layout with KPI cards
* Consistent color palette
* Responsive layout with clear hierarchy

---

## Technologies Used

* Power BI Desktop
* Power Query (ETL)
* DAX (Data Analysis Expressions)

---

## Future Improvements

* Integration of real-time data
* Advanced anomaly detection
* Performance optimization with larger datasets
* Deployment via Power BI Service

---

## Author

Developed as part of a **data engineering / data analytics portfolio project**.

---

## Key Takeaway

This project demonstrates:

* Data modeling using Star Schema
* Data transformation with Power Query
* Analytical reporting with Power BI
* Dashboard design best practices

---
