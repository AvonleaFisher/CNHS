

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import operator
```


```python
df = pd.read_csv('/Users/avonleafisher/Desktop/CNHS/CNHS.csv')
```


```python
df.head()
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
      <th>Timestamp</th>
      <th>Participant Informed Consent</th>
      <th>birthyear</th>
      <th>race</th>
      <th>ethnicity</th>
      <th>gender</th>
      <th>household</th>
      <th>children</th>
      <th>education</th>
      <th>college</th>
      <th>...</th>
      <th>post_covid_housing_satisfaction</th>
      <th>tenant_rights_workshops</th>
      <th>childcare_required</th>
      <th>childcare_eldercare_required</th>
      <th>care_provider</th>
      <th>dif_care_needed</th>
      <th>job_lost_care</th>
      <th>gatherings</th>
      <th>post_covid_public_involvement</th>
      <th>other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020/08/27 10:03:59 AM AST</td>
      <td>Yes</td>
      <td>9-16-64</td>
      <td>White/Caucasian</td>
      <td>Not of Hispanic or Latino origin;white</td>
      <td>Female</td>
      <td>NaN</td>
      <td>2</td>
      <td>Left High School, have GED</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Before/After School programs on school grounds</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020/08/27 10:41:25 AM AST</td>
      <td>Yes</td>
      <td>9-16-64</td>
      <td>White/Caucasian</td>
      <td>Not of Hispanic or Latino origin;white</td>
      <td>Female</td>
      <td>NaN</td>
      <td>2</td>
      <td>Left High School, have GED</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Before/After School programs on school grounds</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020/08/27 10:41:51 AM AST</td>
      <td>Yes</td>
      <td>9-16-64</td>
      <td>White/Caucasian</td>
      <td>Not of Hispanic or Latino origin;white</td>
      <td>Female</td>
      <td>NaN</td>
      <td>2</td>
      <td>Left High School, have GED</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Before/After School programs on school grounds</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020/08/27 11:02:27 AM AST</td>
      <td>Yes</td>
      <td>10-28-51</td>
      <td>RD</td>
      <td>blank</td>
      <td>Female</td>
      <td>NaN</td>
      <td>blank</td>
      <td>blank</td>
      <td>NaN</td>
      <td>...</td>
      <td>blank</td>
      <td>NaN</td>
      <td>blank</td>
      <td>blank</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>blank</td>
      <td>NaN</td>
      <td>blank</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020/08/28 7:42:51 AM AST</td>
      <td>Yes</td>
      <td>1987</td>
      <td>White/Caucasian</td>
      <td>blank</td>
      <td>blank</td>
      <td>2 adults  4 children</td>
      <td>4</td>
      <td>College degree(s) complete</td>
      <td>Associates degree</td>
      <td>...</td>
      <td>5</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Friends or family</td>
      <td>No</td>
      <td>No</td>
      <td>yes - sporting events</td>
      <td>blank</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 67 columns</p>
</div>




```python
df.columns
```




    Index(['Timestamp', 'Participant Informed Consent', 'birthyear', 'race',
           'ethnicity', 'gender', 'household', 'children', 'education', 'college',
           'residence', 'yrs_at_residence', 'bedrooms', 'bathrooms', 'rent',
           'rent_subsidies', 'gov_benefits', 'services', 'special_needs',
           'handicap_accessibility_needs', 'handicap_accessible',
           'special_needs_met', 'landlord_response', 'health_insurance',
           'insurance_provider', 'cars', 'public_transit',
           'changed_public_transit', 'how_PT_changed', 'PT_services_needed',
           'pre_covid_house_income', 'income_changed_post_covid',
           'unemployment_household', 'denied_unemployment', 'stimcheck',
           'know_why_no_stimcheck', 'sued_by_landlord', 'why_sued_by_landlord',
           'sued_landlord', 'why_sued_landlord', 'tenant_contact',
           'tenant_complaints', 'missed_rent', 'months_missed_rent',
           'fin_situation_discussed', 'details_discussed', 'eviction_threat',
           'eviction_threat_covid', 'place_to_stay_if_evicted',
           'housing_insecurity', 'insecurity_circumstances', 'rent_affordability',
           'future_rent_affordability', 'home_condition', 'repairs_response',
           'landlord_resp_to_covid', 'pre_covid_housing_satisfaction',
           'post_covid_housing_satisfaction', 'tenant_rights_workshops',
           'childcare_required', 'childcare_eldercare_required', 'care_provider',
           'dif_care_needed', 'job_lost_care', 'gatherings',
           'post_covid_public_involvement', 'other'],
          dtype='object')




