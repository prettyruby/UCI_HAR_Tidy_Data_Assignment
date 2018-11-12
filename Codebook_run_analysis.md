Code Book - run_analysis.R - Human Activity Recognition Using Smartphones Dataset - Version 1.0

ORIGINAL INFO

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details.

- 'features.txt': List of all features.

- 'activity_labels.txt': Links the class labels with their activity name.

- 'train/X_train.txt': Training set.

- 'train/y_train.txt': Training labels.

- 'test/X_test.txt': Test set.

- 'test/y_test.txt': Test labels.

ASSIGNMENT INFO

- activity_labels: reads activity_labels.txt; links the class labels with their activity name (long name of each activity)

- features: reads features.txt; lists of all features (all the types of different measurements)

- X_test: reads X_test.txt; test set of measurements

- y_test: reads y_test.txt; test activity class labels

- subject_test: reads subject_test.txt; lists which subject each measurement in X_test was measured from

- X_train: reads X_train.txt; training set of measurements

- y_train: reads y_train.txt; training activity class labels

- subject_train: reads subject_train.txt; lists which subject each measurement in X_train was measured from

- X_subset: Tidy data set with each measurement on the mean and standard deviation for each measurement (mean and std only) for each activity and each subject; 10,299 rows by 68 columns (66 measurements with std or mean in measurement name + Subject + Activity)

- X_avg: Tidy data set with the average of each measurement on the mean and standard deviation for each measurement (mean and std only) for each activity and each subject; 180 rows (30 subjects x 6 activities) by 68 columns (66 measurements with std or mean in measurement name + Subject + Activity)

- Subject: subject identifier; came from subject_test and subject_train

- Activity: test activity class labels and training activity class labels associated with each measurement; long name comes from joining with activity_labels

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

The acceleration signals were measured in standard gravity units 'g'. The angular velocity vector measured by the gyroscope were captured in radians/second.

tBodyAcc-XYZ

tGravityAcc-XYZ

tBodyAccJerk-XYZ

tBodyGyro-XYZ

tBodyGyroJerk-XYZ

tBodyAccMag

tGravityAccMag

tBodyAccJerkMag

tBodyGyroMag

tBodyGyroJerkMag

fBodyAcc-XYZ

fBodyAccJerk-XYZ

fBodyGyro-XYZ

fBodyAccMag

fBodyAccJerkMag

fBodyGyroMag

fBodyGyroJerkMag

The set of variables that were estimated from these signals and included in the tidy data set X_avg are: 

mean(): Mean value
std(): Standard deviation

The signals that have -XYZ thus had means and std for each of those axial measurements.

There was thus a total of 66 different measurements or features averaged in the X_avg table.
