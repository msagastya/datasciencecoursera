# run_analysis.R


## Description
The `run_analysis.R` script performs data preparation and analysis on the UCI HAR Dataset, following a set of five steps outlined in the course project's instructions.


## Steps


1. **Download the dataset**


   The dataset is downloaded from an online source and extracted into a folder named "UCI HAR Dataset".


2. **Assign data to variables**


   Various data files are assigned to specific variables:
   - `features`: features.txt (561 rows, 2 columns)
     - Contains the selected features from the accelerometer and gyroscope signals.
   - `activities`: activity_labels.txt (6 rows, 2 columns)
     - Lists the activities performed and their corresponding codes.
   - `subject_test`: test/subject_test.txt (2947 rows, 1 column)
     - Contains the test data of volunteer test subjects.
   - `x_test`: test/X_test.txt (2947 rows, 561 columns)
     - Includes the recorded features test data.
   - `y_test`: test/y_test.txt (2947 rows, 1 column)
     - Holds the test data of activity codes.
   - `subject_train`: train/subject_train.txt (7352 rows, 1 column)
     - Contains the train data of volunteer subjects.
   - `x_train`: train/X_train.txt (7352 rows, 561 columns)
     - Includes the recorded features train data.
   - `y_train`: train/y_train.txt (7352 rows, 1 column)
     - Holds the train data of activity codes.


3. **Merge training and test sets**


   The script merges the training and test datasets to create one dataset:
   - `X` (10299 rows, 561 columns) combines `x_train` and `x_test` using the `rbind()` function.
   - `Y` (10299 rows, 1 column) combines `y_train` and `y_test` using `rbind()`.
   - `Subject` (10299 rows, 1 column) combines `subject_train` and `subject_test` using `rbind()`.
   - `Merged_Data` (10299 rows, 563 columns) merges `Subject`, `Y`, and `X` using `cbind()`.


4. **Extract mean and standard deviation measurements**


   A subset of the merged dataset, named `TidyData`, is created by selecting columns related to mean and standard deviation measurements:
   - Includes columns for subject, code, and relevant mean and standard deviation (std) measurements.


5. **Label activities and variables descriptively**


   The script replaces activity codes in `TidyData` with descriptive activity names from the `activities` variable. Variable names in `TidyData` are also appropriately labeled:
   - `code` column is renamed to `activities`.
   - Abbreviations and prefixes in variable names are expanded for clarity.


6. **Create a second tidy dataset with averages**


   The script generates a second independent tidy dataset, `FinalData`, by summarizing `TidyData`. The dataset calculates the average of each variable for each activity and subject, after grouping by subject and activity.
   - `FinalData` has 180 rows and 88 columns.


7. **Export FinalData**


   `FinalData` is exported as a text file named "FinalData.txt".
