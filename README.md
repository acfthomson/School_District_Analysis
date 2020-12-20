# School_District_Analysis

A school board hired a consulting firm to analyze student data because of suspected academic dishonesty.  [students_complete.csv](https://github.com/acfthomson/School_District_Analysis/blob/main/students_complete.csv) shows evidence of reading and math grade for Thomas High School ninth graders appears to have been altered.  The school board does not know the full extent of the academic dishonesty , and in order to uphold state testing standard, they have hired this firm for help.

The analysis conducted compares previous school district analysis against this firm's analysis in order to determine how the suspected academic dishonesty affects school performance.

The school board has requested the following deliverables:
- A high-level snapshot of the district's key metrics, presented in a table format
- An overview of the key metrics for each school, presented in a table format
- Tables presenting each of the following metrics:
    - Top 5 and bottom 5 performing schools, based on the overall passing rate
    - The average math score received by students in each grade level at each school
    - The average reading score received by students in each grade level at each school
    - School performance based on the budget per student
    - School performance based on the school size 
    - School performance based on the type of school


## Development Environment
 - Jupyter Notebook
 - Python v3.7.x
    - Dependencies
        - Python Pandas library
        - Python Numpy library


## Resources
 - [schools_complete.csv](https://github.com/acfthomson/School_District_Analysis/tree/main/Resources/schools_complete.csv)
 - [students_complete.csv](https://github.com/acfthomson/School_District_Analysis/tree/main/Resources/students_complete.csv)
 
 
## Results

### District Summary


[![New-District-Summary.png](https://i.postimg.cc/vHXsj0Dk/New-District-Summary.png)](https://postimg.cc/VdSp0BqW)




### School Summary


[![New-Per-School-Summary.png](https://i.postimg.cc/13PHdZfc/New-Per-School-Summary.png)](https://postimg.cc/jLgPWm6L)




### Thomas High School Scores
Math and reading scores for ninth graders at Thomas High School were replaced with 'NaN' (Not a Number) so that their scores would not affect future calculations.  If all of the students' scores were replaced with a 'O', then this would negatively impact averages for the school and school district.

### Thomas High School math scores:
Ninth grade math scores were replaced with NaN.  Thomas High School 10th, 11th, and 12th grade math scores are as follows: 83.1, 83.5, and 83.5.

[![Thomas-High-School-Math-Scores.png](https://i.postimg.cc/WzTzvSrK/Thomas-High-School-Math-Scores.png)](https://postimg.cc/R6p417gQ)


### Thomas High School reading scores:
Ninth grade math scores were replaced with NaN.  Thomas High School 10th, 11th, and 12th grade reading scores are as follows: 84.3, 83.6, and 83.8.

[![Thomas-High-School-Reading-Scores.png](https://i.postimg.cc/2y9DKxxn/Thomas-High-School-Reading-Scores.png)](https://postimg.cc/8fv9FM9C)


### Scores by School Spending
District spending per school was calculated by determining average spending ($620), standard deviation (~30), minimum spending amount ($578), lower quartile ($592), mid quartile ($628), upper quartile ($642), and mximum spending amount ($655) across all 15 schools:

```python
per_school_capita.describe()
count     15.000000
mean     620.066667
std       28.544368
min      578.000000
25%      591.500000
50%      628.000000
75%      641.500000
max      655.000000
dtype: float64
```

Based on the figures given by the .describe() method, spending ranges per student in the school district were determined:
$0-550
$551-600
$601-650
$651-700

```python
# Establish the spending bins and group names.
per_school_capita.describe()
per_school_capita
spending_bins = [0, 550, 600, 650, 700]
per_school_capita.groupby(pd.cut(per_school_capita, spending_bins)).count()
bin_names = ["$0-550", "$551-600", "$601-650", "651-700"]

# Categorize spending based on the bins.
per_school_summary_df["Spending Ranges (Per Student)"] = pd.cut(per_school_capita, spending_bins, labels=bin_names)
```

Schools that spent between $551-600 appear to have the best-performing students in math and reading.
[![New-Scores-by-School-Spending.png](https://i.postimg.cc/G25BkvsS/New-Scores-by-School-Spending.png)](https://postimg.cc/HcbsmczQ)




### Scores by School Size
Scores by school size were calculated by determining size ranges for all 15 schools in the district:
Small (<1000)
Medium (1000-2000)
Large (2000-5000)

```python
# Establish the bins.
size_bins = [0, 1000, 2000, 5000]
group_names = ["Small (<1000)", "Medium (1000-2000)", "Large (2000-5000)"]

# Categorize spending based on the bins.
per_school_summary_df["School Size"] = pd.cut(per_school_summary_df["Total Students"], size_bins, labels=group_names)
```

Small- and medium-sized schools in this district are very close in performance. 
[![New-Scores-By-School-Size.png](https://i.postimg.cc/KjQJxqKs/New-Scores-By-School-Size.png)](https://postimg.cc/N291xxk1)



### Scores by School Type
Schools were either charter or district schools.  Unsurprisingly, charter schools performed better than district schools.

[![New-Scores-by-School-Type.png](https://i.postimg.cc/pTjLw4SR/New-Scores-by-School-Type.png)](https://postimg.cc/vgQy9qMN)

 
 
 ## Summary
Removing 9th grade student scores from Thomas High School affected the school district in the following ways:
- Average math scores dropped slightly (<1%)
- Average reading scores were not affected
- Percentage of students passing math dropped slightly (-1%)
- Percentage of students passing reading dropped slightle (-1%)
- The overall passing rate dropped (-1%)

Only scores for Thomas High School were affected:
- Perentage of students passing math dropped from 93.2% to 66.9%
- Percentage of students passing reading dropped from 97.3% to 69.7%
- Overall passing percentage dropped from 90.9% to 65.1%

Thomas High School affected school rankings in the following ways:
- Thomas High school dropped out of the top 5 high schools in the district
- Wright High School moved into the top 5 high schools in the district
- Bottom 5 high schools was unaffected

Removing 9th grade student scores from Thomas High School affected other reports:
- Math and reading scores by grade remained the same for all other schools
- Thomas High School had no data to report for 9th grade math and reading scores
- Scores by school spending chaged at the $601-650 range:
    - Percentage passing math dropped from 73% to 67%
    - Percentage passing reading dropped from 84% to 77%
    - Overall passing percentage dropped from 63% to 56%
- Scores by school size changed for medium-sized schools (1000-2000):
    - Percentage passing math dropped from 94% to 85%
    - Percentage passing reading dropped from 97% to 91%
    - Overall passing percentage dropped from 91% to 85%
- Scores by schools type were affected in the following ways:
    - Percentage passing math dropped from 94% to 90%
    - Percentage passing reading dropped from 97% to 93%
    - Overall passing percentage dropped from 90% to 87%

