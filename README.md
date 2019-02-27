# AML-Pump-It-Up

# Advanced Machine Learning - Data Mining the water table(Tips):

## Dataset Description
- Total Number of attributes: 39 + 1(id)
- Number of training set: 59400
- Number of test set: 14850
- Class labels: Functional / Functional but need repair / Non-functional

**List of 39 attributes:**
1. amount_tsh: Amount of water available to the waterpoint.
2. date_recorded: Date of entry.
3. funder: Person who funded the well.
4. gps_height: Altitude of the well.
5. installer: Organization that installed the well.
6. longitude: GPS Longitudinal coordinate.
7. latitude: GPS Latitudinal coordinate.
8. wpt_name: Name of the waterpoint.
9. num_private: Private number.
10. basin: Geographic water basin.
11. subvillage: Geographic location.
12. region: Geographic location.
13. region_code: Geographic location code.
14. district_code: Geographic location code.
15. lga: Geographic location.
16. ward: Geographic location.
17. population: Population around the well.
18. public_meeting: True/False.
19. recorded_by: Person entering the data.
20. scheme_management: One who operates the waterpoint.
21. scheme_name: Who operates the waterpoint.
22. permit: If a permit exists for the waterpoint or not.
23. construction_year: Year of construction of the waterpoint.
24. extraction_type: Kind of extraction that the waterpoint uses.
25. extraction_type_group: Kind of extraction that the waterpoint uses.
26. extraction_type_class: Kind of extraction that the waterpoint uses.
27. management: How the waterpoint is managed.
28. management_group: How the waterpoint is managed.
29. payment: What the water costs.
30. payment_type: What the water costs.
31. water_quality: Quality of the water.
32. quality_group: The quality of the water.
33. quantity: The quantity of water.
34. quantity_group: The quantity of water.
35. source: Source of water.
36. source_type: The source of water.
37. source_class: The source of water.
38. waterpoint_type: The kind of waterpoint.
39. waterpoint_type_group: The kind of waterpoint.

**There are lots of redundant attributes.**
------

## Data Cleaning
### 1. Null values

|feature|# null|
|-------|------|
|funder|3635|
|installer|3655|
|subvillage|371|
|public_meeting|3334|
|scheme_management|3877|
|scheme_name|28166|
|permit|3056|

### 2. Drop redundant columns
**The attributes we keep initially:**
```python=
['id', 'amount_tsh', 'funder', 'gps_height',
       'installer', 'wpt_name', 'num_private',
       'basin', 'subvillage', 'region', 'region_code', 'district_code', 'lga',
       'ward', 'population', 'public_meeting', 'recorded_by',
       'scheme_management', 'permit', 'construction_year',
       'extraction_type_class', 'management_group', 'payment_type',
       'water_quality', 'quantity', 'source_class', 'waterpoint_type_group',
       'status_group']
```
The reason of removing:
- `longitude, latitude`: geographical data
- `scheme_name`: too many null value
- `extraction_type, extraction_type_group, management, payment, quality_group, quantity_group, source, source_type, waterpoint_type`: redundant

### 3. Explore the data "one by one" and transform them into categorial data
- `status_group`: Most of the wells are functional, only a little need repair, the quatity of non-functional wells is not small.
- `longitude, latitude`: Missing value. Drop these two columns.
- `date_recorded`: Transform it into `days_since_recorded`.
- `funder`: Remain top 5 + other.
- `installer`: Remain top 5 + other.
- `gps_height`: Temporially remain.
- `wpt_name`: No predictive pover, remove.
- `num_private`: Do not know the meaning of it, remove.
- `status_group`: No missing values, 9 categories.
- `subvillage`: No dominant values, remove
- `region`: No missing value, 21 categories, keep.
- `region_code, district_code`: We already had region that represents the geographical information. Remove this feature.
- `population`: Very skewed data. Need to be transformed.***uncompleted***.
- `amount_tsh`: Very skewed data. Need to be transformed.***uncompleted***.
- `public_meeting`: Replace NA by `unknown`, cause there are only 3334 null values among 59400 items.
- `recorded_by`: All the value in this columns are the same, drop it.
- `scheme_management`: Keep top 5 + other
- `permit`: Replace NA by `unknown`
-  `construction_year`:`'60s','70s','80s','90s','00s','10s','unknown'`
- `extraction_type_class`: No missing value.7 categories.
- `management_group`: Very skewed data.***How?***
- `payment_type`: 7 categories. 8157 unknow.
- `water_quality`: 8 categories. 1876 unknow. 
- `quantity`: 5 categories. 789 unknow.
- `source_class`: 3 categories. 278 unknow.
- `waterpoint_type_group`: 6 categories.

### 4. Final result
1. `df_training`: 59400 * 21

    `df_test`: 14850 * 20
2. Unresolved problems:
    - How to transform skewed data like `population`, `amount_tsh` and `management_group`
    - Can `gps_height` provide predictive power?

