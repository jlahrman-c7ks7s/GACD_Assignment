# GACD_Assignment

This codebook describes describes the variables, the data, and the transformations or work that the author performed to clean up the data used for the Practical Machine Learning class assignment. Each variable in the final dataset will also be described.
The goals of the project, using the specified data, are to:
1.	Merge the training and the test sets to create one data set.
2.	Extracts only the measurements on the mean and standard deviation for each measurement.
3.	Use descriptive activity names to name the activities in the data set
4.	Appropriately labels the data set with descriptive variable names. 
5.	From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
The run_Analysis.R script performs steps 1-5 in reproducible code. The following steps are performed by the code. The goal that each step goes towards achieving is also specified.
Lines 1-9: The activity_labels.txt and features.txt files are read. The activity_labels.txt file provides descriptive labels for the activity codes listed in Y_data (Goal 3) and the features.txt file provides descriptive variable names for the fields in X_data (Goal 4)
Lines 10-33: The test and training data for the subject, Y, and X datasets are read. The rbind command is used to stack the test and training data for each respective pair of data sets (Goal 1). In line 18 and 26, the individual columns of the Subject and Y_data are named (Goal 4).
Lines 34-40: A for loop is used to assign the elements of the features.txt file as the variable names of the X_data file (Goal 4).
Lines 41-52: Two grep functions are used to reduce the X_data to contain only the measurements on the mean and standard deviation for each measurement (Goal 2). The first grep function reduces the file to only fields that contain the text “mean()” or “std()”. Note that this function was performed before the Subject and Y_data are merged with the X_data to avoid causing the removal of these two variables. It was noticed that the first grep function keeps field names that include the text “meanFreq()”. The second grep function removes these fields. This decision has been made for two reasons. Firstly, the meanFreq() text differs from the mean() format of the other variables names. Secondly, the meanFreq() variables are not followed by variables with std() in the title, as the mean() are. It appears that these meanFreq() titles refer to the type of data contained in the variable, as opposed to the statistic calculated on the variable.
Lines 53-56: The subject, Y, and X data are combined using a cbind function to create one overall dataset (Goal 1)
Lines 57-63: A merge function is used to add the activity_labels field that provides a description of the activity specified by the numerical code of the activity field (Goal 3). This complete dataset is then stored as a txt file for documentation.
Lines 64-69: An aggregate function is used to calculate the average of each variable by activity and subject (Goal 5). This tidy dataset is then written as both a .csv and .txt file.
VARIABLES IN THE FINAL TIDY DATASET
Activity_Label
	Activity performed by subject
Subject:
	1-30. unique identifier of individual participant

For all remaining variables, the result indicates the mean of the measurement for the respondent. The original measurement is the differences of the individual reading from the overall mean of the measurement, normalized and bounded within [-1,1]
tBodyAcc-mean()-X, -Y, -Z (three variables, each referring to one axis)
tBodyAcc-std()-X, -Y, -Z (three variables, each referring to one axis)
tGravityAcc-mean()-X, -Y, -Z (three variables, each referring to one axis)
tGravityAcc-std()-X, -Y, -Z (three variables, each referring to one axis)
tBodyAccJerk-mean()-X, -Y, -Z (three variables, each referring to one axis)
tBodyAccJerk-std()-X, -Y, -Z (three variables, each referring to one axis)
tBodyGyro-mean()-X, -Y, -Z (three variables, each referring to one axis)
tBodyGyro-std()-X, -Y, -Z (three variables, each referring to one axis)
tBodyGyroJerk-mean()-X, -Y, -Z (three variables, each referring to one axis)
tBodyGyroJerk-std()-X, -Y, -Z (three variables, each referring to one axis)
tBodyAccMag-mean()
tBodyAccMag-std()
tGravityAccMag-mean()
tGravityAccMag-std()
tBodyAccJerkMag-mean()
tBodyAccJerkMag-std()
tBodyGyroMag-mean()
tBodyGyroMag-std()
tBodyGyroJerkMag-mean()
tBodyGyroJerkMag-std()
fBodyAcc-mean()-X, -Y, -Z (three variables, each referring to one axis)
fBodyAcc-std()-X, -Y, -Z (three variables, each referring to one axis)
fBodyAccJerk-mean()-X, -Y, -Z (three variables, each referring to one axis)
fBodyAccJerk-std()-X, -Y, -Z (three variables, each referring to one axis)
fBodyGyro-mean()-X, -Y, -Z (three variables, each referring to one axis)
fBodyGyro-std()-X, -Y, -Z (three variables, each referring to one axis)
fBodyAccMag-mean()
fBodyAccMag-std()
fBodyBodyAccJerkMag-mean()
fBodyBodyAccJerkMag-std()
fBodyBodyGyroMag-mean()
fBodyBodyGyroMag-std()
fBodyBodyGyroJerkMag-mean()
fBodyBodyGyroJerkMag-std()