```python
df.loc[(df.race == 'Black or African American'),'race']='Black'
df.loc[(df.race == 'White/Caucasian'),'race']='White'
df.loc[(df.race == 'Black or African American;why?'),'race']='Black'
df.loc[(df.race == 'Black or African American;White/Caucasian'),'race']='Black and White'
df.loc[(df.race == 'White/Caucasian;American Indian/Alaska Native'),'race']='White and American Indian/Alaska Native'
```


```python
race = df.race
race.dropna(inplace=True)
race = race[race != '--']
race = race[race != 'Black or African American;Sub Saharan African;American Indian/Alaska Native']
race = race[race != '--']
race = race[race != 'na']
race = race[race != 'blank']
```


```python
print(race.unique)
```

    <bound method Series.unique of 0       White
    1       White
    2       White
    3          RD
    4       White
           ...   
    89      Black
    90      Black
    91    Bengali
    93      Black
    94      White
    Name: race, Length: 84, dtype: object>



```python
race.replace(to_replace=[i for i in race if len(i) > 12], value="Multiracial", inplace=True)
```


```python
races = []
for row in race:
    if row not in races:
        races.append(row)
```


```python
race_freqs = {}
for r in races:
    race_freqs[r] = 0
    for i in race:
        if i == r:
            race_freqs[r] += 1
```


```python
race_freqs
```




    {'White': 20,
     'RD': 1,
     'Black': 43,
     'Bengali': 9,
     'Multiracial': 8,
     'Muslim': 1,
     'Afrikan': 1,
     'American': 1}




```python
sorted_races = dict(sorted(race_freqs.items(), key=operator.itemgetter(1), reverse=False))
```


```python
import matplotlib.pyplot as plt
%matplotlib inline

x = list(sorted_races.keys())
y = list(sorted_races.values())
plt.rcParams['axes.facecolor'] = 'lavender'
plt.figure(figsize = (17,10))

plt.bar(x, y, color = 'midnightblue', edgecolor='1')

plt.xlabel('Race', fontsize=17, fontname='Serif')
plt.ylabel('Number Of Respondents', fontsize=17, fontname='Serif')
plt.xticks(fontsize=17, fontname='Serif')
plt.yticks(fontsize=17, fontname='Serif')
plt.title('Respondent Racial Identity', fontsize=23, fontname='Serif')
plt.show()
```


![png](output_12_0.png)



```python
df.rent = df.rent[df.rent != "Don't want to say"]
df.rent = df.rent[df.rent != "blank"]
df.rent = df.rent[df.rent != "I have two apts.  #1 85.00  #2 #163.00"]
df.rent = df.rent[df.rent != "na"]
df.rent.dropna(inplace=True)
```


```python
rent = df.rent
for index, value in rent.items():
    if len(value) > 10:
        rent.drop(index, inplace=True)
        print(f"Index : {index}, Value : {value}")
```


```python
rent.dropna(inplace=True)
rent = rent[rent != 'none']
rent = rent[rent != '--']
rent = rent[rent != '-']
rent = rent[rent != 'what I can']
rent = rent[rent != 'own it']
rent = rent.replace( '[\$,)]','', regex=True)
rent = pd.to_numeric(rent, downcast="float")
```


```python
rent_freqs = {'0-200': 0, '201-400': 0, '401-600': 0, '601-800': 0, '801-1000': 0 , '1001-1200': 0, 'Above 1200': 0}

for r in rent:
    type(r) == int
    if 0 < r < 200:
        rent_freqs['0-200'] += 1
    if 201 < r < 400:
        rent_freqs['401-600'] += 1
    if 401 < r < 600:
        rent_freqs['601-800'] += 1
    if 801 < r < 1000:
        rent_freqs['801-1000'] += 1
    if 1000 < r < 1200:
        rent_freqs['1001-1200'] += 1
    if 1200 < r:
        rent_freqs['Above 1200'] += 1
```


