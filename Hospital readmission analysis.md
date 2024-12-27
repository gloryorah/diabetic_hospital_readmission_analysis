```python
#import libraries
```


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
#load the data
```


```python
diabetic_data= pd.read_csv('diabetic_data.csv')
```


```python
#view the first five rows
```


```python
diabetic_data.head()
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
      <th>encounter_id</th>
      <th>patient_nbr</th>
      <th>race</th>
      <th>gender</th>
      <th>age</th>
      <th>weight</th>
      <th>admission_type_id</th>
      <th>discharge_disposition_id</th>
      <th>admission_source_id</th>
      <th>time_in_hospital</th>
      <th>...</th>
      <th>citoglipton</th>
      <th>insulin</th>
      <th>glyburide-metformin</th>
      <th>glipizide-metformin</th>
      <th>glimepiride-pioglitazone</th>
      <th>metformin-rosiglitazone</th>
      <th>metformin-pioglitazone</th>
      <th>change</th>
      <th>diabetesMed</th>
      <th>readmitted</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2278392</td>
      <td>8222157</td>
      <td>Caucasian</td>
      <td>Female</td>
      <td>[0-10)</td>
      <td>?</td>
      <td>6</td>
      <td>25</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>149190</td>
      <td>55629189</td>
      <td>Caucasian</td>
      <td>Female</td>
      <td>[10-20)</td>
      <td>?</td>
      <td>1</td>
      <td>1</td>
      <td>7</td>
      <td>3</td>
      <td>...</td>
      <td>No</td>
      <td>Up</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Ch</td>
      <td>Yes</td>
      <td>&gt;30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>64410</td>
      <td>86047875</td>
      <td>AfricanAmerican</td>
      <td>Female</td>
      <td>[20-30)</td>
      <td>?</td>
      <td>1</td>
      <td>1</td>
      <td>7</td>
      <td>2</td>
      <td>...</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>NO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>500364</td>
      <td>82442376</td>
      <td>Caucasian</td>
      <td>Male</td>
      <td>[30-40)</td>
      <td>?</td>
      <td>1</td>
      <td>1</td>
      <td>7</td>
      <td>2</td>
      <td>...</td>
      <td>No</td>
      <td>Up</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Ch</td>
      <td>Yes</td>
      <td>NO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16680</td>
      <td>42519267</td>
      <td>Caucasian</td>
      <td>Male</td>
      <td>[40-50)</td>
      <td>?</td>
      <td>1</td>
      <td>1</td>
      <td>7</td>
      <td>1</td>
      <td>...</td>
      <td>No</td>
      <td>Steady</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Ch</td>
      <td>Yes</td>
      <td>NO</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 50 columns</p>
</div>




```python
#get more info about the columns
```


