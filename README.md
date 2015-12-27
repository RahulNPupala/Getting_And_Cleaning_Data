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

activity_labels         <- read.table("./activity_labels.txt")
colnames(activity_labels) <- c("Activity_Id", "Activity_Label") # Add descriptive column names

x_test                  <- read.table("./test/X_test.txt")
y_test                  <- read.table("./test/y_test.txt")
subject_test            <- read.table("./test/subject_test.txt")
colnames(x_test)        <- feature_list1                        # Add descriptive column names
colnames(y_test)        <- c("Activity_Id")                     # Add descriptive column names
colnames(subject_test)  <- c("Subject_Id")                      # Add descriptive column names

x_train                 <- read.table("./train/X_train.txt")
y_train                 <- read.table("./train/y_train.txt")
subject_train           <- read.table("./train/subject_train.txt")
colnames(x_train)       <- feature_list1                        # Add descriptive column names
colnames(y_train)       <- c("Activity_Id")                     # Add descriptive column names
colnames(subject_train) <- c("Subject_Id")                      # Add descriptive column names
```

* Do Step 1 Merge the training and the test sets to create one data set. Use cbind(), rbind(). Add a row Id column (rightmost) to rescue row scrambling by merge()
```
data_test   <- cbind(subject_test,  y_test,  x_test)    # <Subject Id, Activity Id, <561-variables>>
data_train  <- cbind(subject_train, y_train, x_train)

data_step1  <- rbind(data_test, data_train)             # merge the rows of train and test data
data_step1$rowID <- 1:nrow(data_step1)                  # Add a row Id column to rescue row scrambling by merge()
```