```python
rent_freqs
```




    {'0-200': 13,
     '201-400': 0,
     '401-600': 17,
     '601-800': 12,
     '801-1000': 4,
     '1001-1200': 0,
     'Above 1200': 3}




```python
x = list(rent_freqs.keys())
y = list(rent_freqs.values())
plt.rcParams['axes.facecolor'] = 'lavender'
plt.figure(figsize = (20,15))

plt.barh(x, y, color = 'midnightblue', edgecolor='1')

#label the axes, title, and ticks
plt.xlabel('Number Of Respondents', fontsize=25, fontname='Serif')
plt.ylabel('Rent Range in USD', fontsize=25, fontname='Serif')
plt.xticks(fontsize=20, fontname='Serif')
plt.yticks(fontsize=22, fontname='Serif')
plt.title('Respondent Monthly Rent', fontsize=30, fontname='Serif')

#display the plot
plt.show()
```


![png](output_18_0.png)



```python
rent.describe()
```




    count      65.000000
    mean      434.792297
    std       342.912628
    min         0.000000
    25%       198.000000
    50%       307.000000
    75%       560.000000
    max      1350.000000
    Name: rent, dtype: float64




```python
ages = pd.Series(ages)
```


```python
ages.describe()
```




    count    64.000000
    mean     50.531250
    std      16.848502
    min       9.000000
    25%      35.000000
    50%      50.000000
    75%      63.250000
    max      85.000000
    dtype: float64




```python
affordable_pre = df.rent_affordability
affordable_pre.dropna(inplace=True)
affordable_pre = affordable_pre[affordable_pre != 'blank']
affordable_pre = affordable_pre[affordable_pre != 'BLANK']
affordable_pre = affordable_pre[affordable_pre != 'Good']
affordable_pre = affordable_pre[affordable_pre != 'same as is now']
affordable_pre = affordable_pre[affordable_pre != '"checked"']
```


```python
affordable_dict_pr = {'1': 0, '2': 0, '3': 0, '4':0, '5':0}
for i in affordable_pre:
    if int(i) == 1:
        affordable_dict_pr['1'] += 1
    if int(i) == 2:
        affordable_dict_pr['2'] += 1
    if int(i) == 3:
        affordable_dict_pr['3'] += 1
    if int(4) == 1:
        affordable_dict_pr['4'] += 1
    if int(5) == 1:
        affordable_dict_pr['5'] += 1
```


```python
affordable_dict_pr
```




    {'1': 7, '2': 7, '3': 17, '4': 0, '5': 0}




```python
affordable_post = df.future_rent_affordability
```


```python
affordable_post.dropna(inplace=True)
affordable_post = affordable_post[affordable_post != 'blank']
affordable_post = affordable_post[affordable_post != 'BLANK']
```


```python
affordable_post_dict = {'1': 0, '2': 0, '3': 0, '4':0, '5':0}
for i in affordable_post:
    if int(i) == 1:
        affordable_post_dict['1'] += 1
    if int(i) == 2:
        affordable_post_dict['2'] += 1
    if int(i) == 3:
        affordable_post_dict['3'] += 1
    if int(4) == 1:
        affordable_post_dict['4'] += 1
    if int(5) == 1:
        affordable_post_dict['5'] += 1
```


```python
affordable_post_dict
```




    {'1': 10, '2': 4, '3': 15, '4': 0, '5': 0}




```python
x1 = list(affordable_dict_pr.keys())
y1 = list(affordable_dict_pr.values())

x2 = list(affordable_post_dict.keys())
y2 = list(affordable_post_dict.values())

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(16,8))
fig.suptitle('Affordability of Rent Before and After COVID-19', fontname='serif', fontsize=23, y=1.08)
plt.text(x=0.5, y=0.99, s= "1=least affordable", fontsize=12,fontname='serif', ha="center", transform=fig.transFigure)
plt.text(x=0.5, y=0.95, s= "5=most affordable", fontsize=12,fontname='serif', ha="center", transform=fig.transFigure)
plt.text(x=0.5, y=0.01, s= "Affordability Rating", fontsize=15,fontname='serif', ha="center", transform=fig.transFigure)

ax1.bar(x1, y1, color = 'midnightblue', edgecolor='1')
ax1.set_title('Before', fontname='serif', fontsize=12)
ax1.set_ylabel('Number of Respondents', fontname='serif', fontsize=15)

ax2.bar(x2, y2, color = 'midnightblue', edgecolor='1')
ax2.set_title('After', fontname='serif', fontsize=12)
```




    Text(0.5, 1.0, 'After')




