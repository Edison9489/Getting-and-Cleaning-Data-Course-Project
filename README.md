# Getting-and-Cleaning-Data-Course-Project
library(data.table)
library(dplyr)
####Read data
####Training
trainSubject <- read.table("UCI HAR Dataset/train/subject_train.txt", header = FALSE)
trainLabel <- read.table("UCI HAR Dataset/train/y_train.txt", header = FALSE)
trainSet <- read.table("UCI HAR Dataset/train/X_train.txt", header = FALSE)
####Testing
testSubject <- read.table("UCI HAR Dataset/test/subject_test.txt", header = FALSE)
testLabel <- read.table("UCI HAR Dataset/test/y_test.txt", header = FALSE)
testSet <- read.table("UCI HAR Dataset/test/X_test.txt", header = FALSE)

####1.Merges the training and the test sets to create one data set.
feature <- read.table("UCI HAR Dataset/features.txt")
subject <- rbind(trainSubject,testSubject)
label <- rbind(trainLabel,testLabel)
set <- rbind(trainSet,testSet)
colnames(subject) <- "subject"
colnames(label) <- "label"
colnames(set) <- t(feature[2])
alldata <- cbind(set,label,subject)

####2.Extracts only the measurements on the mean and standard deviation for each measurement.
colWithMeanStd <- grep(".*Mean.*|.*Std.*", names(alldata), ignore.case=TRUE)
dataExtracted <- alldata[,c(colWithMeanStd,ncol(alldata)-1,ncol(alldata))]

####3.Uses descriptive activity names to name the activities in the data set
activityLabels <- read.table("UCI HAR Dataset/activity_labels.txt", header = FALSE)
for (i in 1:6) {
  dataExtracted$label[which(dataExtracted$label == i)] <- as.character(activityLabels$V2[i])
}

####4.Appropriately labels the data set with descriptive variable names
names(dataExtracted)
names(dataExtracted)<-gsub("^t", "time", names(dataExtracted))
names(dataExtracted)<-gsub("^f", "frequency", names(dataExtracted))
names(dataExtracted)<-gsub("Acc", "Accelerometer", names(dataExtracted))
names(dataExtracted)<-gsub("Gyro", "Gyroscope", names(dataExtracted))
names(dataExtracted)<-gsub("Mag", "Magnitude", names(dataExtracted))
names(dataExtracted)<-gsub("BodyBody", "Body", names(dataExtracted))

####5.From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
tidyData <- aggregate(. ~subject + label, dataExtracted, mean)

write.table(tidyData, file = "Data.txt",row.name=FALSE)
