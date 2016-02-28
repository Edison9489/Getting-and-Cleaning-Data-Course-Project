##Codebook

###Overview

[Source](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip) of the original data:

	https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

[Full Description](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones) at the site where the data was obtained:

	http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones
	
###process
The run_analysis.R can finish the following tasks:
	1. Reads data from all train and test data file and merges all training and the test sets to create one data. Also 			       columns have been properly labeled.
	2. Extracts only the measurements on the mean and standard deviation for each measurement.
	3. Loads activity labels from activity_labels.txt and uses descriptive activity names to name the activities in the data 	   set
	4. Appropriately labels the data set with descriptive variable names.
	5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each 			   activity and each subject and saves the data as Data.txt

###Variables
	trainSubject - table contents of train/subject_train.txt
	trainLabel - table contents of train/y_train.txt
	trainSet - table contents of train/X_train.txt
	testSubject - table contents of test/subject_test.txt
	testLabel - table contents of test/y_test.txt
	testSet - table contents of test/X_test.txt
	feature - table contents of features.txt
	alldata - combinded dataset for all training and test data
	colWithMeanStd - places of columns refering mean and std measurement in the alldata
	dataExtracted - extracted dataset with only the measurements on the mean and standard deviation
	activityLabels - table contents of activity_labels.txt
	tidyData - subsetted, human-readable data ready for output according to project description
	
###Output

####Data.txt
Data.txt is a 180x88 data frame.

- The first column contains subject IDs.
- The second column contains activity names.
- The averages for each of the 86 attributes are in columns 3-88.

	