![png](output_29_1.png)



```python
hi = df.health_insurance
hi.dropna(inplace=True)
hi = hi[hi != 'blank']
hi = hi[hi != '--']
hi = hi[hi != 'Medical']
hi = hi[hi != 'Medicaid']
```


```python
sn3 = df.handicap_accessibility_needs
```


```python
sn3.dropna(inplace=True)
sn3 = sn3[sn3 != 'blank']
sn3 = sn3[sn3 != '--']
sn3 = sn3[sn3 != 'na']
sn3 = sn3[sn3 != 'none']
sn3 = sn3[sn3 != 'no']
sn3 = sn3[sn3 != 'No']
sn3 = sn3[sn3 != 'None']
sn3 = sn3[sn3 != 'nothing']
sn3.value_counts()
```




    ramp                          1
    bigger places                 1
    higher toilets                1
    walker                        1
    all                           1
    grip bars, wheelchair ramp    1
    ramps, low countertops        1
    grip bars in bathroom         1
    [sic] Reading writing         1
    Name: handicap_accessibility_needs, dtype: int64




```python
sn2 = df['handicap_accessible']
sn2.dropna(inplace=True)
sn2 = sn2[sn2 != 'blank']
sn2 = sn2[sn2 != '--']
sn2 = sn2[sn2 != 'na']
```


```python
sn1 = df.special_needs
```


```python
sn.dropna(inplace=True)
sn1 = sn1[sn1 != 'blank']
sn1 = sn1[sn1 != '--']
sn1 = sn1[sn1 != 'na']
sn1 = sn1[sn1 != 'ADHD']
sn1 = sn1[sn1 != 'Self, left ankle injury 1997']
sn1 = sn1[sn1 != 'senior citizen']
sn1 = sn1[sn1 != '1 senior citizen']
```


```python
sn = df.special_needs_met
```


```python
sn.dropna(inplace=True)
sn = sn[sn != 'blank']
sn = sn[sn != '--']
sn = sn[sn != 'No, I just do what I can']
sn = sn[sn != 'na']
sn = sn[sn != 'no']
```


```python
fig, axs = plt.subplots(2, 2)
axs[0, 0].plot(x, y)
axs[0, 0].set_title('Axis [0,0]')
axs[0, 1].plot(x, y, 'tab:orange')
axs[0, 1].set_title('Axis [0,1]')
axs[1, 0].plot(x, -y, 'tab:green')
axs[1, 0].set_title('Axis [1,0]')
axs[1, 1].plot(x, -y, 'tab:red')
axs[1, 1].set_title('Axis [1,1]')

for ax in axs.flat:
    ax.set(xlabel='x-label', ylabel='y-label')

# Hide x labels and tick labels for top plots and y ticks for right plots.
for ax in axs.flat:
    ax.label_outer()
```


```python
fig, axs = plt.subplots(2, 2, figsize=(16, 16))
fig.suptitle('Accessibility', fontname='serif', fontsize=20)
axs[0, 1].set_title('Have accessibility needs (if any) been addressed by landlord/property manager?', fontname='serif', fontsize=12)
sn.value_counts().plot(kind='pie', ax=axs[0, 1], colors = ['midnightblue'])
axs[0, 1].set_ylabel('')

axs[0, 0].set_title('Anyone with special needs in household?', fontname='serif', fontsize=12)
sn1.value_counts().plot(kind='bar', ax=axs[0, 0], color = 'midnightblue', edgecolor='1')


axs[1, 0].set_title('Is your home handicap accessible?', fontname='serif', fontsize=12)
sn2.value_counts().plot(kind='bar', ax=axs[1, 0], color = 'midnightblue', edgecolor='1')


axs[1, 0].set_title('Is your home handicap accessible?', fontname='serif', fontsize=12)
sn2.value_counts().plot(kind='bar', ax=axs[1, 0], color = 'midnightblue', edgecolor='1')

axs[1, 1].set_title('What types of handicap accessibility (if any), would be useful to you?', fontname='serif', fontsize=12)
sn3.value_counts().plot(kind='pie', ax=axs[1, 1], colors = ['midnightblue', 'teal', 'lightsteelblue', 'slategray', 'lavender', 'indigo', 'thistle', 'lavenderblush', 'purple'])
axs[1, 1].set_ylabel('')
```




    Text(0, 0.5, '')




