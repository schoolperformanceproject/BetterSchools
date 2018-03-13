

```python
# import dependencies
import pandas as pd
import numpy as np
pd.set_option('max_colwidth', 500)
```


```python
# define which school year to extract performance data
year = '2016'
```


```python
# read raw data file as dataframe 
df_campus = pd.read_csv('CAMPSTAAR2_year%s.dat' %year)
df_campus.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CAMPUS</th>
      <th>CA00AR01016D</th>
      <th>CA00AR01S16N</th>
      <th>CB00AR01016D</th>
      <th>CB00AR01S16N</th>
      <th>CW00AR01016D</th>
      <th>CW00AR01S16N</th>
      <th>CH00AR01016D</th>
      <th>CH00AR01S16N</th>
      <th>CI00AR01016D</th>
      <th>...</th>
      <th>CE00A003A17R</th>
      <th>CS00A003017D</th>
      <th>CS00A003A17N</th>
      <th>CS00A003A17R</th>
      <th>CR00A003017D</th>
      <th>CR00A003A17N</th>
      <th>CR00A003A17R</th>
      <th>CL00A003017D</th>
      <th>CL00A003A17N</th>
      <th>CL00A003A17R</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1902001</td>
      <td>108</td>
      <td>78</td>
      <td>-1</td>
      <td>-1</td>
      <td>88</td>
      <td>70</td>
      <td>-1</td>
      <td>-1</td>
      <td>.</td>
      <td>...</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>0</td>
      <td>.</td>
      <td>.</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1902041</td>
      <td>116</td>
      <td>100</td>
      <td>-1</td>
      <td>-1</td>
      <td>92</td>
      <td>80</td>
      <td>12</td>
      <td>9</td>
      <td>.</td>
      <td>...</td>
      <td>10</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>0</td>
      <td>.</td>
      <td>.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1902103</td>
      <td>115</td>
      <td>104</td>
      <td>-1</td>
      <td>-1</td>
      <td>92</td>
      <td>88</td>
      <td>13</td>
      <td>9</td>
      <td>.</td>
      <td>...</td>
      <td>18</td>
      <td>38</td>
      <td>7</td>
      <td>18</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1903001</td>
      <td>207</td>
      <td>173</td>
      <td>10</td>
      <td>6</td>
      <td>173</td>
      <td>147</td>
      <td>15</td>
      <td>13</td>
      <td>.</td>
      <td>...</td>
      <td>6</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>-1</td>
      <td>0</td>
      <td>.</td>
      <td>.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1903041</td>
      <td>284</td>
      <td>224</td>
      <td>20</td>
      <td>9</td>
      <td>226</td>
      <td>184</td>
      <td>22</td>
      <td>16</td>
      <td>.</td>
      <td>...</td>
      <td>13</td>
      <td>101</td>
      <td>7</td>
      <td>7</td>
      <td>286</td>
      <td>7</td>
      <td>2</td>
      <td>0</td>
      <td>.</td>
      <td>.</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 1513 columns</p>
</div>




```python
# do initial data cleansing by replacing '.' or '-1' (masked data) with NaN
df_campus.replace('-1',np.nan,inplace=True)
df_campus.replace('.',np.nan,inplace=True)
```


```python
# quick data exploration shows it is a big and wide table
df_campus.shape
```




    (8757, 1513)




```python
# the column headers are coded and not user friendly for further exploration
df_campus.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CAMPUS</th>
      <th>CA00AR01016D</th>
      <th>CA00AR01S16N</th>
      <th>CB00AR01016D</th>
      <th>CB00AR01S16N</th>
      <th>CW00AR01016D</th>
      <th>CW00AR01S16N</th>
      <th>CH00AR01016D</th>
      <th>CH00AR01S16N</th>
      <th>CI00AR01016D</th>
      <th>...</th>
      <th>CE00A003A17R</th>
      <th>CS00A003017D</th>
      <th>CS00A003A17N</th>
      <th>CS00A003A17R</th>
      <th>CR00A003017D</th>
      <th>CR00A003A17N</th>
      <th>CR00A003A17R</th>
      <th>CL00A003017D</th>
      <th>CL00A003A17N</th>
      <th>CL00A003A17R</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1902001</td>
      <td>108</td>
      <td>78</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>88</td>
      <td>70</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1902041</td>
      <td>116</td>
      <td>100</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>92</td>
      <td>80</td>
      <td>12</td>
      <td>9</td>
      <td>NaN</td>
      <td>...</td>
      <td>10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1902103</td>
      <td>115</td>
      <td>104</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>92</td>
      <td>88</td>
      <td>13</td>
      <td>9</td>
      <td>NaN</td>
      <td>...</td>
      <td>18</td>
      <td>38</td>
      <td>7</td>
      <td>18</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1903001</td>
      <td>207</td>
      <td>173</td>
      <td>10</td>
      <td>6</td>
      <td>173</td>
      <td>147</td>
      <td>15</td>
      <td>13</td>
      <td>NaN</td>
      <td>...</td>
      <td>6</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1903041</td>
      <td>284</td>
      <td>224</td>
      <td>20</td>
      <td>9</td>
      <td>226</td>
      <td>184</td>
      <td>22</td>
      <td>16</td>
      <td>NaN</td>
      <td>...</td>
      <td>13</td>
      <td>101</td>
      <td>7</td>
      <td>7</td>
      <td>286</td>
      <td>7</td>
      <td>2</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 1513 columns</p>
