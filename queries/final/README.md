

-- 1.1 Previewing the first 100 records to understand the column schema and data structure
SELECT TOP 100 * 
FROM road_accident;

-- 1.2 Verifying the total row count after ingestion (Should be around 307,000 rows)
SELECT COUNT(*) AS total_records 
FROM road_accident;


-- =================================================================================
-- SECTION 2: PRIMARY KPIs (Current Year 2022 vs Previous Year 2021)
-- =================================================================================

-- 2.1 CY Casualties (Current Year - 2022)
-- Target Dashboard Value: 195,737
SELECT SUM(number_of_casualties) AS CY_Casualties
FROM road_accident
WHERE YEAR(accident_date) = 2022;

-- 2.2 PY Casualties (Previous Year - 2021)
-- Target Dashboard Value: 222,146
SELECT SUM(number_of_casualties) AS PY_Casualties
FROM road_accident
WHERE YEAR(accident_date) = 2021;

-- 2.3 Year-over-Year (YoY) Growth Percentage of Casualties
-- Target Dashboard Value: -11.9%
SELECT 
    CY.CY_Casualties,
    PY.PY_Casualties,
    CAST(((CY.CY_Casualties - PY.PY_Casualties) * 100.0) / PY.PY_Casualties AS DECIMAL(10, 2)) AS YoY_Casualties_Growth_PCT
FROM 
    (SELECT SUM(number_of_casualties) AS CY_Casualties FROM road_accident WHERE YEAR(accident_date) = 2022) CY,
    (SELECT SUM(number_of_casualties) AS PY_Casualties FROM road_accident WHERE YEAR(accident_date) = 2021) PY;

-- 2.4 CY Accidents Count (Current Year - 2022)
-- Target Dashboard Value: 144,419
SELECT COUNT(DISTINCT accident_index) AS CY_Accidents_Count
FROM road_accident
WHERE YEAR(accident_date) = 2022;

-- 2.5 PY Accidents Count (Previous Year - 2021)
-- Target Dashboard Value: 163,554
SELECT COUNT(DISTINCT accident_index) AS PY_Accidents_Count
FROM road_accident
WHERE YEAR(accident_date) = 2021;

-- 2.6 Year-over-Year (YoY) Growth Percentage of Accidents
-- Target Dashboard Value: -11.7%
SELECT 
    CY.CY_Accidents_Count,
    PY.PY_Accidents_Count,
    CAST(((CY.CY_Accidents_Count - PY.PY_Accidents_Count) * 100.0) / PY.PY_Accidents_Count AS DECIMAL(10, 2)) AS YoY_Accidents_Growth_PCT
FROM 
    (SELECT COUNT(DISTINCT accident_index) AS CY_Accidents_Count FROM road_accident WHERE YEAR(accident_date) = 2022) CY,
    (SELECT COUNT(DISTINCT accident_index) AS PY_Accidents_Count FROM road_accident WHERE YEAR(accident_date) = 2021) PY;


-- =================================================================================
-- SECTION 3: CASUALTIES BY ACCIDENT SEVERITY (Current Year - 2022)
-- =================================================================================

-- 3.1 CY Fatal Casualties (2022)
-- Target Dashboard Value: 2,855 (YoY: -33.1%)
SELECT SUM(number_of_casualties) AS CY_Fatal_Casualties
FROM road_accident
WHERE accident_severity = 'Fatal' AND YEAR(accident_date) = 2022;

-- 3.2 CY Serious Casualties (2022)
-- Target Dashboard Value: 27,045 (YoY: -16.0%)
SELECT SUM(number_of_casualties) AS CY_Serious_Casualties
FROM road_accident
WHERE accident_severity = 'Serious' AND YEAR(accident_date) = 2022;

-- 3.3 CY Slight Casualties (2022)
-- Target Dashboard Value: 165,837 (YoY: -10.8%)
SELECT SUM(number_of_casualties) AS CY_Slight_Casualties
FROM road_accident
WHERE accident_severity = 'Slight' AND YEAR(accident_date) = 2022;

-- 3.4 Percentage of Total Casualties by Severity for CY (2022)
SELECT 
    accident_severity,
    SUM(number_of_casualties) AS casualties_count,
    CAST(SUM(number_of_casualties) * 100.0 / 
        (SELECT SUM(number_of_casualties) FROM road_accident WHERE YEAR(accident_date) = 2022) 
        AS DECIMAL(10, 2)) AS percentage_of_total
FROM road_accident
WHERE YEAR(accident_date) = 2022
GROUP BY accident_severity;


-- =================================================================================
-- SECTION 4: SECONDARY KPIs - CASUALTIES BY VEHICLE GROUP (Current Year - 2022)
-- =================================================================================
-- Grouping 15+ vehicle types into 6 main classes: Bike, Car, Bus, Van, Agricultural, Others
SELECT 
    CASE 
        WHEN vehicle_type IN ('Agricultural vehicle', 'Agricultural Locomotive', 'Agricultural Tractor') THEN 'Agricultural'
        WHEN vehicle_type IN ('Car', 'Taxi', 'Private hire car') THEN 'Car'
        WHEN vehicle_type IN ('Motorcycle 50cc and under', 'Motorcycle 125cc', 'Motorcycle over 125cc and up to 500cc', 'Motorcycle over 500cc', 'Pedal cycle') THEN 'Bike'
        WHEN vehicle_type IN ('Bus or coach (17 or more seats)', 'Minibus (8 - 16 seats)') THEN 'Bus'
        WHEN vehicle_type IN ('Goods 7.5 tonnes mgw and over', 'Goods over 3.5t. and under 7.5t', 'Van / Goods 3.5 tonnes mgw or under') THEN 'Van'
        ELSE 'Others'
    END AS vehicle_group,
    SUM(number_of_casualties) AS CY_Casualties
