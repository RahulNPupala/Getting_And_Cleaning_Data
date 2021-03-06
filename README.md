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

#### Code Snippets of run_analysis.R Explained

* **Do Step 0 Go to the directory containing the data**
```
getwd()
setwd("./UCI HAR Dataset")
```

* **Do Step 4 Appropriately labels the data set with descriptive variable names.** 

The colnames() function has been used below to label variables. E.g.
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

* **Do Step 1 Merge the training and the test sets to create one data set.** 

Use cbind(), rbind(). Add a row Id column (rightmost) to rescue row scrambling by merge()
```
data_test   <- cbind(subject_test,  y_test,  x_test)    # <Subject Id, Activity Id, <561-variables>>
data_train  <- cbind(subject_train, y_train, x_train)

data_step1  <- rbind(data_test, data_train)             # merge the rows of train and test data
data_step1$rowID <- 1:nrow(data_step1)                  # Add a row Id column to rescue row scrambling by merge()
```

* **Do Step 2 Extract only the measurements on the mean and standard deviation for each measurement.** 

Inspecting the data dictionary contained in feature.txt, we realize that this amounts to extracting the following columns from the 561-variable sets. We add an offset of 2, to account for the Subject Id and Activity Id columns inserted on the left of this 561-variable set.
```
colsInterested1 <- c(1:6, 41:46, 81:86, 121:126, 161:166)
colsInterested2 <- c(201, 202, 214, 215, 227, 228, 240, 241, 253, 254)
colsInterested3 <- c(266:271, 345:350, 424:429)
colsInterested4 <- c(503, 504, 516, 517, 529, 530, 542, 543)

colsInterested  <- 2 + c(colsInterested1, colsInterested2, colsInterested3, colsInterested4)
                                                        # offset of 2 for left inserted columns

colsInterestedx <- c(1, 2, colsInterested, 564)         # include the Subject Id, Activity Id, rowId

data_step2      <- data_step1[, colsInterestedx]
```

* **Do Step 3 Use descriptive activity names to name the activities in the data set** 

This was done using merge(). Then we use order() to restore the order of the data set which was scrambled by the merge().
We should not include the rowId column after re-ordering.
We write the tidy data to the file tidyData.txt; remembering to set row.name=FALSE
```
m <- merge(data_step2, activity_labels, by.x = "Activity_Id", by.y = "Activity_Id")
merge_data_step3 <- m[order(m$rowID), -c(1, 69)]        # retain original order of tuples, remove rowID column
m2 <- merge_data_step3[, c(1, 68, 2:67)]                # re-order columns

write.table(m2, file = "./tidyData.txt", row.name=FALSE)
```

* **Do Step 5 From the data set in step 4, create a second, independent tidy data set with the average of each variable for each activity and each subject.**

We use the aggregate() command. 
We write the tidy data to the file tidyDataGroupAggregate.txt; remembering to set row.name=FALSE
```
meanV <- aggregate(m2[, 3:68], list(Subject_Id = m2$Subject_Id, Activity_Label = m2$Activity_Label), mean)
write.table(meanV, file = "./tidyDataGroupAggregate.txt", row.name=FALSE)
```