## PyCity Schools Analysis

Observation 1: While it may be easy to assume so, based on the data for the top five highest and lowest performing schools, there does not appear to be a correlation between the budget allocated per student. The average budget per student was higher among the lower performing schools then in the schools that performed better. Just because a school is more well-funded does not necessarily mean that the students will perform better.

Observation 2: Class size and the number of students does affect the passing rate and how students perform. Comparing the highest and lowest performing schools, the lower performing schools consistently had a larger number of students, while the schools that performed well had a smaller student population.

Observation 3: Overall Charter schools performed better than District schools. This may be due to Charter schools, on average, having a smaller student population that District schools, which would positively impact performance. Charter schools had a higher passing percentage in both reading and math, leading to a high overall passing percentage.


```python
#dependencies
import os
import pandas as pd
import numpy as np
```


```python
#create schools df
schools_complete = os.path.join('..','PandasHW','raw_data','schools_complete.csv')
schools_complete_df = pd.read_csv(schools_complete, encoding = "ISO-8859-1")

schools_complete_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
    </tr>
  </tbody>
</table>
</div>




```python
#create students df
students_complete = os.path.join('..','PandasHW','raw_data','students_complete.csv')
students_complete_df = pd.read_csv(students_complete, encoding = "ISO-8859-1")

students_complete_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
#total school
total_schools = students_complete_df["school"].nunique()
total_schools

#total students
total_students = students_complete_df["name"].count()
total_students

#total budget
total_budget = schools_complete_df["budget"].sum()
total_budget

#average math score
avg_math = students_complete_df["math_score"].mean()
avg_math

#average reading score
avg_reading = students_complete_df["reading_score"].mean()
avg_reading

# % passing math
pass_math = students_complete_df.loc[students_complete_df['math_score'] >= 70]
pass_math_total = pass_math["math_score"].count()/total_students*100
pass_math_total

# % passing reading
pass_reading = students_complete_df.loc[students_complete_df['reading_score'] >= 70]
pass_reading_total = pass_reading["reading_score"].count()/total_students*100
pass_reading_total

#overall passing rate
overall_pass = (pass_reading_total + pass_math_total)/2
overall_pass

#snapshot table
district_snapshot = pd.DataFrame({'Total School': [total_schools], 'Total Students':[total_students], 'Total Budget':[total_budget], 
                     'Average Math Score':[avg_math], 'Average Reading Score':[avg_reading],
                     '% Passing Math':[pass_math_total], '% Passing Reading':[pass_reading_total], 
                                  '% Overall Passing Rate':[overall_pass]})
district_snapshot['Total Budget'] = district_snapshot['Total Budget'].map('${:,.2f}'.format)
district_snapshot

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>% Overall Passing Rate</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Total Budget</th>
      <th>Total School</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>80.393158</td>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>$24,649,428.00</td>
      <td>15</td>
      <td>39170</td>
    </tr>
  </tbody>
</table>
</div>