FROM road_accident
WHERE YEAR(accident_date) = 2022
GROUP BY 
    CASE 
        WHEN vehicle_type IN ('Agricultural vehicle', 'Agricultural Locomotive', 'Agricultural Tractor') THEN 'Agricultural'
        WHEN vehicle_type IN ('Car', 'Taxi', 'Private hire car') THEN 'Car'
        WHEN vehicle_type IN ('Motorcycle 50cc and under', 'Motorcycle 125cc', 'Motorcycle over 125cc and up to 500cc', 'Motorcycle over 500cc', 'Pedal cycle') THEN 'Bike'
        WHEN vehicle_type IN ('Bus or coach (17 or more seats)', 'Minibus (8 - 16 seats)') THEN 'Bus'
        WHEN vehicle_type IN ('Goods 7.5 tonnes mgw and over', 'Goods over 3.5t. and under 7.5t', 'Van / Goods 3.5 tonnes mgw or under') THEN 'Van'
        ELSE 'Others'
    END
ORDER BY CY_Casualties DESC;


-- =================================================================================
-- SECTION 5: TRENDS ANALYSIS (Current Year vs Previous Year Monthly Trend)
-- =================================================================================

-- 5.1 Monthly Trend Comparison (CY 2022 vs PY 2021)
-- Sorted chronologically from January to December
SELECT 
    DATENAME(MONTH, accident_date) AS month_name,
    MONTH(accident_date) AS month_number,
    SUM(CASE WHEN YEAR(accident_date) = 2022 THEN number_of_casualties ELSE 0 END) AS CY_Casualties,
    SUM(CASE WHEN YEAR(accident_date) = 2021 THEN number_of_casualties ELSE 0 END) AS PY_Casualties
FROM road_accident
GROUP BY DATENAME(MONTH, accident_date), MONTH(accident_date)
ORDER BY month_number;


-- =================================================================================
-- SECTION 6: ROAD TYPE & ENVIRONMENTAL FACTORS
-- =================================================================================

-- 6.1 Casualties by Road Type (CY 2022)
SELECT 
    road_type,
    SUM(number_of_casualties) AS CY_Casualties
FROM road_accident
WHERE YEAR(accident_date) = 2022
GROUP BY road_type
ORDER BY CY_Casualties DESC;

-- 6.2 Casualties and Percentage by Urban or Rural Area (CY 2022)
-- Urban: ~61.90% | Rural: ~38.10%
SELECT 
    urban_or_rural_area,
    SUM(number_of_casualties) AS CY_Casualties,
    CAST(SUM(number_of_casualties) * 100.0 / 
        (SELECT SUM(number_of_casualties) FROM road_accident WHERE YEAR(accident_date) = 2022) 
        AS DECIMAL(10, 2)) AS percentage_of_total
FROM road_accident
WHERE YEAR(accident_date) = 2022
GROUP BY urban_or_rural_area;

-- 6.3 Casualties by Light Condition Group (Day vs Night) for CY 2022
-- Day: ~73.84% | Night: ~26.16%
SELECT 
    CASE 
        WHEN light_conditions IN ('Daylight') THEN 'Day'
        WHEN light_conditions IN ('Darkness - lights lit', 'Darkness - lights unlit', 'Darkness - no lighting', 'Darkness - lighting unknown') THEN 'Night'
        ELSE 'Unknown'
    END AS light_condition_group,
    SUM(number_of_casualties) AS CY_Casualties,
    CAST(SUM(number_of_casualties) * 100.0 / 
        (SELECT SUM(number_of_casualties) FROM road_accident WHERE YEAR(accident_date) = 2022) 
        AS DECIMAL(10, 2)) AS percentage_of_total
FROM road_accident
WHERE YEAR(accident_date) = 2022
GROUP BY 
    CASE 
        WHEN light_conditions IN ('Daylight') THEN 'Day'
        WHEN light_conditions IN ('Darkness - lights lit', 'Darkness - lights unlit', 'Darkness - no lighting', 'Darkness - lighting unknown') THEN 'Night'
        ELSE 'Unknown'
    END;


-- =================================================================================
-- SECTION 7: GEOGRAPHICAL HOTSPOTS (TOP 10 LOCAL AUTHORITIES)
-- =================================================================================

-- 7.1 Top 10 Locations with Highest Number of Casualties (All-Time Cumulative)
-- Leader: Birmingham (~8,574)
SELECT TOP 10 
    local_authority,
    SUM(number_of_casualties) AS total_casualties
FROM road_accident
GROUP BY local_authority
ORDER BY total_casualties DESC;