```python
diabetic_data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 101766 entries, 0 to 101765
    Data columns (total 50 columns):
     #   Column                    Non-Null Count   Dtype 
    ---  ------                    --------------   ----- 
     0   encounter_id              101766 non-null  int64 
     1   patient_nbr               101766 non-null  int64 
     2   race                      101766 non-null  object
     3   gender                    101766 non-null  object
     4   age                       101766 non-null  object
     5   weight                    101766 non-null  object
     6   admission_type_id         101766 non-null  int64 
     7   discharge_disposition_id  101766 non-null  int64 
     8   admission_source_id       101766 non-null  int64 
     9   time_in_hospital          101766 non-null  int64 
     10  payer_code                101766 non-null  object
     11  medical_specialty         101766 non-null  object
     12  num_lab_procedures        101766 non-null  int64 
     13  num_procedures            101766 non-null  int64 
     14  num_medications           101766 non-null  int64 
     15  number_outpatient         101766 non-null  int64 
     16  number_emergency          101766 non-null  int64 
     17  number_inpatient          101766 non-null  int64 
     18  diag_1                    101766 non-null  object
     19  diag_2                    101766 non-null  object
     20  diag_3                    101766 non-null  object
     21  number_diagnoses          101766 non-null  int64 
     22  max_glu_serum             5346 non-null    object
     23  A1Cresult                 17018 non-null   object
     24  metformin                 101766 non-null  object
     25  repaglinide               101766 non-null  object
     26  nateglinide               101766 non-null  object
     27  chlorpropamide            101766 non-null  object
     28  glimepiride               101766 non-null  object
     29  acetohexamide             101766 non-null  object
     30  glipizide                 101766 non-null  object
     31  glyburide                 101766 non-null  object
     32  tolbutamide               101766 non-null  object
     33  pioglitazone              101766 non-null  object
     34  rosiglitazone             101766 non-null  object
     35  acarbose                  101766 non-null  object
     36  miglitol                  101766 non-null  object
     37  troglitazone              101766 non-null  object
     38  tolazamide                101766 non-null  object
     39  examide                   101766 non-null  object
     40  citoglipton               101766 non-null  object
     41  insulin                   101766 non-null  object
     42  glyburide-metformin       101766 non-null  object
     43  glipizide-metformin       101766 non-null  object
     44  glimepiride-pioglitazone  101766 non-null  object
     45  metformin-rosiglitazone   101766 non-null  object
     46  metformin-pioglitazone    101766 non-null  object
     47  change                    101766 non-null  object
     48  diabetesMed               101766 non-null  object
     49  readmitted                101766 non-null  object
    dtypes: int64(13), object(37)
    memory usage: 38.8+ MB



```python
#select columns to convert to strings
```


```python
cols_to_str= ['encounter_id', 'patient_nbr', 'admission_type_id', 'discharge_disposition_id', 'admission_source_id']
```


```python
#change datatypes from int to strings
```


```python
diabetic_data[cols_to_str] = diabetic_data[cols_to_str].astype(str)
```


```python
#view data types
```


```python
diabetic_data.dtypes
```




    encounter_id                object
    patient_nbr                 object
    race                        object
    gender                      object
    age                         object
    weight                      object
    admission_type_id           object
    discharge_disposition_id    object
    admission_source_id         object
    time_in_hospital             int64
    payer_code                  object
    medical_specialty           object
    num_lab_procedures           int64
    num_procedures               int64
    num_medications              int64
    number_outpatient            int64
    number_emergency             int64
    number_inpatient             int64
    diag_1                      object
    diag_2                      object
    diag_3                      object
    number_diagnoses             int64
    max_glu_serum               object
    A1Cresult                   object
    metformin                   object
    repaglinide                 object
    nateglinide                 object
    chlorpropamide              object
    glimepiride                 object
    acetohexamide               object
    glipizide                   object
    glyburide                   object
    tolbutamide                 object
    pioglitazone                object
    rosiglitazone               object
    acarbose                    object
    miglitol                    object
    troglitazone                object
    tolazamide                  object
    examide                     object
    citoglipton                 object
    insulin                     object
    glyburide-metformin         object
    glipizide-metformin         object
    glimepiride-pioglitazone    object
    metformin-rosiglitazone     object
    metformin-pioglitazone      object
    change                      object
    diabetesMed                 object
    readmitted                  object
    dtype: object




```python
#view shape of dataframe
```


```python
diabetic_data.shape
```




    (101766, 50)




```python
#view first ten rows of weight column
```


```python
col_with_values_to_replace= ['weight', 'gender', 'race', 'admission_source_id']
diabetic_data[col_with_values_to_replace].head(10)
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
      <th>weight</th>
      <th>gender</th>
      <th>race</th>
      <th>admission_source_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>?</td>
      <td>Female</td>
      <td>Caucasian</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>?</td>
      <td>Female</td>
      <td>Caucasian</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>?</td>
      <td>Female</td>
      <td>AfricanAmerican</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>?</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>?</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>7</td>
    </tr>
    <tr>
      <th>5</th>
      <td>?</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>?</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>?</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>?</td>
      <td>Female</td>
      <td>Caucasian</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>?</td>
      <td>Female</td>
      <td>Caucasian</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
#replace ? with NaN
```


```python
diabetic_data[col_with_values_to_replace]=diabetic_data[col_with_values_to_replace].replace('?', np.nan)
```


```python
#view first ten rows of col_with_values_to_replace
```


```python
diabetic_data[col_with_values_to_replace].head(10)
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
      <th>weight</th>
      <th>gender</th>
      <th>race</th>
      <th>admission_source_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>Female</td>
      <td>Caucasian</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>Female</td>
      <td>Caucasian</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>Female</td>
      <td>AfricanAmerican</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>7</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>Male</td>
      <td>Caucasian</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>Female</td>
      <td>Caucasian</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>Female</td>
      <td>Caucasian</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
