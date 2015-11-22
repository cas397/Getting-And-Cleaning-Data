---
title: "README"
author: "Christian Segarra"
date: "November 21, 2015"
output: html_document
---

###Processing And Tidying Of Data
The code used to process and tidy the data does the following:

1. The data given in "train.txt" and "test.txt" had no column names assigned. So a vector containing the names of the features in "features.txt" was created. These names were then assigned to the columns of "train.txt" and "test.txt". They were assigned in the following fashion: row 1 of features was assigned to the first column, row 2 of features was assigned to the second column and so on.

2. The column in "subject_test.txt" and "subject_train.txt" was assigned the name "Subject". The column in "y_test.txt" and "y_train.txt" was assigned the name "Activity"

3. The data given in "train.txt" and "test.txt" also did not specify which Subject and Activity the data corresponded to. The number of rows in "subject_test.txt", "y_test.txt", and "test.txt" were all equivalent, so it was therefore assumed that row 1 of "subject_test.txt" corresponded with row 1 of "y_test.txt" and row 1 "test.txt". Row 2 of each file corresponded to each other and so on. Using this assumption, the column in "subject_test.txt" and the column in "y_test.txt" were appended as the first two columns to "test.txt". The same reasoning and process was used to append the column in "subject_train.txt" and "y_train.txt" to "train.txt".

4. The data in "test.txt" and "train.txt" was combined horizontally to create one data frame containing all of the training and test data.

5. The columns that contained the strings "mean" or "std" were extracted.

6. The values of the column "Activity" contained integers that corresponded to actual Activity names. The file containing these names, "activity_labels.txt" was read into a vector. The integers were then replaced with their corresponding labels.

7. Values were listed as variables. The gather function was used to create a key value pair, where the key was named "Feature". The "Subject" and "Activity" columns were left as is.

8. The group_by function was used to group the data by Subject, by Activity, by Feature. The summarize function was used to find the mean of each group's Feature value. The resulting summary column was named "Mean".

The code used to process and tidy the data can be find in run_Analysis.R