</div>




```python
# read 3 indiviudal header mapping tables and combine them into one mapping table
df_header1 = pd.read_csv('header_mapping_1_%s.csv' %year)
df_header2 = pd.read_csv('header_mapping_2_%s.csv' %year)
df_header3 = pd.read_csv('header_mapping_3_%s.csv' %year)
df_header = pd.concat([df_header1,df_header2,df_header3],ignore_index=True)
df_header.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME</th>
      <th>LABEL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CB00A001S16N</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, African American All Tests Numerator</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CB00A001S16R</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, African American All Tests Rate</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CB00AM01S16N</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, African American Mathematics Numerator</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CB00AM01S16R</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, African American Mathematics Rate</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CB00AR01S16N</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, African American Reading/ELA Numerator</td>
    </tr>
  </tbody>
</table>
</div>




```python
# create a dictionary for the column header mapping table, and use it to rename the column headers
header_dict = {}
for i in range(len(df_header)):
    header_dict[df_header.loc[i,'NAME']] = df_header.loc[i,'LABEL']    
df_campus = df_campus.rename(columns = header_dict)
df_campus.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CAMPUS</th>
      <th>Campus 2016 Index 1: Summed Grades 3-11, All Students Reading/ELA Performance Denominator</th>
      <th>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students Reading/ELA Numerator</th>
      <th>Campus 2016 Index 1: Summed Grades 3-11, African American Reading/ELA Performance Denominator</th>
      <th>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, African American Reading/ELA Numerator</th>
      <th>Campus 2016 Index 1: Summed Grades 3-11, White Reading/ELA Performance Denominator</th>
      <th>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, White Reading/ELA Numerator</th>
      <th>Campus 2016 Index 1: Summed Grades 3-11, Hispanic Reading/ELA Performance Denominator</th>
      <th>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, Hispanic Reading/ELA Numerator</th>
      <th>Campus 2016 Index 1: Summed Grades 3-11, American Indian Reading/ELA Performance Denominator</th>
      <th>...</th>
      <th>Index 3 Campus 2017 Performance, Masters Grade Level: Grades 3-11, Summed Econ Disadv All Subjects Rate</th>
      <th>Index 3 Campus 2017 Performance: Grades 3-11, Summed Special Ed All Subjects Denominator</th>
      <th>Index 3 Campus 2017 Performance, Masters Grade Level: Grades 3-11, Summed Special Ed All Subjects Numerator</th>
      <th>Index 3 Campus 2017 Performance, Masters Grade Level: Grades 3-11, Summed Special Ed All Subjects Rate</th>
      <th>Index 3 Campus 2017 Performance: Grades 3-11, Summed At Risk All Subjects Denominator</th>
      <th>Index 3 Campus 2017 Performance, Masters Grade Level: Grades 3-11, Summed At Risk All Subjects Numerator</th>
      <th>Index 3 Campus 2017 Performance, Masters Grade Level: Grades 3-11, Summed At Risk All Subjects Rate</th>
      <th>Index 3 Campus 2017 Performance: Grades 3-11, Summed ELL All Subjects Denominator</th>
      <th>Index 3 Campus 2017 Performance, Masters Grade Level: Grades 3-11, Summed ELL All Subjects Numerator</th>
      <th>Index 3 Campus 2017 Performance, Masters Grade Level: Grades 3-11, Summed ELL All Subjects Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1902001</td>
      <td>108</td>
      <td>78</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>88</td>
      <td>70</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1902041</td>
      <td>116</td>
      <td>100</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>92</td>
      <td>80</td>
      <td>12</td>
      <td>9</td>
      <td>NaN</td>
      <td>...</td>
      <td>10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1902103</td>
      <td>115</td>
      <td>104</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>92</td>
      <td>88</td>
      <td>13</td>
      <td>9</td>
      <td>NaN</td>
      <td>...</td>
      <td>18</td>
      <td>38</td>
      <td>7</td>
      <td>18</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1903001</td>
      <td>207</td>
      <td>173</td>
      <td>10</td>
      <td>6</td>
      <td>173</td>
      <td>147</td>
      <td>15</td>
      <td>13</td>
      <td>NaN</td>
      <td>...</td>
      <td>6</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1903041</td>
      <td>284</td>
      <td>224</td>
      <td>20</td>
      <td>9</td>
      <td>226</td>
      <td>184</td>
      <td>22</td>
      <td>16</td>
      <td>NaN</td>
      <td>...</td>
      <td>13</td>
      <td>101</td>
      <td>7</td>
      <td>7</td>
      <td>286</td>
      <td>7</td>
      <td>2</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 1513 columns</p>
