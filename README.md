--------------------------------------------------------------------------------------------
Name        : run_analysis()

Purpose     : Get, Clean, and Create Tidy Data for analyzing a given data set.
              The steps to be performed in the assignment are listed below.

Notes       : We perform all the needed steps, though not in the order given.
              The comments within the code, specify the step associated with a code snippet

Usage       : source("run_analysis")

Author      : Rahul N. Pupala

Date        : 25 Dec 2015

--------------------------------------------------------------------------------------------

Assignment ---------------------------------------------------------------------------------
Merges the training and the test sets to create one data set.

Extracts only the measurements on the mean and standard deviation for each measurement. 

Uses descriptive activity names to name the activities in the data set

Appropriately labels the data set with descriptive variable names. 

From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
--------------------------------------------------------------------------------------------

Do Step 0 Go to the directory containing the data


Do Step 4 Appropriately labels the data set with descriptive variable names. --------------
   the colnames() function has been used below to label variables. E.g.
x_test                  <- read.table("./test/X_test.txt")
colnames(x_test)        <- feature_list1                        # Add descriptive column names


Do Step 1 Merge the training and the test sets to create one data set. --------------------
Use cbind(), rbind(). Add a row Id column (rightmost) to rescue row scrambling by merge()


Do Step 2 Extract only the measurements on the mean and standard deviation for each measurement.


Do Step 3 Use descriptive activity names to name the activities in the data set -----------
done using merge(). Then use order() to restore the order of the data set which was scrambled
by the merge().
Do not include the rowId column after re-ordering.
Write the tidy data to the file tidyData.txt. Remember to set row.name=FALSE


Do Step 5 From the data set in step 4, creates a second, independent tidy data set with the 
   average of each variable for each activity and each subject.
Use the aggregate() command. 
Write the tidy data to the file tidyDataGroupAggregate.txt. Remember to set row.name=FALSE