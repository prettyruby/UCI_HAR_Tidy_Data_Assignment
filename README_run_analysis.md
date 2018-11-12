#Read the data into R

setwd("~/R/data/UCI_HAR_Dataset")
activity_labels <- read.table("activity_labels.txt")
features <- read.table("features.txt")

setwd("~/R/data/UCI_HAR_Dataset/test")
X_test <- read.table("X_test.txt")
y_test <- read.table("y_test.txt")
subject_test <- read.table("subject_test.txt")

setwd("~/R/data/UCI_HAR_Dataset/train")
X_train <- read.table("X_train.txt")
y_train <- read.table("y_train.txt")
subject_train <- read.table("subject_train.txt")

#use View() on each data frame (if using RStudio) to look at the data frame and understand its structure
#can also use dim() and/or head()
#any(is.na(X_test)) or sum(is.na(X_test)) to check if any NA's in X_test data frame (FALSE or 0 means none)
#any(is.na(X_train)) or sum(is.na(X_train)) to check if any NA's in X_train data frame (FALSE or 0 means none)

#note that subject_train and subject_test only use numbers to distinguish the subjects
#n_distinct(subject_test) gives 9 different subjects
#n_distinct(subject_train) gives 21 different subjects

#rename column names of X_test using features data frame
#join y_test observations from numbers to the corresponding activity labels
#bind y_test activity labels to X_test data frame
#bind subject_test column to X_test data frame

#rename column names of X_train using features data frame
#join y_train observations from numbers to the corresponding activity labels
#append y_train activity labels to X_train data frame
#append subject_train column to the X_train data frame

#combine transformed X_test and X_train by column name using rbind in order to stack data frames

#subset combined data frame to include only mean and std dev for each measurement

#create a new tidy data set with the average of each variable for each activity and each subject (group_by)

library(dplyr)

#rename column names of X_test using features data frame
X_test_colnames <- X_test %>% rename_at(vars(names(X_test)), function (x) features$V2)

#join y_test column V1 to the corresponding activity label names
y_test_ljoin <- left_join(y_test, activity_labels)
names(y_test_ljoin) <- c("V1", "Activity")

#append y_test activity labels to X_test data frame
Activity <- y_test_ljoin$Activity
X_test_bind_y <- cbind(X_test_colnames, Activity)

#rename subject_test column names for clarity
names(subject_test) <- c("Subject")

#append subject_test column to X_test data frame
X_test_bind_y_subj <- cbind(X_test_bind_y, subject_test)

#rename column names of X_train using features data frame
X_train_colnames <- X_train %>% rename_at(vars(names(X_train)), function (x) features$V2)

#join y_train column V1 to the corresponding activity label names
y_train_ljoin <- left_join(y_train, activity_labels)
names(y_train_ljoin) <- c("V1", "Activity")

#append y_test activity labels to X_test data frame
Activity <- y_train_ljoin$Activity
X_train_bind_y <- cbind(X_train_colnames, Activity)

#rename subject_test column names for clarity
names(subject_train) <- c("Subject")

#append subject_test column to X_test data frame
X_train_bind_y_subj <- cbind(X_train_bind_y, subject_train)

#combine transformed X_test and X_train by column name using rbind in order to stack data frames
X_test_train <- rbind(X_test_bind_y_subj, X_train_bind_y_subj)

#subset combined data frame to include only mean and std dev for each measurement
X_subset_mean_std <- X_test_train[,grepl("mean()|std()|Subject|Activity", colnames(X_test_train))]
X_subset <- X_subset_mean_std[,!grepl("Freq", colnames(X_subset_mean_std))]

#create a new tidy data set with the average of each variable for each activity and each subject (group_by)
X_avg <- X_subset %>% group_by(Activity, Subject) %>% summarise_all(mean)
print(X_avg)
#or alternatively:
#X_avg <- X_subset %>% group_by(Subject, Activity) %>% summarise_all(mean)