```python
#School Overview

#average math score

huang_high = students_complete_df.loc[students_complete_df['school'] == "Huang High School"]
huang_high_mavg = huang_high["math_score"].mean()
huang_high_mavg

huang_math = huang_high.loc[huang_high["math_score"] >= 70]
huang_math_total = huang_math["math_score"].count()/2917*100
huang_math_total

fig_high = students_complete_df.loc[students_complete_df['school'] == "Figueroa High School"]
fig_high_mavg = fig_high["math_score"].mean()
fig_high_mavg

fig_math = fig_high.loc[fig_high["math_score"] >= 70]
fig_math_total = fig_math["math_score"].count()/2949*100
fig_math_total

shelton_high = students_complete_df.loc[students_complete_df['school'] == "Shelton High School"]
shelton_high_mavg = shelton_high["math_score"].mean()
shelton_high_mavg

shelton_math = shelton_high.loc[shelton_high["math_score"] >= 70]
shelton_math_total = shelton_math["math_score"].count()/1761*100
shelton_math_total

hernandez_high = students_complete_df.loc[students_complete_df['school'] == "Hernandez High School"]
hernandez_high_mavg = hernandez_high["math_score"].mean()
hernandez_high_mavg

hernandez_math = hernandez_high.loc[hernandez_high["math_score"] >= 70]
hernandez_math_total = hernandez_math["math_score"].count()/4635*100
hernandez_math_total

griffin_high = students_complete_df.loc[students_complete_df['school'] == "Griffin High School"]
griffin_high_mavg = griffin_high["math_score"].mean()
griffin_high_mavg

griffin_math = griffin_high.loc[griffin_high["math_score"] >= 70]
griffin_math_total = griffin_math["math_score"].count()/1468*100
griffin_math_total

Wilson_high = students_complete_df.loc[students_complete_df['school'] == "Wilson High School"]
Wilson_high_mavg = Wilson_high["math_score"].mean()
Wilson_high_mavg

Wilson_math = Wilson_high.loc[Wilson_high["math_score"] >= 70]
Wilson_math_total = Wilson_math["math_score"].count()/2283*100
Wilson_math_total

Cabrera_high = students_complete_df.loc[students_complete_df['school'] == "Cabrera High School"]
Cabrera_high_mavg = Cabrera_high["math_score"].mean()
Cabrera_high_mavg

Cabrera_math = Cabrera_high.loc[Cabrera_high["math_score"] >= 70]
Cabrera_math_total = Cabrera_math["math_score"].count()/1858*100
Cabrera_math_total

Bailey_high = students_complete_df.loc[students_complete_df['school'] == "Bailey High School"]
Bailey_high_mavg = Bailey_high["math_score"].mean()
Bailey_high_mavg

Bailey_math = Bailey_high.loc[Bailey_high["math_score"] >= 70]
Bailey_math_total = Bailey_math["math_score"].count()/4976*100
Bailey_math_total

Holden_high = students_complete_df.loc[students_complete_df['school'] == "Holden High School"]
Holden_high_mavg = Holden_high["math_score"].mean()
Holden_high_mavg

Holden_math = Holden_high.loc[Holden_high["math_score"] >= 70]
Holden_math_total = Holden_math["math_score"].count()/427*100
Holden_math_total

Pena_high = students_complete_df.loc[students_complete_df['school'] == "Pena High School"]
Pena_high_mavg = Pena_high["math_score"].mean()
Pena_high_mavg

Pena_math = Pena_high.loc[Pena_high["math_score"] >= 70]
Pena_math_total = Pena_math["math_score"].count()/962*100
Pena_math_total

Wright_high = students_complete_df.loc[students_complete_df['school'] == "Wright High School"]
Wright_high_mavg = Wright_high["math_score"].mean()
Wright_high_mavg

Wright_math = Wright_high.loc[Wright_high["math_score"] >= 70]
Wright_math_total = Wright_math["math_score"].count()/1800*100
Wright_math_total

Rodriguez_high = students_complete_df.loc[students_complete_df['school'] == "Rodriguez High School"]
Rodriguez_high_mavg = Rodriguez_high["math_score"].mean()
Rodriguez_high_mavg

Rodriguez_math = Rodriguez_high.loc[Rodriguez_high["math_score"] >= 70]
Rodriguez_math_total = Rodriguez_math["math_score"].count()/3999*100
Rodriguez_math_total

Johnson_high = students_complete_df.loc[students_complete_df['school'] == "Johnson High School"]
Johnson_high_mavg = Johnson_high["math_score"].mean()
Johnson_high_mavg

Johnson_math = Johnson_high.loc[Johnson_high["math_score"] >= 70]
Johnson_math_total = Johnson_math["math_score"].count()/4761*100
Johnson_math_total

Ford_high = students_complete_df.loc[students_complete_df['school'] == "Ford High School"]
Ford_high_mavg = Ford_high["math_score"].mean()
Ford_high_mavg

Ford_math = Ford_high.loc[Ford_high["math_score"] >= 70]
Ford_math_total = Ford_math["math_score"].count()/2739*100
Ford_math_total

Thomas_high = students_complete_df.loc[students_complete_df['school'] == "Thomas High School"]
Thomas_high_mavg = Thomas_high["math_score"].mean()
Thomas_high_mavg

Thomas_math = Thomas_high.loc[Thomas_high["math_score"] >= 70]
Thomas_math_total = Thomas_math["math_score"].count()/1635*100
Thomas_math_total

#average reading score

huang_high = students_complete_df.loc[students_complete_df['school'] == "Huang High School"]
huang_high_ravg = huang_high["reading_score"].mean()
huang_high_ravg

huang_read = huang_high.loc[huang_high["reading_score"] >= 70]
huang_read_total = huang_read["reading_score"].count()/2917*100
huang_read_total

fig_high = students_complete_df.loc[students_complete_df['school'] == "Figueroa High School"]
fig_high_ravg = fig_high["reading_score"].mean()
fig_high_ravg

fig_read = fig_high.loc[fig_high["reading_score"] >= 70]
fig_read_total = fig_read["reading_score"].count()/2949*100
fig_read_total

shelton_high = students_complete_df.loc[students_complete_df['school'] == "Shelton High School"]
shelton_high_ravg = shelton_high["reading_score"].mean()
shelton_high_ravg

shelton_read = shelton_high.loc[shelton_high["reading_score"] >= 70]
shelton_read_total = shelton_read["reading_score"].count()/1761*100
shelton_read_total

hernandez_high = students_complete_df.loc[students_complete_df['school'] == "Hernandez High School"]
hernandez_high_ravg = hernandez_high["reading_score"].mean()
hernandez_high_ravg

hernandez_read = hernandez_high.loc[hernandez_high["reading_score"] >= 70]
hernandez_read_total = hernandez_read["reading_score"].count()/4635*100
hernandez_read_total

griffin_high = students_complete_df.loc[students_complete_df['school'] == "Griffin High School"]
griffin_high_ravg = griffin_high["reading_score"].mean()
griffin_high_ravg

griffin_read = griffin_high.loc[griffin_high["reading_score"] >= 70]
griffin_read_total = griffin_read["reading_score"].count()/1468*100
griffin_read_total

Wilson_high = students_complete_df.loc[students_complete_df['school'] == "Wilson High School"]
Wilson_high_ravg = Wilson_high["reading_score"].mean()
Wilson_high_ravg

Wilson_read = Wilson_high.loc[Wilson_high["reading_score"] >= 70]
Wilson_read_total = Wilson_read["reading_score"].count()/2283*100
Wilson_read_total

Cabrera_high = students_complete_df.loc[students_complete_df['school'] == "Cabrera High School"]
Cabrera_high_ravg = Cabrera_high["reading_score"].mean()
Cabrera_high_ravg

Cabrera_read = Cabrera_high.loc[Cabrera_high["reading_score"] >= 70]
Cabrera_read_total = Cabrera_read["reading_score"].count()/1858*100
Cabrera_read_total

Bailey_high = students_complete_df.loc[students_complete_df['school'] == "Bailey High School"]
Bailey_high_ravg = Bailey_high["reading_score"].mean()
Bailey_high_ravg

Bailey_read = Bailey_high.loc[Bailey_high["reading_score"] >= 70]
Bailey_read_total = Bailey_read["reading_score"].count()/4976*100
Bailey_read_total

Holden_high = students_complete_df.loc[students_complete_df['school'] == "Holden High School"]
Holden_high_ravg = Holden_high["reading_score"].mean()
Holden_high_ravg

Holden_read = Holden_high.loc[Holden_high["reading_score"] >= 70]
Holden_read_total = Holden_read["reading_score"].count()/427*100
Holden_read_total

Pena_high = students_complete_df.loc[students_complete_df['school'] == "Pena High School"]
Pena_high_ravg = Pena_high["reading_score"].mean()
Pena_high_ravg

Pena_read = Pena_high.loc[Pena_high["reading_score"] >= 70]
Pena_read_total = Pena_read["reading_score"].count()/962*100
Pena_read_total

Wright_high = students_complete_df.loc[students_complete_df['school'] == "Wright High School"]
Wright_high_ravg = Wright_high["reading_score"].mean()
Wright_high_ravg

Wright_read = Wright_high.loc[Wright_high["reading_score"] >= 70]
Wright_read_total = Wright_read["reading_score"].count()/1800*100
Wright_read_total

Rodriguez_high = students_complete_df.loc[students_complete_df['school'] == "Rodriguez High School"]
Rodriguez_high_ravg = Rodriguez_high["reading_score"].mean()
Rodriguez_high_ravg

Rodriguez_read = Rodriguez_high.loc[Rodriguez_high["reading_score"] >= 70]
Rodriguez_read_total = Rodriguez_read["reading_score"].count()/3999*100
Rodriguez_read_total

Johnson_high = students_complete_df.loc[students_complete_df['school'] == "Johnson High School"]
Johnson_high_ravg = Johnson_high["reading_score"].mean()
Johnson_high_ravg

Johnson_read = Johnson_high.loc[Johnson_high["reading_score"] >= 70]
Johnson_read_total = Johnson_read["reading_score"].count()/4761*100
Johnson_read_total

Ford_high = students_complete_df.loc[students_complete_df['school'] == "Ford High School"]
Ford_high_ravg = Ford_high["reading_score"].mean()
Ford_high_ravg

Ford_read = Ford_high.loc[Ford_high["reading_score"] >= 70]
Ford_read_total = Ford_math["reading_score"].count()/2739*100
Ford_read_total

Thomas_high = students_complete_df.loc[students_complete_df['school'] == "Thomas High School"]
Thomas_high_ravg = Thomas_high["reading_score"].mean()
Thomas_high_ravg

Thomas_read = Thomas_high.loc[Thomas_high["reading_score"] >= 70]
Thomas_read_total = Thomas_read["reading_score"].count()/1635*100
Thomas_read_total

#

schools_overview_df = schools_complete_df

schools_overview_df["Budget Per Student"] = schools_complete_df["budget"]/schools_complete_df["size"]

#average math score
schools_overview_df["Average Math Score"] = [huang_high_mavg, fig_high_mavg, shelton_high_mavg, 
                                             hernandez_high_mavg, griffin_high_mavg, Wilson_high_mavg, 
                                             Cabrera_high_mavg, Bailey_high_mavg, Holden_high_mavg, 
                                             Pena_high_mavg, Wright_high_mavg, Rodriguez_high_mavg,
                                           Johnson_high_mavg, Ford_high_mavg, Thomas_high_mavg]
#average reading score
schools_overview_df["Average Reading Score"] = [huang_high_ravg, fig_high_ravg, shelton_high_ravg, 
                                            hernandez_high_ravg, griffin_high_ravg, Wilson_high_ravg, 
                                             Cabrera_high_ravg, Bailey_high_ravg, Holden_high_ravg, 
                                             Pena_high_ravg, Wright_high_ravg, Rodriguez_high_ravg,
                                            Johnson_high_ravg, Ford_high_ravg, Thomas_high_ravg]

# % Passing Math
schools_overview_df["% Passing Math"] = [huang_math_total, fig_math_total, shelton_math_total, 
                                             hernandez_math_total, griffin_math_total, Wilson_math_total, 
                                             Cabrera_math_total, Bailey_math_total, Holden_math_total, 
                                             Pena_math_total, Wright_math_total, Rodriguez_math_total,
                                           Johnson_math_total, Ford_math_total, Thomas_math_total]

# % Passing Reading
schools_overview_df["% Passing Reading"] = [huang_read_total, fig_read_total, shelton_read_total, 
                                             hernandez_read_total, griffin_read_total, Wilson_read_total, 
                                             Cabrera_read_total, Bailey_read_total, Holden_read_total, 
                                             Pena_read_total, Wright_read_total, Rodriguez_read_total,
                                           Johnson_read_total, Ford_read_total, Thomas_read_total]

#overall passing rate
schools_overview_df["% Overall Passing"] = [(huang_math_total + huang_read_total)/2, 
                                            (fig_math_total + fig_read_total)/2,
                                           (shelton_math_total + shelton_read_total)/2,
                                           (hernandez_math_total + hernandez_read_total)/2,
                                           (griffin_math_total + griffin_read_total)/2,
                                           (Wilson_math_total + Wilson_read_total)/2,
                                           (Cabrera_math_total + Cabrera_read_total)/2,
                                           (Bailey_math_total + Bailey_read_total)/2,
                                           (Holden_math_total + Holden_read_total)/2,
                                           (Pena_math_total + Pena_read_total)/2,
                                           (Wright_math_total + Wright_read_total)/2,
                                           (Rodriguez_math_total + Rodriguez_read_total)/2,
                                           (Johnson_math_total + Johnson_read_total)/2,
                                           (Ford_math_total + Ford_read_total)/2,
                                           (Thomas_math_total + Thomas_read_total)/2]

#rename columns
school_overview = schools_overview_df.rename(columns={"size":"Total Students", "budget":"Total Budget",
                                                      "name":"School Name", "type":"Type"})

#formatting Total Budget column to currency
school_overview['Total Budget'] = school_overview['Total Budget'].map('${:,.2f}'.format)

#setting index of df for School Name
school_overview_final = school_overview.set_index('School Name')

school_overview_final


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>Type</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Huang High School</th>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635.00</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>2</td>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600.00</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>3</td>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020.00</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574.00</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Bailey High School</th>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>$3,124,928.00</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>8</td>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087.00</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858.00</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>10</td>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400.00</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>94.972222</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650.00</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>68.309602</td>
      <td>68.309602</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>$1,043,130.00</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
  </tbody>
</table>
</div>




```python
#top 5 performing schools 
top5_schools = school_overview.loc[school_overview["% Overall Passing"] >= 95]
top5 = top5_schools.set_index('School Name')
top5


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>Type</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Griffin High School</th>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574.00</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858.00</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>$1,043,130.00</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
  </tbody>
