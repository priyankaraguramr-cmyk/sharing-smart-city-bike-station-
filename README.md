#Smart City Bike-Sharing - Station Performance Analysis (Power BI)
Project Title:
Analyzing Smart City Bike Sharing Data using Power BI

Project Overview:
This project analyzes real-time bike station data from a public bike-sharing system across multiple European cities. Using Power BI, raw station snapshot data (bike availability, dock capacity, station status) is cleaned, modeled into a star schema, and turned into an interactive dashboard that surfaces station performance, usage efficiency, and operational patterns across cities.

Business Objective:
●Identify the highest and lowest performing cities by average station occupancy rate.
●Track total stations, snapshot volume, and network-wide occupancy trend over time (2022–2025).
●Diagnose why specific cities show abnormally high closed-station rates.
●Use historical trend data to anticipate near-term occupancy levels.
●Recommend concrete actions (maintenance, rebalancing, benchmarking) for underperforming cities.

Dataset:
The dataset consists of continuous station-level snapshots (SnapshotID, StationID, DateKey, SnapshotTime, Hour, BikeStands, AvailableBikeStands, AvailableBikes, Status) alongside station master data (name, address, coordinates, banking/bonus flags) and city/date reference data.

Tools & Technology:
●Power BI Desktop — data import, Power Query, data modeling, DAX, visualization
●Power Query Editor — data cleaning and transformation
●DAX (Data Analysis Expressions) — calculated columns and measures
●Star Schema Data Modeling — fact and dimension tables with defined relationships

Data Model (Star Schema):
The model follows a standard star schema with one fact table at the center and three supporting dimension tables:
Table	Type	Key Fields
Fact_StationStatus	Fact	SnapshotID, StationID, DateKey, AvailableBikes, BikeStands, Status
Dim_Station	Dimension	StationID, StationName, Latitude, Longitude, CityID, Banking, Bonus
Dim_City	Dimension	CityID, City, Country
Dim_Date	Dimension	DateKey, Date, Year, Quarter, Month, DayName

Relationships:
●Dim_Station[CityID] → Dim_City[CityID]  (One-to-many, single direction)
●Fact_StationStatus[StationID] → Dim_Station[StationID]  (One-to-many, single direction)
●Fact_StationStatus[DateKey] → Dim_Date[DateKey]  (One-to-many, single direction)
Key DAX Measures & Calculated Columns
Calculated Columns:
OccupancyRate = DIVIDE(Fact_StationStatus[AvailableBikes], Fact_StationStatus[BikeStands])
StatusFlag = IF(Fact_StationStatus[Status] = "CLOSED", "Inactive", "Active")

Key Measures:
●Avg Occupancy Rate — network-wide average bike availability vs. capacity
●Closed Station Rate — % of snapshots where a station was closed
●Underperforming City Flag — flags a city as Healthy / Underperforming / Unknown based on occupancy and closure thresholds
●YoY Occupancy Change — year-over-year change in average occupancy
●Total Stations, Total Snapshots, Median Occupancy Rate, Occupancy Std Dev, Banking Station %, Total Network Capacity

Dashboard Pages:
Page	Contents
Station Performance Dashboard	KPI cards, station map, occupancy trend line (with forecast), city performance table, bar chart, city/year slicers
Analysis Report	Four-quadrant summary: Descriptive, Diagnostic, Predictive, and Prescriptive analysis of network performance

Key Insights:
●Network-wide average occupancy rate is 32.8%, with a 7.3% closed-station rate.
●Dublin, Toulouse, and Nantes are the top-performing cities (37–39% occupancy, under 1% closure).
●Cergy-Pontoise (71.1% closed) and Marseille (34.4% closed) are the most significant underperformers, pointing to an operations/maintenance issue rather than low demand.
●Namur and Rouen show moderate occupancy with elevated closure rates, suggesting partial rather than total station failure.

Recommendations:
●Prioritize station audits and maintenance in Cergy-Pontoise and Marseille.
●Rebalance bike/dock allocation in Namur and Rouen.
●Benchmark uptime practices from Dublin, Toulouse, and Nantes across the rest of the network.
●Investigate cities flagged "Unknown" to confirm whether thin data reflects a small deployment or a data-collection gap.

Repository Structure:
 SmartCityBikeSharing.pbix (Power BI project file)
 raw_dataset(Original bike station dataset)
 screenshots(Power Query, Model, DAX, Dashboard screenshots)One_Page_Report.docx / .pdf       (One-page insights summary)
 Assignment_Screenshots.pdf(Question & screenshot compiled document)
 README.md(This file)

How to Use
●Download SmartCityBikeSharing.pbix and open it in Power BI Desktop.
●Use the City and Year slicers on the dashboard to filter results.
●Navigate between the Station Performance Dashboard and Analysis Report pages using the page tabs at the bottom.
