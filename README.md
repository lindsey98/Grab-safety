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


## Feature extraction
- Acceleration-based features:

  We first calculate the resultant acceleration by taking the l2 norm of acc_x, acc_y and acc_z.
  
- Gyroscope-based features:

  We first calculate the resultant gyroscope by taking the l2 norm of gyro_x, gyro_y and gyro_z.
  
- Speed-based features

- Bearing-based features
  



## Model building

