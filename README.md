# Kaggle Featured, ASHRAE - Great Energy Predictor III
> In this competition, you’ll develop models of metered building energy usage in the following areas: chilled water, electric, hot water, and steam meters. The data comes from over 1,000 buildings over a three-year timeframe. 

> [For more info of the competition](https://www.kaggle.com/c/ashrae-energy-prediction/overview)

> [Direct link for data](https://www.kaggle.com/c/9994/download-all)
## some thoughts after EDA/discussion
- site 0:
has meter reading 0 in the first few months in training set
- site 7:
all are educational buildings, with large area
- building 778,1099:
extreme large consumption

## fill building info
- fill missing 'year_built' and change to 'age'
- fill missing 'floor_count' by considering 'area(square feet)' per floor of the same primary use
result in building_metadata2

## fill weather data
- add features 'relative_humidity', 'apparent_temp' based on 'air_temperature', 'dew_temperature', 'wind_speed'
- result in weather_train_fixweather

## add min max temp
- add daily min max air temperature
- result in weather_train_agg

## merge files
- merge weather, building into train/test data

### [xgboost]
#### per building per meter, an eariler version for an old machine
- XGB_old_fillweather
- XGB_old_onehot
- XGB_old
- XGB_old_output

#### per meter, high memory usage for onehot enconding and DMatrix
- XGB_onehot
- XGB_per_meter


### [lightGBM]
- LGBM_merge
- LGBM`

## fill missing result
- there are some gaps in test set where weather data is not available, and meter reading are predicted using prediction of nearest timestamp before/after
