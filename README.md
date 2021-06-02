# pandas-challenge - Pandas Assignment - Data Analytics Bootcamp

## Pandas Homework - PyCitySchools

### Setting up folders in Github

1. Created a new repository for the project called pandas-challenge in Github. Cloned the repository to the local computer.

2. Created new directory within pandas-challenge called PyCitySchools

3. Inside the new directory, created a PyCitySchools_starter.ipynb file and a folder Resources to hold the csv files for schools and students.

4. Executed the pandas code for each step.

### PyCitySchools

   * Imported the pandas module.
```
import pandas as pd
```
  * Read the csv files into dataframes and merged the 2 files using field 'school_name'
```
school_data = pd.read_csv(school_data_to_load)
student_data = pd.read_csv(student_data_to_load)

school_data_complete = pd.merge(student_data, school_data, how="left", on=["school_name", "school_name"])
```

* Created a dataframe with the district summary using the merged dataframe above. 
  * The summary shows the total number of schools, total number of students, total budget, average math score, average reading score, percentage of students with a         passing math score, percentage of students with a passing reading score, percentage of students who passed math and reading. 
  * Calculated the total schools using the unique function
  * Calculated the total students using the count function 
  * Calculated the total budgets using the sum function
  * Calculated the average math score using the mean function
  * Calculated the average reading score using the mean function
  * Calculated the percentage of students who passed in math using the loc function to find the count of students with passing score of 70 and above and divided with       the total number of students.
  * Calculated the percentage of students who passed in reading using the loc function to find the count of students with passing score of 70 and above and divided         with the total number of students.
  * Calculated the percentage of students who passed in both math and reading using the loc function to find the count of students with passing score of 70 and above       in both subjects and divided with the total number of students.
  * Formatted the data using the map function

* Create a dataframe with the school summary grouping on the school name in the merged dataframe above. 
  * The summary shows the School Name, School Type, Total Students, Total School Budget, Per Student Budget, Average Math Score, Average Reading Score, % Passing           Math, % Passing Reading, % Overall Passing
  * Grouped the combined dataframe using the groupby function on school_name
  * Using the unique function, obtain the school type for each school name in the grouped dataframe
  * Calculated the total students for school using the count function
  * Retreived the total budgets for each school using max function
  * Calulated the budget per student by dividing the budget with the total number of students
  * Calculated the average math score using the mean function on the grouped dataframe
  * Calculated the average reading score using the mean function on the grouped dataframe
  * Calulated the percentage of students who passed math for each school by filtering the combined dataframe to contain only the students with passing math score of 70     and above. Grouping this on the school name and obtaining the number of students per school and dividing this by the total number of students.
  * Calulated the percentage of students who passed reading for each school by filtering the combined dataframe to contain only the students with passing reading score     of 70 and above. Grouping this on the school name and obtaining the number of students per school and dividing this by the total number of students.
  * Calulated the percentage of students who passed both math and reading for each school by filtering the combined dataframe to contain only the students with passing     math and reading score of 70 and above. Grouping this on the school name and obtaining the number of students per school and dividing this by the total number of       students.
  * Formatted the dataframe using the map function

* Using the sort_values function in descending order on column overall passing, obtained the top 5 performing school using head function

* Using the sort_values function in ascending order on column overall passing, obtained the bottom 5 performing school using head function

* Create a dataframe grouped by school_name with average Math scores by grades
  * Dataframe shows school_name, average math score of 9th grade, average math score of 10th grade, average math score of 11th grade and average math score of 12th         grade.
  * Using the loc method, retrieve data for the 9th grade students.
  * Grouping this dataframe using groupby function on school name and find the mean of the math score
  * Repeat the above for 10th grade, 11th grade and 12th grade.

* Create a dataframe grouped by school_name with average Reading scores by grades
  * Dataframe shows school_name, average reading score of 9th grade, average reading score of 10th grade, average reading score of 11th grade and average reading score     of 12th grade.
  * Using the loc method, retrieve data for the 9th grade students.
  * Grouping this dataframe using groupby function on school name and find the mean of the average score
  * Repeat the above for 10th grade, 11th grade and 12th grade.

* Create a dataframe to show scores by school spending
  * Dataframe shows the spending group, average math score, average reading score, % passing math, % passing reading and % overall passing
  * Added column 'size' to a copy of the school summary dataframe
  * Converted the 'per student budget' column into float.
  * Created 4 bins to group 'school spending' and created corresponding labels as 0-585, 585-630, 630-645 and 645-680 dollars
  * Using pd.cut() function, created a new data series for the spending group based on the bins and labels applied to the 'per student budget' column
  * Did a groupby on the spending group and created new dataframe and formatted using map function
  * Formatted the columns using the map function

* Create a dataframe to show scores by school size
  * Dataframe shows the school size, average math score, average reading score, % passing math, % passing reading and % overall passing
  * Created 3 bins to group 'school size' and created corresponding labels as less than 1000, 1000 - 2000 and 2000 - 5000.
  * Using pd.cut() function, created a new data series for the size group based on the bins and labels applied to the 'size' column
  * Did a groupby on the size_group and created new dataframe and formatted using map function
 * Formatted the columns using the map function

* Create a dataframe to show scores by school type
  * Dataframe shows the school type, average math score, average reading score, % passing math, % passing reading and % overall passing
  * Groupby the copy of the school summary dataframe by school type and calculated the mean
  * Formatted the columns using the map function

## Observations
* Charter schools have higher overall passing percentage. All the top 5 performing schools are charter schools. All 8 Charter schools have close to 90% students   passing in both maths and reading. Whereas, all district schools have only close to 50% students passing both maths and reading.

* Small and medium sized schools have better overall performance. Larger schools with over 2000 students have lesser overall passing percentage, with the exception of   Wilson High School, which is a charter school and is among the top 5 performing schools. This again shows the charter schools are better performing.

* Schools with lower budget per student are found to be better performing. Here we can see again that district schools fall under the 630-645 dollars or 645-680   dollars higher spending per student group. Thomas High School, which is a charter school, with a per student spending 630-645 dollars is still found to be performing   well. 

