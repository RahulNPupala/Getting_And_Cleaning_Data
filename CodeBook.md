### Codebook - Getting, Cleaning, and Creating Tidy Data Set
---
###Variables

* ***feature_list1*** : captures the names of the 561 measurement variables, which are given in the file `features.txt`

* ***activity_labels*** : the mapping from Activity-Id to an Activity-Label. The label is a descriptive text. E.g. `1` corresponds to `walking`, `4` corresponds to `sitting` etc. The mapping data for all the 6 activities is provided in the `activity_labels.txt` file.  

* ***x_test*** : Test measurement data (561 columns), 1 row per observation.

* ***y_test*** : Activity Labels for the Test data, 1 row per observation; same number of rows as x_test.

* ***subject_test*** : Subject Id for the Test data, 1 row per observation; same number of rows as x_test. Subject Id is a number. A mapping to a name is not provided to maintain anonymity.

* ***x_train, y_train, subject_train*** : variables corresonding to the training data, similar to the test data set above. 

* ***meanV*** : final output of the data analysis, which  creates the second, independent tidy data set with the average of each variable for each activity and each subject.

---
###Temporary (Programming) Variables

* ***colsInterestedx*** : since we want only certain columns (mean and std of measurement variables)

* ***data_step1*** : output of transformation step #1

* ***data_step2*** : output of transformation step #2. At this point, we have selected only the columns of interest (mean and std of measurement variables). The colsInterestedx variable identifies these columns for us.

* ***m*** : descriptive activity names replace the activity ids of variable data_step2.

*  ***merge_data_step3*** is used as an intermediate to m2, before re-ordering the rows which were scrambled by the merge() operation. Also, we discard the rowId column.

* ***m2*** : output of step #3. At this stage, descriptive activity names replace the activity ids in the data set data_step2.

---
###Transformations

* ***Step #4:*** 

Appropriately labels the data set with descriptive variable names. This step was performed first as a matter of programming convenience. No new variables were created. The variable names were descriptively added to the original names i.e. feature_list1, activity_labels, x_test, y_test, subject_test, x_train, y_train, subject_train

* ***Step #1:*** 
![alt text](https://github.com/RahulNPupala/Getting_And_Cleaning_Data/blob/master/step1.jpg "Step #1 Data Transformation")

* ***Step #2:***

data_step2      <- data_step1[, colsInterestedx]

* ***Step #3:***

data_step2 ---> m ---> merge_data_step3 ---> m2

* ***Step #5:***

m2 ---> meanV

The variable meanV is a bit of a misnomer, since it contains mean and std columns of the measurement variables.

---