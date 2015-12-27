### Programming Assignment: Get, Clean, and Create Tidy Data for Analyzing a given Data Set. 

---

####Assignment 

* *Step 1: Merges the training and the test sets to create one data set.*

* *Step 2: Extracts only the measurements on the mean and standard deviation for each measurement.* 

* *Step 3: Uses descriptive activity names to name the activities in the data set*

* *Step 4: Appropriately labels the data set with descriptive variable names.* 

* *Step 5: From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.*

---

####Notes

We perform **all** the needed steps above, **though not in the order given**. The comments within the code (run_analysis.R), specify the step associated with a code snippet

---

#### Code Snippets Explained

* Do Step 0 Go to the directory containing the data
```
getwd()
setwd("./UCI HAR Dataset")
```

* Do Step 4 Appropriately labels the data set with descriptive variable names. the colnames() function has been used below to label variables. E.g.
```
feature_list  <- read.table("./features.txt", stringsAsFactors=FALSE)
feature_list1 <- feature_list[, 2]
```
 
