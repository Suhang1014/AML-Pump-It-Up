- remove

  ```python
  'lga'(Geographic location), 'ward'(Geographic location),'region_code', 'district_code', 'wpt_name'(Name of the waterpoint),'scheme_name','extraction_type','extraction_type_group','management','payment','quality_group','quantity_group','source_type','source','waterpoint_type'
  ```

- add `'existing year' ` replacing ` 'dat_recorded' ` and `'construction_year'` 

- replace the `'nan'` value of `'existing year'` to `'unkonwn'`

- remove

  ```python
  'amount_tsh', 'funder', 'subvillage','recorded_by'
  ```

- replace the `'nan'` value of `'public meeting'` to `'unkonwn'`

- finally, the columns kept are 

  ```python
  'existing year', 'gps_height', 'installer', 'longitude','latitude', 'num_private', 'basin', 'region', 'population','public_meeting', 'scheme_management', 'permit',
  'extraction_type_class', 'management_group', 'payment_type','water_quality', 'quantity', 'source_class', 'waterpoint_type_group','status_group'
  ```

- convert categorical variables into dummy/indicator variables, dummy columns

  ```python
  'installer', 'basin', 'region', 'public_meeting','scheme_management', 'permit','extraction_type_class', 'management_group', 'payment_type','water_quality', 'quantity', 'source_class', 'waterpoint_type_group'
  ```

  