</table>
</div>




```python
#bottom 5 performing schools
bottom5_schools = school_overview.loc[school_overview["% Overall Passing"] <= 73.8]
bottom5 = bottom5_schools.set_index('School Name')
bottom5
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>Type</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Huang High School</th>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635.00</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650.00</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>68.309602</td>
      <td>68.309602</td>
    </tr>
  </tbody>
</table>
</div>




```python
#average Math Score for students of each grade level (9th, 10th, 11th, 12th) 

school_grade = students_complete_df.set_index('school')
school_math_grade = school_grade.pivot_table(values='math_score', index=school_grade.index, columns='grade', aggfunc='mean')
school_math_grade


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>grade</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
      <th>9th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
      <td>77.083676</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
      <td>83.094697</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
      <td>76.403037</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
      <td>77.361345</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
      <td>82.044010</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
      <td>77.438495</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
      <td>83.787402</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
      <td>77.027251</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
      <td>77.187857</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
      <td>83.625455</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
      <td>76.859966</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
      <td>83.420755</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
      <td>83.590022</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
      <td>83.085578</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
      <td>83.264706</td>
    </tr>
  </tbody>
</table>
</div>




```python
#average Reading Score for students of each grade level (9th, 10th, 11th, 12th) 

school_grade = students_complete_df.set_index('school')
school_read_grade = school_grade.pivot_table(values='reading_score', index=school_grade.index, columns='grade', aggfunc='mean')
school_read_grade
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>grade</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
      <th>9th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
      <td>81.303155</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
      <td>83.676136</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
      <td>81.198598</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
      <td>80.632653</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
      <td>83.369193</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
      <td>80.866860</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
      <td>83.677165</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
      <td>81.290284</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
      <td>81.260714</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
      <td>83.807273</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
      <td>80.993127</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
      <td>84.122642</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
      <td>83.728850</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
      <td>83.939778</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
      <td>83.833333</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a table that breaks down school performances based on average Spending Ranges (Per Student). 
# Use 4 reasonable bins to group school spending. Include in the table each of the following: Average Math Score,
# Average Reading Score, % Passing Math, % Passing Reading, Overall Passing Rate (Average of the above two)

bins = [0, 585, 620, 650, 675]
group_names = ["<$585", "$585-620", "$620-650", "$650-675"]
pd.cut(school_overview_final["Budget Per Student"], bins, labels=group_names)

school_overview_final["Spending Range"] = pd.cut(school_overview_final["Budget Per Student"], bins, labels=group_names)
school_overview_final

spending_range = school_overview_final.groupby("Spending Range")
spending_range_final = spending_range.mean()

spending_range_final[["Average Math Score", "Average Reading Score", "% Passing Math", "% Passing Reading", "% Overall Passing"]]



```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>Spending Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.455399</td>
      <td>83.933814</td>
      <td>93.460096</td>
      <td>96.610877</td>
      <td>95.035486</td>
    </tr>
    <tr>
      <th>$585-620</th>
      <td>83.599686</td>
      <td>83.885211</td>
      <td>94.230858</td>
      <td>95.900287</td>
      <td>95.065572</td>
    </tr>
    <tr>
      <th>$620-650</th>
      <td>78.792545</td>
      <td>81.759287</td>
      <td>74.295260</td>
      <td>83.838919</td>
      <td>79.067090</td>
    </tr>
    <tr>
      <th>$650-675</th>
      <td>76.959583</td>
      <td>81.058567</td>
      <td>66.218444</td>
      <td>81.089710</td>
      <td>73.654077</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Repeat the above breakdown, but this time group schools based on a reasonable approximation of school size 
