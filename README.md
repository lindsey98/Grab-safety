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

** Note: The acceleration, gyroscope are measured by smartphone whose coordinate system is aligned with the car movement, the y axis points towards the orientation of the car,the z-axis points downwards so that it is aligned with gravity when the smartphone is flat on a table, the x-axis points to the side. **

## Data cleansing

* For bookingID with multiple labels, I treat them as dangerous(label = 1) because they are suspicious. 

* The records who have speed larger than 400km/h or negative values are removed because they are unrealistic;

* Trips which last for more than 12 hours are also dropped because it is unlikely that a single trip can extend to 12 hours;

* Moreover, to ensure the accuracy of the readings, we only keep records who have accuracy less than 50 meters(more confident in the GPS readings);

* Finally, trips who have less than 60 records(namely insufficient data points) are removed.

## Feature extraction

&nbsp;&nbsp;&nbsp;Some previous work have been using signal-based features(Fourier transformation to get the highest FFT; PAR; SVM; DSVM etc.). But their data are continuously collected every fixed interval of time, but in this real-life dataset, the records may not be available for every second in a trip and they are missing at random position. Thus, using signal-based techniques may not be very fruitful. 

&nbsp;&nbsp;&nbsp;For each trip, the time series of acceleration, speed, gyroscope are first smoothed out by implementing moving average with window size = 5, this is to denoise data and avoid random fluctuation. Then, features are extracted as following:

- Acceleration-based features:

&nbsp;&nbsp;&nbsp;&nbsp;Resultant acceleration is computed as the following: `result_acc = acc_x ** 2 + acc_y ** 2 + acc_z **2 `, descriptive statistics(mean, max, std, iqr) are extracted from the raw series. In addition, change in acceleration between two consecutive data points are extracted and mean_diff and max_diff are added. Besides, acc_increase, acc_decrease are the maximum length of consecutive increase/decrease normalized by trip length. 
  
- Gyroscope-based features:

&nbsp;&nbsp;&nbsp;&nbsp;Resultant gyroscope is computed as the following: `result_gyro = gyro_x ** 2 + gyro_y ** 2 + gyro_z **2 `, same features are computed for result_gyro, except that a new feature called avg_gyro is added: `avg_gyro = total radians / time duration of the trip`, the `total_radians` is the integration of gyro speed over time which measures the total angle the car has turned during a trip.

- Speed-based features:

&nbsp;&nbsp;&nbsp;&nbsp;Similar features are extracted from speed, `avg_speed` is computed using the same logic for `avg_gyro`

- Bearing-based features:
  
The features that can be extracted out of Bearing is limited since Bearing is different from the actual heading direction of the car, however, it may be still helpful to get the change in bearing over time. `bearing_std, consecutive_bear_increase, consecutive_bear_decrease,mean_bear_diff, max_bear_diff ` are calculated; Moreover, `bearing_change_per_dist = sum(bearing_change) / total_distance` is a good measure for how tortuous the route is. 

- Rotation-based features:

According to [1], the instant rotation angle about x-axis and y-axis can be approximated using acc_x , acc_y and acc_z, and the rotation angle phi, theta are summarized by maximum value, maximum value in difference. In addition, the number of 90 degree change in direction may also be a related factor. It is computed by getting the cumulative integral of gyro_z(rotation around z-axis) and count the number of times the cumulative changes in this integral list are larger than 90 degree. The mean time gap between 90 degree change is also returned. 

- Other features:

** Distance: Integration of Speed over time (total distance)

** Rad_dist: Integration of Result_gyro over time (total rotation angle)

** Trip_len: The last timestamp for the trip (total time)

** Rotation_x_dist: Integration of gyro_x (total rotation angle about x axis)

** Rotation_y_dist: Integration of gyro_y (total rotation angle about y axis)




## Model building


## Instructions

1. If you want to validate the results, you can first run *safety_data_cleaning.ipynb* and extract the raw dataframe, then run *safety_feature.ipynb* to extract the features and output the df_feature in a csv file, finally run *safety_training.ipynb* to train the model, you can save your model for future use.

2. You are free to skip the data_cleaning and feature_engineering notebook and directly jump to *safety_training.ipynb* using df_feature.csv as input which has been uploaded to this repository.

3. For model testing, please first import your testing dataset and extract corresponding features and save it to a dataframe, then import the model you have trained on the full training dataset.

## References
1. 
2.
3.
4.

