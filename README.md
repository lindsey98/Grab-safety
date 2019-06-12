# Grab-safety

&nbsp;&nbsp;&nbsp;This project is for 2019 Grab AI challenge.

## Problem description

&nbsp;&nbsp;&nbsp;We aim to categorize car trips as being dangerous or normal based on a set of features:
- Accuracy : the accuracy of GPS
- Bearing : Bearing is the direction to the destination or target. It is different from Heading(measures the exact direction the car is heading), so the change in bearing cannot be used to compute the number of turns in a route.
- Acceleration_x : the acceleration on x axis, this will control the rotational acceleration.
- Acceleration_y : the acceleration on y axis, this is the linear acceleration pointing to the heading of the car.
- Acceleration_z : the acceleration on z axis, this is the vertical acceleration pointing to the earth.  
- Gyro_x : the gyroscope about x axis, this is the angular velocity when rotating around x axis.
- Gyro_y : the gyroscope about y axis, this is the angular velocity when rotating around y axis.
- Gyro_z : the gyroscope about z axis, this is the angular velocity when rotating around x axis.
- Speed : the instantaneous velocity
- Second : the time when the record is taken

** Note: The acceleration, gyroscope are measured by smartphone whose coordinate system is aligned with the car movement, the y axis points towards the orientation of the car,the z-axis points downwards so that it is aligned with gravity when the smartphone is flat on a table, the x-axis points to the side.

## Data cleansing

* For bookingID with multiple labels, I treat them as dangerous(label = 1) because they are suspicious. 

* The records who have speed larger than 200km/h (55.56 m/s) or negative values are removed because they are unrealistic;

* Trips which last for more than 12 hours are also dropped because it is unlikely that a single trip can extend to 12 hours;

* Moreover, to ensure the accuracy of the readings, we only keep records who have accuracy less than 50 meters(more confident in the GPS readings);

* Finally, trips who have less than 60 records(namely insufficient data points) are removed.

## Feature extraction

&nbsp;&nbsp;&nbsp;Some previous work have been using signal-based features(Fourier transformation to get the highest FFT; PAR; SVM; DSVM etc.). But their data are continuously collected every fixed interval of time, but in this real-life dataset, the records may not be available for every second in a trip and they are missing at random position. Thus, using signal-based techniques may not be very fruitful. 

&nbsp;&nbsp;&nbsp;For each trip, the time series of acceleration, speed, gyroscope are first smoothed out by implementing moving average with window size = 5, this is to denoise data and avoid random fluctuation. Then, features are extracted as following:

- Acceleration-based features:

&nbsp;&nbsp;&nbsp;&nbsp;I first calculate the resultant acceleration.
  
- Gyroscope-based features:
  
- Speed-based features:

- Bearing-based features:
  



## Model building
