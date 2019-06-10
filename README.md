# Grab-safety
This project is for 2019 Grab AI challenge.
## Problem description
We aim to categorize car trips as being dangerous or normal based on a set of features:
- Accuracy : the accuracy of GPS
- Bearing : Bearing is the direction to the destination or target.
- Acceleration_x : the acceleration on x axis
- Acceleration_y : the acceleration on y axis
- Acceleration_z : the acceleration on z axis
- Gyro_x : the gyroscope on x axis
- Gyro_y : the gyroscope on y axis
- Gyro_z : the gyroscope on z axis
- Speed : the velocity
- Second : the time when the record is taken

## Data cleansing

* For bookingID with multiple labels, I treat them as dangerous(label = 1) because they are suspicious. 

* The records who have speed larger than 200km/h (55.56 m/s) or negative values are removed because they are unrealistic;

* Trips which last for more than 12 hours are also dropped because it is unlikely that a single trip can extend to 12 hours;

* Moreover, to ensure the accuracy of the readings, we only keep records who have accuracy less than 50 meters(more confident in the GPS readings);

* Finally, trips who have less than 60 records(namely insufficient data points) are removed.

## Feature extraction

For each trip, the time series of acceleration, speed, gyroscope are first smoothed out by implementing moving average with window size = 5, this is to denoise data and avoid random fluctuation. Then, features are extracted as following:

- Acceleration-based features:

    I first calculate the resultant acceleration.
  
- Gyroscope-based features:
  
- Speed-based features:

- Bearing-based features:
  



## Model building

