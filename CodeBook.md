### Codebook - Getting, Cleaning, and Creating Tidy Data Set
---
###Variables
---
* ***feature_list1*** : captures the names of the 561 measurement variables, which are given in the file `features.txt`

* ***activity_labels*** : the mapping from Activity-Id to an Activity-Label. The label is a descriptive text. E.g. `1` corresponds to `walking`, `4` corresponds to `sitting` etc. The mapping data for all the 6 activities is provided in the `activity_labels.txt` file.  

* ***x_test*** : Test measurement data (561 columns), 1 row per observation.

* ***y_test*** : Activity Labels for the Test data, 1 row per observation; same number of rows as x_test.

* ***subject_test*** : Subject Id for the Test data, 1 row per observation; same number of rows as x_test. Subject Id is a number. A mapping to a name is not provided to maintain anonymity.

* ***x_train, y_train, subject_train*** : variables corresonding to the training data, similar to the test data set above. 

---
###Transformation
---
---