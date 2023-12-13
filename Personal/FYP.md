#### Problem statement

- Hard to read pH level of an environment manually in some environment
- Tedious and repetitive routine of action
- Manually collect and analyse the data

#### Requirement

- pH sensor Arduino
- google cloud account
- 3d printer for casing

#### PH tester

1. get data from pH sensor Arduino
2. use a cup with a hole as tank and clear the tank x seconds after reader read data (rain, animal saliva)
3. stick into cup and read data every x seconds (tank, pool, soil)
4. send data using containerised REST api to cloud
5. display the pH result in graph and real time data, alert in drastic changes

#### What are these for?

1. Enforcers to track activity of agriculture
2. Farmers to ensure the crop is in good acidity or alkalinity
3. Acid rain warning
4. Animal health tracker
5. Drinking water quality test
6. Admin control

#### For improvements

1. send data using MQTT protocol to reduce the amount of sim card needed for agriculture use case
2. attach more sensor such as temperature, light intensity, wind reader, for weather analysis
