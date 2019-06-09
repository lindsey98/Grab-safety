# Grab-safety
This is project is for 2019 Grab AI challenge.
## Problem description
We aim to categorize car trips as being dangerous or normal based on a set of features:
- Accuracy : the accuracy of GPS
- Bearing : the GPS bearing
- Acceleration_x : the acceleration on x axis
- Acceleration_y : the acceleration on y axis
- Acceleration_z : the acceleration on z axis
- Gyro_x : the gyroscope on x axis
- Gyro_y : the gyroscope on y axis
- Gyro_z : the gyroscope on z axis
- Speed : the velocity
- Second : the time when the record is taken

## Data cleansing
For bookingID with multiple labels, I treat them as dangerous(label = 1) because they are suspicious. The records who have speed larger than 200km/h (55.56 m/s) or negative values are removed because they are unrealistic, trips which last for more than 12 hours are also dropped because it is unlikely that a single trip can extend to 12 hours. Moreover, to ensure the accuracy of the readings, we only keep records who have accuracy less than 50 meters(more confident in the GPS readings). 

## Feature extraction
- Acceleration-based features:

    I first calculate the resultant acceleration by taking the l2 norm of acc_x, acc_y and acc_z.
  
- Gyroscope-based features:

    I first calculate the resultant gyroscope by taking the l2 norm of gyro_x, gyro_y and gyro_z.
  
- Speed-based features

- Bearing-based features
  



## Model building