#check for missing values in the dataframe
```


```python
diabetic_data.isna().sum()
```




    encounter_id                    0
    patient_nbr                     0
    race                         2273
    gender                          0
    age                             0
    weight                      98569
    admission_type_id               0
    discharge_disposition_id        0
    admission_source_id             0
    time_in_hospital                0
    payer_code                      0
    medical_specialty               0
    num_lab_procedures              0
    num_procedures                  0
    num_medications                 0
    number_outpatient               0
    number_emergency                0
    number_inpatient                0
    diag_1                          0
    diag_2                          0
    diag_3                          0
    number_diagnoses                0
    max_glu_serum               96420
    A1Cresult                   84748
    metformin                       0
    repaglinide                     0
    nateglinide                     0
    chlorpropamide                  0
    glimepiride                     0
    acetohexamide                   0
    glipizide                       0
    glyburide                       0
    tolbutamide                     0
    pioglitazone                    0
    rosiglitazone                   0
    acarbose                        0
    miglitol                        0
    troglitazone                    0
    tolazamide                      0
    examide                         0
    citoglipton                     0
    insulin                         0
    glyburide-metformin             0
    glipizide-metformin             0
    glimepiride-pioglitazone        0
    metformin-rosiglitazone         0
    metformin-pioglitazone          0
    change                          0
    diabetesMed                     0
    readmitted                      0
    dtype: int64




```python
#create a 5% treshold for values to drop
```


```python
threshold=len(diabetic_data)*0.05
```


```python
print(threshold)
```

    5088.3



```python
#race is the only column with missing values above the threshold
#drop missing values in the race column
```


```python
diabetic_data.dropna(subset='race', inplace=True)
```


```python
#View remaining columns with missing values
```


```python
cols_with_missing_values = diabetic_data.columns[diabetic_data.isna().sum() > 0]
print(cols_with_missing_values)
```

    Index(['weight', 'max_glu_serum', 'A1Cresult'], dtype='object')



```python
#imput the mode in place of missing values
#iterate through the columns with missing values 
```


```python
for col in cols_with_missing_values: 
    if col in diabetic_data.columns:  # Check if the column exists
        mode_value = diabetic_data[col].mode()[0] 
        diabetic_data[col].fillna(mode_value)