#(Small, Medium, Large).

bins = [0, 1000, 3000, 5000]
group_names = ["Small", "Medium", "Large"]
pd.cut(school_overview_final["Total Students"], bins, labels=group_names)

school_overview_final["Student Population"] = pd.cut(school_overview_final["Total Students"], bins, labels=group_names)
school_overview_final

student_population = school_overview_final.groupby("Student Population")
student_population_final = student_population.mean()

student_population_final[["Average Math Score", "Average Reading Score", "% Passing Math", "% Passing Reading", "% Overall Passing"]]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>Student Population</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small</th>
      <td>83.821598</td>
      <td>83.929843</td>
      <td>93.550225</td>
      <td>96.099437</td>
      <td>94.824831</td>
    </tr>
    <tr>
      <th>Medium</th>
      <td>81.176821</td>
      <td>82.933187</td>
      <td>84.649798</td>
      <td>90.095366</td>
      <td>87.372582</td>
    </tr>
    <tr>
      <th>Large</th>
      <td>77.063340</td>
      <td>80.919864</td>
      <td>66.464293</td>
      <td>81.059691</td>
      <td>73.761992</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Repeat the above breakdown, but this time group schools based on school type (Charter vs. District).

school_type = school_overview_final.groupby("Type")
school_type_final = school_type.mean()

school_type_final[["Average Math Score", "Average Reading Score", "% Passing Math", "% Passing Reading", "% Overall Passing"]]

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.473852</td>
      <td>83.896421</td>
      <td>93.620830</td>
      <td>96.586489</td>
      <td>95.103660</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.956733</td>
      <td>80.966636</td>
      <td>66.548453</td>
      <td>79.229146</td>
      <td>72.888799</td>
    </tr>
  </tbody>
</table>
</div>


