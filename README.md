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
  * Read the csv files into dataframes and merge the 2 files using field 'school_name'
```
school_data = pd.read_csv(school_data_to_load)
student_data = pd.read_csv(student_data_to_load)

school_data_complete = pd.merge(student_data, school_data, how="left", on=["school_name", "school_name"])
```
* Create a dataframe with the district summary using the merged dataframe above. 
  ** The summary shows the total number of schools, total number of students, total budget, average math score, average reading score,      percentage of students with a passing math score, percentage of students with a passing reading score, percentage of students who      passed math and reading. 
```
# Calculate total schools
total_schools_district = len(school_data_complete['school_name'].unique())

# Calculate total students
total_students_district = school_data_complete['student_name'].count()

# Calculate total budgets
total_budget_district = (school_data_complete.groupby(['school_name'])['budget'].max()).sum()

# Calculate average math score
average_math_district = school_data_complete['math_score'].mean()

# Calculate average reading score
average_reading_district = school_data_complete['reading_score'].mean()

# Calculate percentage of students who passed in math
student_pass_math_district = school_data_complete.loc[school_data_complete['math_score'] >= 70, 'student_name'].count()
percentage_math_district = (student_pass_math_district/total_students_district) * 100

# Calculate percentage of students who passed in reading
student_pass_reading_district = school_data_complete.loc[school_data_complete['reading_score'] >= 70, 'student_name'].count()
percentage_reading_district = (student_pass_reading_district/total_students_district) * 100

# Calculate percentage of students who passed in both math and reading
student_pass_both_district = school_data_complete.loc[(school_data_complete['reading_score'] >= 70) 
                                             & (school_data_complete['math_score'] >= 70),'student_name'].count()
percentage_both_district = (student_pass_both_district/total_students_district) * 100
```
* Create the dataframe and format
```
# Create a dataframe to hold the above results and format 
district_summary = pd.DataFrame({'Total Schools': total_schools_district,
                               'Total Students' : total_students_district,
                               'Total Budget': total_budget_district,
                               'Average Math Score': average_math_district,
                               'Average Reading Score': average_reading_district,
                               '% Passing Math': percentage_math_district,
                               '% Passing Reading': percentage_reading_district,
                               '% Overall Passing': percentage_both_district}, index=[0])

district_summary['Total Students'] = district_summary['Total Students'].map("{:,}".format)
district_summary['Total Budget'] = district_summary['Total Budget'].map("${:,.2f}".format)
district_summary['Average Math Score'] = district_summary['Average Math Score'].map("{:.2f}".format)
district_summary['Average Reading Score'] = district_summary['Average Reading Score'].map("{:.2f}".format)
district_summary['% Passing Math'] = district_summary['% Passing Math'].map("{:.2f}".format)
district_summary['% Passing Reading'] = district_summary['% Passing Reading'].map("{:.2f}".format)
district_summary['% Overall Passing'] = district_summary['% Overall Passing'].map("{:.2f}".format)
```
* Create a dataframe with the school summary grouping by on the school name in the merged dataframe above. 
  ** The summary shows the School Name, School Type, Total Students, Total School Budget, Per Student Budget, Average Math Score,      Average Reading Score, % Passing Mathing, % Passing Reading, % Overall Passing
```
# Groupby the combined dataframe by the school name
grouped_school_df = school_data_complete.groupby(['school_name'])

# Get the School type for school_name group
school_type = grouped_school_df['type'].unique().str.get(0)

# Get the total students for school_name group
total_students_school = grouped_school_df['Student ID'].count()

# Get the total budgets for school_name group
total_school_budget_school = grouped_school_df['budget'].max()

# Get the budget per student for school_name group
per_student_budget_school = (grouped_school_df['budget'].max())/total_students_school

# Get the average math score for school_name group
average_math_school = grouped_school_df['math_score'].mean()

# Get the average reading score for school_name group
average_reading_school = grouped_school_df['reading_score'].mean()

# Get the percentage of students who passed math for school_name group
studentpass_math_school = school_data_complete[school_data_complete['math_score'] >= 70].groupby(['school_name'])['Student ID'].count()
percentage_math_school = (studentpass_math_school/total_students_school)*100

# Get the percentage of students who passed reading for school_name group
studentpass_reading_school = school_data_complete[school_data_complete['reading_score'] >= 70].groupby(['school_name'])['Student ID'].count()
percentage_reading_school = (studentpass_reading_school/total_students_school)*100

# Get the percentage of students who passed both math and reading for school_name group
studentpass_both_school = school_data_complete[(school_data_complete['reading_score'] >= 70) 
                                                  & (school_data_complete['math_score'] >= 70)].groupby(['school_name'])['Student ID'].count()
percentage_both_school = (studentpass_both_school/total_students_school)*100

```
* Create the dataframe and format. 
```
# Create new dataframe and format
school_summary = pd.DataFrame({'School Type': school_type, 
                              'Total Students': total_students_school,
                              'Total School Budget': total_school_budget_school,
                              'Per Student Budget': per_student_budget_school,
                              'Average Math Score': average_math_school,
                              'Average Reading Score': average_reading_school,
                              '% Passing Math': percentage_math_school,
                              '% Passing Reading': percentage_reading_school,
                              '% Overall Passing': percentage_both_school})

school_summary['Total School Budget'] = school_summary['Total School Budget'].map("${:,.2f}".format)
school_summary['Per Student Budget'] = school_summary['Per Student Budget'].map("${:,.2f}".format)
```