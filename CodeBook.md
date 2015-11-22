---
title: "Assignment Codebook"
author: "Christian Segarra"
date: "November 21, 2015"
output: html_document
---
###Description Of Raw Data Obtained
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain.

The raw data used can be found at:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

###Description Of Columns In Raw Data
Each record contains:

* Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
* Triaxial Angular velocity from the gyroscope. 
* A 561-feature vector with time and frequency domain variables. 
* Its activity label. 
* An identifier of the subject who carried out the experiment.

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

* tBodyAcc-XYZ
* tGravityAcc-XYZ
* tBodyAccJerk-XYZ
* tBodyGyro-XYZ
* tBodyGyroJerk-XYZ
* tBodyAccMag
* tGravityAccMag
* tBodyAccJerkMag
* tBodyGyroMag
* tBodyGyroJerkMag
* fBodyAcc-XYZ
* fBodyAccJerk-XYZ
* fBodyGyro-XYZ
* fBodyAccMag
* fBodyAccJerkMag
* fBodyGyroMag
* fBodyGyroJerkMag

The set of variables that were estimated from these signals are: 

* mean(): Mean value
* std(): Standard deviation
* mad(): Median absolute deviation 
* max(): Largest value in array
* min(): Smallest value in array
* sma(): Signal magnitude area
* energy(): Energy measure. Sum of the squares divided by the number of values. 
* iqr(): Interquartile range 
* entropy(): Signal entropy
* arCoeff(): Autorregresion coefficients with Burg order equal to 4
* correlation(): correlation coefficient between two signals
* maxInds(): index of the frequency component with largest magnitude
* meanFreq(): Weighted average of the frequency components to obtain a mean frequency
* skewness(): skewness of the frequency domain signal 
* kurtosis(): kurtosis of the frequency domain signal 
* bandsEnergy(): Energy of a frequency interval within the 64 bins of the FFT of each window.
* angle(): Angle between to vectors.

Additional vectors obtained by averaging the signals in a signal window sample. These are used on the angle() variable:

* gravityMean
* tBodyAccMean
* tBodyAccJerkMean
* tBodyGyroMean
* tBodyGyroJerkMean

The complete list of variables of each feature vector is available in "features.txt"

###Processng Done To Make Data Set Complete
The following steps were taken to create a complete data set from the separate files provided.

1. The data given in "train.txt" and "test.txt" had no column names assigned. So a vector containing the names of the features in "features.txt" was created. These names were then assigned to the columns of "train.txt" and "test.txt". They were assigned in the following fashion: row 1 of features was assigned to the first column, row 2 of features was assigned to the second column and so on.

2. The column in "subject_test.txt" and "subject_train.txt" was assigned the name "Subject". The column in "y_test.txt" and "y_train.txt" was assigned the name "Activity"

3. The data given in "train.txt" and "test.txt" also did not specify which Subject and Activity the data corresponded to. The number of rows in "subject_test.txt", "y_test.txt", and "test.txt" were all equivalent, so it was therefore assumed that row 1 of "subject_test.txt" corresponded with row 1 of "y_test.txt" and row 1 "test.txt". Row 2 of each file corresponded to each other and so on. Using this assumption, the column in "subject_test.txt" and the column in "y_test.txt" were appended as the first two columns to "test.txt". The same reasoning and process was used to append the column in "subject_train.txt" and "y_train.txt" to "train.txt".

4. The data in "test.txt" and "train.txt" was combined horizontally to create one data frame containing all of the training and test data.

5. The columns that contained the strings "mean" or "std" were extracted.

6. The values of the column "Activity" contained integers that corresponded to actual Activity names. The file containing these names, "activity_labels.txt" was read into a vector. The integers were then replaced with their corresponding labels.

###Work Done to Tidy Up Data
The following steps were taken to tidy up the data.

1. Values were listed as variables. The gather function was used to create a key value pair, where the key was named "Feature". The "Subject" and "Activity" columns were left as is.

2. The group_by function was used to group the data by Subject, by Activity, by Feature. The summarize function was used to find the mean of each group's Feature value. The resulting summary column was named "Mean".

The code used to process and tidy the data can be find in run_Analysis.R