```

# Research Questions

1. What is the overall distribution of readmission rates?
2. What is the average length of stay in the hospital?
3. What is the most common age group among the patients?
4. What are the most frequent primary diagnoses (`diag_1`)?

5. Is there a relationship between age and readmission rates?
6. Do different genders have different readmission rates?
7. How does race/ethnicity influence readmission rates?

8. Is there a relationship between the number of medications prescribed and readmission rates?

9. Do patients admitted through different sources (e.g., emergency room, physician referral) have different readmission rates?
10. Is there a relationship between the number of lab procedures and readmission rates?


## 1. What is the overall distribution of readmission rates?



```python
#view the proportion of readmissions
```


```python
readmitted_prop= diabetic_data['readmitted'].value_counts(normalize=True)
```


```python
print(readmitted_prop) 
```

    readmitted
    NO     0.535887
    >30    0.351854
    <30    0.112259
    Name: proportion, dtype: float64



```python
#get the percentages
```


```python
readmitted_prop* 100
```




    readmitted
    NO     53.588695
    >30    35.185390
    <30    11.225915
    Name: proportion, dtype: float64




```python
readmission_rate = (diabetic_data['readmitted'] != 'NO').mean()* 100
print(f"Overall Readmission Rate: {readmission_rate:.2f}%") 
```

    Overall Readmission Rate: 46.41%



```python
#countplot of the 'readmitted' column
```


```python
r= sns.countplot(x='readmitted', data= diabetic_data)
plt.xlabel= 'Readmission Status'
plt.ylabel= 'Number of Patients'
r.set_title('Distribution of Readmissions')
plt.show()
```


    
![png](output_42_0.png)
    


## 2. What is the average length of stay in the hospital?


```python
#descriptive statistics for time_in_hospital
```


```python
time_in_hospital_stats = diabetic_data['time_in_hospital'].agg(['mean', 'median', 'std', 'min', 'max'])
print(time_in_hospital_stats)
```

    mean       4.398420
    median     4.000000
    std        2.986977
    min        1.000000
    max       14.000000
    Name: time_in_hospital, dtype: float64



```python
#visualize the distribution of time_in_hospital
```


```python
t_h=sns.histplot(x= 'time_in_hospital', data= diabetic_data, binwidth=1)
plt.xlabel= 'Time in Hodspital (Days)'
plt.ylabel= 'Number of Patients'
t_h.set_title('Distribution of Hospital Stay Lengths')
plt.show()
```


    
![png](output_47_0.png)
    


## 3. What is the most common age group among the patients?


```python
#view a countplot of the age column
```


```python
a=sns.countplot(x='age', data= diabetic_data, hue='readmitted')
plt.xlabel= 'Age Group'
plt.ylabel= 'Number of Patients'
a.set_title('Age Groups and Readmission Patterns in Diabetic Patients')
plt.xticks(rotation=60) 
plt.show()
```


    
![png](output_50_0.png)
    



```python
#or find the modal agr group
```


```python
diabetic_data['age'].mode()
```




    0    [70-80)
    Name: age, dtype: object



## 4. What are the most frequent primary diagnoses (diag_1)?


```python
#find the top ten most frequent primary diagnoses
```


```python
fpd= diabetic_data['diag_1'].value_counts().head(10)
print(fpd)
```

    diag_1
    428    6739
    414    6407
    786    3938
    410    3518
    486    3425
    427    2712
    491    2228
    715    2099
    682    1996
    780    1991
    Name: count, dtype: int64


*** **Note**: ICD-9 codes:
        **428** corresponds to the diagnosis of Heart failure.
        **414** corresponds to the diagnosis of Other forms of chronic ischemic heart disease. 
        **786** refers to Symptoms involving the respiratory system and other chest symptoms.
        **410** corresponds to the diagnosis of Acute myocardial infarction (heart attack).
        **486** corresponds to the diagnosis of Pneumonia, organism unspecified.
        **427** corresponds to the diagnosis of Cardiac dysrhythmias.
        **491** corresponds to the diagnosis of Chronic bronchitis.
        **715** corresponds to the diagnosis of Osteoarthrosis and allied disorders.
        **682** corresponds to the diagnosis of Other cellulitis and abscess.
        **434** corresponds to the diagnosis of Occlusion of cerebral arteries.


```python
#filter diabetic_data to include only the rows with fpd
```


```python
top_10_diag_1= diabetic_data[diabetic_data['diag_1'].isin(fpd.index)]
```


```python
#visualize the top 10 most common diagnoses
```


```python
d1= sns.countplot(x='diag_1', data=top_10_diag_1)
plt.xlabel= 'Primary Diagnosis'
plt.ylabel= 'Number of Patients'
d1.set_title('Primary Diagnoses and Readmission Patterns')
plt.show()   
```


    
![png](output_60_0.png)
    


## 5. Is there a relationship between age and readmission rates?


```python
#create a boxplot to visualize the relationship
```


```python
rel_a_r= sns.boxplot(x='readmitted', y='age', data= diabetic_data)
rel_a_r.set (xlabel= 'Readmission Status', ylabel= 'Age Group')
rel_a_r.set_title('Relationship between Age And Readmission Status')
plt.show()
```


    
![png](output_63_0.png)
    



```python
#create a lineplot to view the relationship
```

## 6. Do different genders have different readmission rates?


```python
#calculate readmission by gender
```


```python
readmission_rates_by_gender = diabetic_data.groupby('gender')['readmitted'].value_counts(normalize=True).unstack() * 100
print(readmission_rates_by_gender)
```

    readmitted             <30        >30          NO
    gender                                           
    Female           11.313112  35.944004   52.742884
    Male             11.124420  34.301021   54.574558
    Unknown/Invalid        NaN        NaN  100.000000



```python
#show boxplots of readmission rates for different genders
```


```python
sns.catplot(x='readmitted', data= diabetic_data, kind= 'count', col='gender')
```




    <seaborn.axisgrid.FacetGrid at 0x126b874d0>




    
![png](output_69_1.png)
    


## 7. How does race/ethnicity influence readmission rates


```python
#calculate readmission by race
```


```python
readmission_rates_by_race = diabetic_data.groupby('race')['readmitted'].value_counts(normalize=True).unstack() * 100
print(readmission_rates_by_race)
```

    readmitted             <30        >30         NO
    race                                            
    AfricanAmerican  11.218116  34.534097  54.247788
    Asian            10.140406  25.117005  64.742590
    Caucasian        11.290556  35.643044  53.066400
    Hispanic         10.407462  31.516937  58.075601
    Other             9.628154  29.614874  60.756972



```python
#view the countplot of readmission status with hue set to race
```


```python
sns.countplot(x='readmitted', data=diabetic_data, hue='race')
```




    <Axes: xlabel='readmitted', ylabel='count'>




    
![png](output_74_1.png)
    


## 8. Is there a relationship between the number of medications prescribed and readmission rates? 


```python
#calculate mean number of medications per readmission status
```


```python
readmission_rates_by_np= diabetic_data.groupby('readmitted')['num_medications'].mean()
print(readmission_rates_by_np)
```

    readmitted
    <30    16.927926
    >30    16.273945
    NO     15.675394
    Name: num_medications, dtype: float64



```python
#create a scatterplot to visualize the relationship
```


```python
sns.lineplot(x='readmitted', y='num_medications', data=diabetic_data)
plt.show()
```


    
![png](output_79_0.png)
    


## 9. Do patients admitted through different sources (e.g., emergency room, physician referral) have different readmission rates?


```python
#calculate readmission by source
```


```python
readmission_rates_by_source = diabetic_data.groupby('admission_source_id')['readmitted'].value_counts(normalize=True).unstack() * 100
print(readmission_rates_by_source)
```

    readmitted                 <30        >30          NO
    admission_source_id                                  
    1                    10.667129  32.895512   56.437359
    10                         NaN  28.571429   71.428571
    11                         NaN        NaN  100.000000
    13                         NaN        NaN  100.000000
    14                         NaN        NaN  100.000000
    17                   10.435951  36.249627   53.314422
    2                    10.460653  28.598848   60.940499
    20                   13.750000  50.625000   35.625000
    22                   16.666667  25.000000   58.333333
    25                         NaN        NaN  100.000000
    3                    15.508021  31.016043   53.475936
    4                     9.879437  21.701273   68.419290
    5                    11.792453  27.594340   60.613208
    6                     8.999497  18.049271   72.951232
    7                    11.731883  37.777228   50.490889
    8                    12.500000  25.000000   62.500000
    9                    18.518519  11.111111   70.370370


*** **Note** admission_source_id
description
1-Physician Referral, 2-Clinic Referral, 3_HMO Referral, 4-Transfer from a hospital, 5-Transfer from a Skilled Nursing Facility (SNF), 6-Transfer from another health care facility, 7-Emergency Room, 8-Court/Law Enforcement
, 9-
Not Available
, 10-
Transfer from critial access hospital
, 11-
Normal Delivery
, 12-
Premature Delivery
, 13-
Sick Baby
, 14-
Extramural Birth
, 15-
Not Available
, 17-
NULL
, 18-
Transfer From Another Home Health Agency
, 19-
Readmission to Same Home Health Agency
, 20-
Not Mapped
, 21-
Unknown/Invalid
, 22-
Transfer from hospital inpt/same fac reslt in a sep claim
, 23-
Born inside this hospital
, 24-
Born outside this hospital
, 25-
Transfer from Ambulatory Surgery Center
, 26-
Transfer from Hospice


```python
#view distribution of the admission_source_id
```


```python
sns.countplot(x='admission_source_id', data=diabetic_data, hue='readmitted')
plt.show
```




    <function matplotlib.pyplot.show(close=None, block=None)>




    
![png](output_85_1.png)
    


## Distribution of Hospital Length of Stay by Readmission Rates


```python
t=sns.boxplot(x='readmitted', y='time_in_hospital', data= diabetic_data)
plt.xlabel= 'Readmission Status'
plt.ylabel= 'Time in Hospital (Days)'
t.set_title('Distribution of Hospital Stay Lengths by Readmission Status')
plt.show()
```


    
![png](output_87_0.png)
    



```python

```


```python
 
```