</div>




```python
# use melt function to transform dataset from wide table to long table so that it will be easier to set filter on the fields
df_campus = df_campus.melt(id_vars='CAMPUS', var_name='Category', value_name='Value')
print(df_campus.shape)
df_campus.head()
```

    (13240584, 3)
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CAMPUS</th>
      <th>Category</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1902001</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students Reading/ELA Performance Denominator</td>
      <td>108</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1902041</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students Reading/ELA Performance Denominator</td>
      <td>116</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1902103</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students Reading/ELA Performance Denominator</td>
      <td>115</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1903001</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students Reading/ELA Performance Denominator</td>
      <td>207</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1903041</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students Reading/ELA Performance Denominator</td>
      <td>284</td>
    </tr>
  </tbody>
</table>
</div>




```python
# create a function 'contain' to do partial string search (case insensitive) which is used in filtering data fields
def contain(string,target):
    return string.lower() in target.lower()
```


```python
# select data for the year requested
df_campus = df_campus[df_campus['Category'].apply(lambda x: contain(year,x))]
```


```python
# get the total student count by campus and remove NaN
df_student_count = df_campus[df_campus['Category'].apply(
    lambda x: contain('All Students All Tests Performance Denominator',x))].dropna()
print(df_student_count.shape)
df_student_count.head()
```

    (7990, 3)
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CAMPUS</th>
      <th>Category</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1225980</th>
      <td>1902001</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>256</td>
    </tr>
    <tr>
      <th>1225981</th>
      <td>1902041</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>337</td>
    </tr>
    <tr>
      <th>1225982</th>
      <td>1902103</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>303</td>
    </tr>
    <tr>
      <th>1225983</th>
      <td>1903001</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>484</td>
    </tr>
    <tr>
      <th>1225984</th>
      <td>1903041</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>854</td>
    </tr>
  </tbody>