![png](output_39_1.png)



```python
df.columns
```




    Index(['Timestamp', 'Participant Informed Consent', 'birthyear', 'race',
           'ethnicity', 'gender', 'household', 'children', 'education', 'college',
           'residence', 'yrs_at_residence', 'bedrooms', 'bathrooms', 'rent',
           'rent_subsidies', 'gov_benefits', 'services', 'special_needs',
           'handicap_accessibility_needs', 'handicap_accessible',
           'special_needs_met', 'landlord_response', 'health_insurance',
           'insurance_provider', 'cars', 'public_transit',
           'changed_public_transit', 'how_PT_changed', 'PT_services_needed',
           'pre_covid_house_income', 'income_changed_post_covid',
           'unemployment_household', 'denied_unemployment', 'stimcheck',
           'know_why_no_stimcheck', 'sued_by_landlord', 'why_sued_by_landlord',
           'sued_landlord', 'why_sued_landlord', 'tenant_contact',
           'tenant_complaints', 'missed_rent', 'months_missed_rent',
           'fin_situation_discussed', 'details_discussed', 'eviction_threat',
           'eviction_threat_covid', 'place_to_stay_if_evicted',
           'housing_insecurity', 'insecurity_circumstances', 'rent_affordability',
           'future_rent_affordability', 'home_condition', 'repairs_response',
           'landlord_resp_to_covid', 'pre_covid_housing_satisfaction',
           'post_covid_housing_satisfaction', 'tenant_rights_workshops',
           'childcare_required', 'childcare_eldercare_required', 'care_provider',
           'dif_care_needed', 'job_lost_care', 'gatherings',
           'post_covid_public_involvement', 'other'],
          dtype='object')




```python
by = df.birthyear
```


```python
by.dropna(inplace=True)
by = by[by != 'blank']
by = by[by != '--']
```


```python
def calc_age(year):
    if type(year) == int:
        age = 2020 - year
        return age
```


```python
by[0] = 1964
```


```python
by[1] = 1964
```


```python
by[3] = 1951
```


```python
ages = []
for i in by:
    if len(str(i)) == 4:
        ages.append(2020-int(i))
```


```python
ages_dict = {'18 or under': 0, '19-29': 0, '30-39': 0, '40-49': 0, '50-59':0, '60-69':0, '70-79':0, '80 or above':0 }
for i in ages:
    if i <= 18:
        ages_dict['18 or under'] += 1
    if 18 < i < 30:
        ages_dict['19-29'] += 1
    if 30 <= i < 39:
        ages_dict['30-39'] += 1
    if 40 <= i < 49:
        ages_dict['40-49'] += 1
    if 50 <= i < 59:
        ages_dict['50-59'] += 1
    if 60 <= i < 69:
        ages_dict['60-69'] += 1
    if 70 <= i < 79:
        ages_dict['70-79'] += 1
    if i >= 80:
        ages_dict['80 or above'] += 1
```


```python
ages_dict
```




    {'18 or under': 1,
     '19-29': 4,
     '30-39': 13,
     '40-49': 8,
     '50-59': 14,
     '60-69': 10,
     '70-79': 4,
     '80 or above': 5}




```python
x = list(ages_dict.keys())
y = list(ages_dict.values())
plt.rcParams['axes.facecolor'] = 'lavender'
plt.figure(figsize = (17,10))

plt.bar(x, y, color = 'midnightblue', edgecolor='1')

plt.xlabel('Age (Years)', fontsize=17, fontname='Serif')
plt.ylabel('Number Of Respondents', fontsize=17, fontname='Serif')
plt.xticks(fontsize=17, fontname='Serif')
plt.yticks(fontsize=17, fontname='Serif')
plt.title('Respondent Age', fontsize=23, fontname='Serif')
plt.show()
```


![png](output_50_0.png)

