# Getting-and-Cleaning-data---project
As part of the GandC course

getwd()
setwd("C:/Users/User/Documents/UCI HAR Dataset")##This was the location of the file
##Had to be extracted from the zip mode due to an error that appears when I load the data, and I could not solve it in time.

# Uses descriptive activity/test names to name the activitie/test in the data set
ActLabels <- read.table("activity_labels.txt")##the labels were charged, it was a little bit difficult to find the cause of the error (txt.)
ActLabels[,2] <- as.character(Labels[,2])##and located
features <- read.table("features.txt")##the features were charged
features[,2] <- as.character(features[,2])##and located

# Extracts only the measurements on the mean and standard deviation for each measurement.
feat <- grep(".*mean.*|.*std.*", features[,2])##Looking for mean and standar deviation in features
feat.names <- features[feat,2]
feat.names = gsub('-mean', 'Mean', feat.names)##Substitution of terms that can be misleading
feat.names = gsub('-std', 'Std', feat.names)##Substitution of terms that can be misleading
feat.names <- gsub('[-()]', '', feat.names)##Substitution of terms that can be misleading


# Loading the databases
train <- read.table("train/X_train.txt")[feat]##reading the db train
trainAct <- read.table("train/Y_train.txt")##reading the activities of db train
trainSub <- read.table("train/subject_train.txt")##reading the db train subjects
train <- cbind(trainSub, trainAct, train)##Combining the 3 db

test <- read.table("test/X_test.txt")[feat]##reading the db test
testAct <- read.table("test/Y_test.txt")##reading the activities of db test
testSub <- read.table("test/subject_test.txt")##reading the db train subjects
test <- cbind(testSub, testAct, test)##Combining the 3 db

# Merging the training and the test sets to create one data set. 
Finale <- rbind(train, test)##Finally the db were merged
colnames(Finale) <- c("subject", "activity", feat.names)##Giving the names of the columns with the variable created previously

# activities and subjects as factors
Finale$activity <- factor(Finale$activity, levels = ActLabels[,1], labels = ActLabels[,2])##turning to factors to aggregate to the evaluation
Finale$subject <- as.factor(Finale$subject)##Turning as factors to aggregate to the evaluation

library(reshape2)##Necesary to melt

##From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
Finale.melted <- melt(Finale, id = c("subject", "activity"))##putting together subject and activity
Finale.mean <- dcast(Finale.melted, subject + activity ~ variable, mean)##I want a column for subject and activity

write.table(Finale.mean, "tidy.txt", row.names = FALSE, quote = FALSE)

head(Finale.melted)
View(Finale.melted)
View(Finale.mean)
View("tidy.txt")