</table>
</div>




```python
# get the student count for those passing the exam by campus and remove NaN
df_pass_count = df_campus[df_campus['Category'].apply(
    lambda x: contain('All Students All Tests Numerator',x))].dropna()
print(df_pass_count.shape)
df_pass_count.head()
```

    (7990, 3)
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CAMPUS</th>
      <th>Category</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1234737</th>
      <td>1902001</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>201</td>
    </tr>
    <tr>
      <th>1234738</th>
      <td>1902041</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>276</td>
    </tr>
    <tr>
      <th>1234739</th>
      <td>1902103</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>264</td>
    </tr>
    <tr>
      <th>1234740</th>
      <td>1903001</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>428</td>
    </tr>
    <tr>
      <th>1234741</th>
      <td>1903041</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>657</td>
    </tr>
  </tbody>
</table>
</div>




```python
# get the student pass rate by campus and remove NaN
df_pass_rate = df_campus[df_campus['Category'].apply(
    lambda x: contain('All Students All Tests Rate',x))].dropna()
print(df_pass_rate.shape)
df_pass_rate.head()
```

    (7761, 3)
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CAMPUS</th>
      <th>Category</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1471176</th>
      <td>1902001</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1471177</th>
      <td>1902041</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>82</td>
    </tr>
    <tr>
      <th>1471178</th>
      <td>1902103</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>87</td>
    </tr>
    <tr>
      <th>1471179</th>
      <td>1903001</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>88</td>
    </tr>
    <tr>
      <th>1471180</th>
      <td>1903041</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge dataframes to include all data elements
df_performance = df_student_count.merge(df_pass_count,on='CAMPUS',how='outer').merge(df_pass_rate,on='CAMPUS',how='outer')
print(df_performance.shape)
df_performance.head()
```

    (7990, 7)
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CAMPUS</th>
      <th>Category_x</th>
      <th>Value_x</th>
      <th>Category_y</th>
      <th>Value_y</th>
      <th>Category</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1902001</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>256</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>201</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1902041</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>337</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>276</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>82</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1902103</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>303</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>264</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1903001</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>484</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>428</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>88</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1903041</td>
      <td>Campus 2016 Index 1: Summed Grades 3-11, All Students All Tests Performance Denominator</td>
      <td>854</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Numerator</td>
      <td>657</td>
      <td>Campus 2016 Index 1: Index 1 (Phase1 Level2 &amp; PM_ELL), Summed Grades 3-11, All Students All Tests Rate</td>
      <td>77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# select columns and rename column headers, add a column for the school year requested
df_performance = df_performance[['CAMPUS','Value_x','Value_y','Value']].rename(
    columns = {'CAMPUS':'campus_id','Value_x':'student_count','Value_y':'pass_count','Value':'pct_pass'})
df_performance['year'] = year
print(df_performance.shape)
df_performance.head()
```

    (7990, 5)
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>campus_id</th>
      <th>student_count</th>
      <th>pass_count</th>
      <th>pct_pass</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1902001</td>
      <td>256</td>
      <td>201</td>
      <td>79</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1902041</td>
      <td>337</td>
      <td>276</td>
      <td>82</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1902103</td>
      <td>303</td>
      <td>264</td>
      <td>87</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1903001</td>
      <td>484</td>
      <td>428</td>
      <td>88</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1903041</td>
      <td>854</td>
      <td>657</td>
      <td>77</td>
      <td>2016</td>
    </tr>
  </tbody>
</table>
</div>




```python
# note there are 7990 schools but only 7761 schools have reported with pass rate.
# the delta represents the schools with small number of students and pass rate data are masked by TEA
print(df_performance['campus_id'].count())
print(df_performance['pct_pass'].count())
```

    7990
    7761
    


```python
# remove schools without pass rate
df_performance = df_performance.dropna()
df_performance.shape
```




    (7761, 5)




```python
# save data to csv file
df_performance.to_csv('campus_performance_%s.csv' %year,index=False)
```
