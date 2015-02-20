# GACD_Assignment

R code used to create tidy_data.txt

  setwd("C:/Joel_Work/Coursera/8_Getting_and_Cleaning_Data_JH/Assignments")
  activity_labels = read.csv("activity_labels.txt", header = FALSE, sep = "", stringsAsFactors = FALSE)
  colnames(activity_labels)[1] = "Activity"
  colnames(activity_labels)[2] = "Activity_Label"
  features = read.table("features.txt")
  colnames(features)[1] = "Index"
  colnames(features)[2] = "Feature"
  features$Feature = as.character(features$Feature)
  
  #1.Merges the training and the test sets to create one data set.
  
  #First combine the training and test sets into one set for each of the three file types:
  setwd("C:/Joel_Work/Coursera/8_Getting_and_Cleaning_Data_JH/Assignments/test")
  subject_test = read.table("subject_test.txt", stringsAsFactors = FALSE)
  setwd("C:/Joel_Work/Coursera/8_Getting_and_Cleaning_Data_JH/Assignments/train")
  subject_train = read.table("subject_train.txt", stringsAsFactors = FALSE)
  subject_data = rbind(subject_test,subject_train)
  colnames(subject_data)[1] = "Subject"
  
  
  setwd("C:/Joel_Work/Coursera/8_Getting_and_Cleaning_Data_JH/Assignments/test")
  Y_test = read.table("Y_test.txt", stringsAsFactors = FALSE)
  setwd("C:/Joel_Work/Coursera/8_Getting_and_Cleaning_Data_JH/Assignments/train")
  Y_train = read.table("Y_train.txt", stringsAsFactors = FALSE)
  Y_data = rbind(Y_test,Y_train)
  colnames(Y_data)[1] = "Activity"
  
  setwd("C:/Joel_Work/Coursera/8_Getting_and_Cleaning_Data_JH/Assignments/test")
  X_test = read.table("X_test.txt", stringsAsFactors = FALSE)
  setwd("C:/Joel_Work/Coursera/8_Getting_and_Cleaning_Data_JH/Assignments/train")
  X_train = read.table("X_train.txt", stringsAsFactors = FALSE)
  X_data = rbind(X_test,X_train)
  
  #4.Appropriately labels the data set with descriptive variable names.
  
  #Use the features.txt and use that for the column names in x:
  for(i in 1:ncol(X_data)){
    names(X_data)[i] = features[i,2]
  }
  
  #2.Extracts only the measurements on the mean and standard deviation for each measurement in X_data.
  full_data = X_data[,grep("mean()|std()",colnames(X_data))]
  ncol(full_data)
  #Now take out meanfreq columns.
  full_data = full_data[,-grep("meanFreq",colnames(full_data))]
  ncol(full_data)
  
  #Note that the line removed columns that have "meanFreq" in the title. There are 13.
  #However, I originally had "meanfreq" as the argument. I would have expected
  #this to leave all 79 columns in there, since none have "meanfreq". But instead
  #it produced 0. Why is that?
  
  #Now combine the three data sets (subject_data, Y_data, X_data)
  full_data = cbind(subject_data,Y_data,full_data)
  ncol(full_data)
  
  #3.Uses descriptive activity names to name the activities in the data set
  #Merge activity labels to the data set using the activity field. This brings in the activity labels field
  full_data = merge(activity_labels,full_data,by.x="Activity",by.y="Activity", all = TRUE)
  
  setwd("C:/Joel_Work/Coursera/8_Getting_and_Cleaning_Data_JH/Assignments")
  write.table(full_data, "full_data.txt", row.names = FALSE)
  
  #5.From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
  tidy_data = as.data.frame(aggregate(full_data[,4:69], by = list(full_data$Activity_Label, full_data$Subject),mean))
  names(tidy_data)[1] = "Activity_Label"
  names(tidy_data)[2] = "Subject"
  write.table(tidy_data, "tidy_data.txt", row.names = FALSE)
  write.csv(tidy_data, "tidy_data.csv", row.names = FALSE)