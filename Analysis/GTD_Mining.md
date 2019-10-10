```python
#Useful imports
import numpy as np
import pandas as pd

%matplotlib inline
```


```python
terrorRaw = pd.read_csv('GTD_Data/gtd_0717.csv', encoding='ISO-8859-1')
terrorRaw.head()
```

    C:\Users\saini\AppData\Roaming\Python\Python37\site-packages\IPython\core\interactiveshell.py:3058: DtypeWarning: Columns (7,62,63,64,77,80,95,97,115,116) have mixed types. Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)
    




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
      <th>Unnamed: 0</th>
      <th>eventid</th>
      <th>iyear</th>
      <th>imonth</th>
      <th>iday</th>
      <th>approxdate</th>
      <th>extended</th>
      <th>resolution</th>
      <th>country</th>
      <th>country_txt</th>
      <th>...</th>
      <th>addnotes</th>
      <th>scite1</th>
      <th>scite2</th>
      <th>scite3</th>
      <th>dbsource</th>
      <th>INT_LOG</th>
      <th>INT_IDEO</th>
      <th>INT_MISC</th>
      <th>INT_ANY</th>
      <th>related</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>82108</td>
      <td>200701010001</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>1/8/2007</td>
      <td>155</td>
      <td>West Bank and Gaza Strip</td>
      <td>...</td>
      <td>NaN</td>
      <td>"Peruvian Journalist Is Seized in Gaza," The N...</td>
      <td>ÂNew Clashes in Gaza Strip,Â The Advertiser ...</td>
      <td>Geoffrey Wansell, Â28 days ago, this Scot was...</td>
      <td>CETIS</td>
      <td>-9</td>
      <td>-9</td>
      <td>1</td>
      <td>1</td>
      <td>200701010001, 200701010008</td>
    </tr>
    <tr>
      <th>1</th>
      <td>82109</td>
      <td>200701010002</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>205</td>
      <td>Thailand</td>
      <td>...</td>
      <td>NaN</td>
      <td>Denis D. Gray, ÂBombs rock Bangkok on New Yea...</td>
      <td>Seth Mydans, ÂBombs in Bangkok Kill 2 and Wou...</td>
      <td>Richard S. Ehrlich, ÂNew year starts on blood...</td>
      <td>CETIS</td>
      <td>-9</td>
      <td>-9</td>
      <td>0</td>
      <td>-9</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>82110</td>
      <td>200701010003</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>186</td>
      <td>Sri Lanka</td>
      <td>...</td>
      <td>NaN</td>
      <td>"Sri Lankan Officials Say At least Eight Kille...</td>
      <td>"Ten Killed in Sri Lanka Violence," Cairo Mena...</td>
      <td>NaN</td>
      <td>CETIS</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>82111</td>
      <td>200701010004</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>4</td>
      <td>Afghanistan</td>
      <td>...</td>
      <td>Victims were repatriated families returning to...</td>
      <td>"Refugee school torched in Eastern Afghanistan...</td>
      <td>"Gunmen torch makeshift school in Eastern Afgh...</td>
      <td>NaN</td>
      <td>CETIS</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>82112</td>
      <td>200701010005</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>153</td>
      <td>Pakistan</td>
      <td>...</td>
      <td>NaN</td>
      <td>"Thousands without power, gas after Pakistan b...</td>
      <td>"BLA claims responsibility gas pipeline blown ...</td>
      <td>NaN</td>
      <td>CETIS</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 136 columns</p>
</div>



## Name of All the Columns in the terror data.


```python
print(terrorRaw.columns)
```

    Index(['Unnamed: 0', 'eventid', 'iyear', 'imonth', 'iday', 'approxdate',
           'extended', 'resolution', 'country', 'country_txt',
           ...
           'addnotes', 'scite1', 'scite2', 'scite3', 'dbsource', 'INT_LOG',
           'INT_IDEO', 'INT_MISC', 'INT_ANY', 'related'],
          dtype='object', length=136)
    

deleteing the unnamed columns.


```python
del terrorRaw['Unnamed: 0']
terrorRaw.columns
```




    Index(['eventid', 'iyear', 'imonth', 'iday', 'approxdate', 'extended',
           'resolution', 'country', 'country_txt', 'region',
           ...
           'addnotes', 'scite1', 'scite2', 'scite3', 'dbsource', 'INT_LOG',
           'INT_IDEO', 'INT_MISC', 'INT_ANY', 'related'],
          dtype='object', length=135)




```python
terrorRaw.head()
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
      <th>eventid</th>
      <th>iyear</th>
      <th>imonth</th>
      <th>iday</th>
      <th>approxdate</th>
      <th>extended</th>
      <th>resolution</th>
      <th>country</th>
      <th>country_txt</th>
      <th>region</th>
      <th>...</th>
      <th>addnotes</th>
      <th>scite1</th>
      <th>scite2</th>
      <th>scite3</th>
      <th>dbsource</th>
      <th>INT_LOG</th>
      <th>INT_IDEO</th>
      <th>INT_MISC</th>
      <th>INT_ANY</th>
      <th>related</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>200701010001</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>1/8/2007</td>
      <td>155</td>
      <td>West Bank and Gaza Strip</td>
      <td>10</td>
      <td>...</td>
      <td>NaN</td>
      <td>"Peruvian Journalist Is Seized in Gaza," The N...</td>
      <td>ÂNew Clashes in Gaza Strip,Â The Advertiser ...</td>
      <td>Geoffrey Wansell, Â28 days ago, this Scot was...</td>
      <td>CETIS</td>
      <td>-9</td>
      <td>-9</td>
      <td>1</td>
      <td>1</td>
      <td>200701010001, 200701010008</td>
    </tr>
    <tr>
      <th>1</th>
      <td>200701010002</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>205</td>
      <td>Thailand</td>
      <td>5</td>
      <td>...</td>
      <td>NaN</td>
      <td>Denis D. Gray, ÂBombs rock Bangkok on New Yea...</td>
      <td>Seth Mydans, ÂBombs in Bangkok Kill 2 and Wou...</td>
      <td>Richard S. Ehrlich, ÂNew year starts on blood...</td>
      <td>CETIS</td>
      <td>-9</td>
      <td>-9</td>
      <td>0</td>
      <td>-9</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>200701010003</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>186</td>
      <td>Sri Lanka</td>
      <td>6</td>
      <td>...</td>
      <td>NaN</td>
      <td>"Sri Lankan Officials Say At least Eight Kille...</td>
      <td>"Ten Killed in Sri Lanka Violence," Cairo Mena...</td>
      <td>NaN</td>
      <td>CETIS</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>200701010004</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>4</td>
      <td>Afghanistan</td>
      <td>6</td>
      <td>...</td>
      <td>Victims were repatriated families returning to...</td>
      <td>"Refugee school torched in Eastern Afghanistan...</td>
      <td>"Gunmen torch makeshift school in Eastern Afgh...</td>
      <td>NaN</td>
      <td>CETIS</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>200701010005</td>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>153</td>
      <td>Pakistan</td>
      <td>6</td>
      <td>...</td>
      <td>NaN</td>
      <td>"Thousands without power, gas after Pakistan b...</td>
      <td>"BLA claims responsibility gas pipeline blown ...</td>
      <td>NaN</td>
      <td>CETIS</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 135 columns</p>
</div>



## Checking all the column names.


```python
terrorRaw.columns.values
```




    array(['eventid', 'iyear', 'imonth', 'iday', 'approxdate', 'extended',
           'resolution', 'country', 'country_txt', 'region', 'region_txt',
           'provstate', 'city', 'latitude', 'longitude', 'specificity',
           'vicinity', 'location', 'summary', 'crit1', 'crit2', 'crit3',
           'doubtterr', 'alternative', 'alternative_txt', 'multiple',
           'success', 'suicide', 'attacktype1', 'attacktype1_txt',
           'attacktype2', 'attacktype2_txt', 'attacktype3', 'attacktype3_txt',
           'targtype1', 'targtype1_txt', 'targsubtype1', 'targsubtype1_txt',
           'corp1', 'target1', 'natlty1', 'natlty1_txt', 'targtype2',
           'targtype2_txt', 'targsubtype2', 'targsubtype2_txt', 'corp2',
           'target2', 'natlty2', 'natlty2_txt', 'targtype3', 'targtype3_txt',
           'targsubtype3', 'targsubtype3_txt', 'corp3', 'target3', 'natlty3',
           'natlty3_txt', 'gname', 'gsubname', 'gname2', 'gsubname2',
           'gname3', 'gsubname3', 'motive', 'guncertain1', 'guncertain2',
           'guncertain3', 'individual', 'nperps', 'nperpcap', 'claimed',
           'claimmode', 'claimmode_txt', 'claim2', 'claimmode2',
           'claimmode2_txt', 'claim3', 'claimmode3', 'claimmode3_txt',
           'compclaim', 'weaptype1', 'weaptype1_txt', 'weapsubtype1',
           'weapsubtype1_txt', 'weaptype2', 'weaptype2_txt', 'weapsubtype2',
           'weapsubtype2_txt', 'weaptype3', 'weaptype3_txt', 'weapsubtype3',
           'weapsubtype3_txt', 'weaptype4', 'weaptype4_txt', 'weapsubtype4',
           'weapsubtype4_txt', 'weapdetail', 'nkill', 'nkillus', 'nkillter',
           'nwound', 'nwoundus', 'nwoundte', 'property', 'propextent',
           'propextent_txt', 'propvalue', 'propcomment', 'ishostkid',
           'nhostkid', 'nhostkidus', 'nhours', 'ndays', 'divert',
           'kidhijcountry', 'ransom', 'ransomamt', 'ransomamtus',
           'ransompaid', 'ransompaidus', 'ransomnote', 'hostkidoutcome',
           'hostkidoutcome_txt', 'nreleased', 'addnotes', 'scite1', 'scite2',
           'scite3', 'dbsource', 'INT_LOG', 'INT_IDEO', 'INT_MISC', 'INT_ANY',
           'related'], dtype=object)




```python
terrorRaw.describe()
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
      <th>eventid</th>
      <th>iyear</th>
      <th>imonth</th>
      <th>iday</th>
      <th>extended</th>
      <th>country</th>
      <th>region</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>specificity</th>
      <th>...</th>
      <th>ransomamt</th>
      <th>ransomamtus</th>
      <th>ransompaid</th>
      <th>ransompaidus</th>
      <th>hostkidoutcome</th>
      <th>nreleased</th>
      <th>INT_LOG</th>
      <th>INT_IDEO</th>
      <th>INT_MISC</th>
      <th>INT_ANY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>9.958300e+04</td>
      <td>99583.000000</td>
      <td>99583.000000</td>
      <td>99583.000000</td>
      <td>99583.000000</td>
      <td>99583.000000</td>
      <td>99583.000000</td>
      <td>98952.000000</td>
      <td>98952.000000</td>
      <td>99578.000000</td>
      <td>...</td>
      <td>4.930000e+02</td>
      <td>4.320000e+02</td>
      <td>4.490000e+02</td>
      <td>425.000000</td>
      <td>8093.000000</td>
      <td>7983.000000</td>
      <td>99583.000000</td>
      <td>99583.000000</td>
      <td>99583.000000</td>
      <td>99583.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2.013425e+11</td>
      <td>2013.358304</td>
      <td>6.495376</td>
      <td>15.681271</td>
      <td>0.060884</td>
      <td>122.421377</td>
      <td>8.094956</td>
      <td>26.421880</td>
      <td>52.720474</td>
      <td>1.464219</td>
      <td>...</td>
      <td>3.044498e+06</td>
      <td>5.850123e+05</td>
      <td>7.557150e+05</td>
      <td>21.665882</td>
      <td>4.847646</td>
      <td>-33.345609</td>
      <td>-5.073968</td>
      <td>-4.965777</td>
      <td>0.062219</td>
      <td>-4.635068</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2.734345e+08</td>
      <td>2.735732</td>
      <td>3.386199</td>
      <td>8.798510</td>
      <td>0.239118</td>
      <td>90.439378</td>
      <td>2.331438</td>
      <td>12.986424</td>
      <td>33.768301</td>
      <td>0.909290</td>
      <td>...</td>
      <td>1.724480e+07</td>
      <td>7.972869e+06</td>
      <td>1.302353e+07</td>
      <td>485.348806</td>
      <td>1.998676</td>
      <td>66.404840</td>
      <td>4.493405</td>
      <td>4.625282</td>
      <td>0.313233</td>
      <td>4.688076</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2.007010e+11</td>
      <td>2007.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>4.000000</td>
      <td>1.000000</td>
      <td>-42.884049</td>
      <td>-124.224996</td>
      <td>1.000000</td>
      <td>...</td>
      <td>-9.900000e+01</td>
      <td>-9.900000e+01</td>
      <td>-9.900000e+01</td>
      <td>-99.000000</td>
      <td>1.000000</td>
      <td>-99.000000</td>
      <td>-9.000000</td>
      <td>-9.000000</td>
      <td>-9.000000</td>
      <td>-9.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2.012041e+11</td>
      <td>2012.000000</td>
      <td>4.000000</td>
      <td>8.000000</td>
      <td>0.000000</td>
      <td>92.000000</td>
      <td>6.000000</td>
      <td>15.964205</td>
      <td>41.333423</td>
      <td>1.000000</td>
      <td>...</td>
      <td>-9.900000e+01</td>
      <td>0.000000e+00</td>
      <td>-9.900000e+01</td>
      <td>0.000000</td>
      <td>3.000000</td>
      <td>-99.000000</td>
      <td>-9.000000</td>
      <td>-9.000000</td>
      <td>0.000000</td>
      <td>-9.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2.014052e+11</td>
      <td>2014.000000</td>
      <td>6.000000</td>
      <td>16.000000</td>
      <td>0.000000</td>
      <td>95.000000</td>
      <td>9.000000</td>
      <td>32.469238</td>
      <td>44.770569</td>
      <td>1.000000</td>
      <td>...</td>
      <td>1.742000e+04</td>
      <td>0.000000e+00</td>
      <td>-9.900000e+01</td>
      <td>0.000000</td>
      <td>5.000000</td>
      <td>0.000000</td>
      <td>-9.000000</td>
      <td>-9.000000</td>
      <td>0.000000</td>
      <td>-9.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.015122e+11</td>
      <td>2015.000000</td>
      <td>9.000000</td>
      <td>23.000000</td>
      <td>0.000000</td>
      <td>160.000000</td>
      <td>10.000000</td>
      <td>34.195751</td>
      <td>70.621679</td>
      <td>1.000000</td>
      <td>...</td>
      <td>2.350000e+05</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000</td>
      <td>7.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2.017123e+11</td>
      <td>2017.000000</td>
      <td>12.000000</td>
      <td>31.000000</td>
      <td>1.000000</td>
      <td>1004.000000</td>
      <td>12.000000</td>
      <td>65.825119</td>
      <td>176.986756</td>
      <td>5.000000</td>
      <td>...</td>
      <td>2.000000e+08</td>
      <td>1.320000e+08</td>
      <td>2.750000e+08</td>
      <td>10000.000000</td>
      <td>7.000000</td>
      <td>2769.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 77 columns</p>
</div>



## Renaming column names for easy reading


```python
terrorRaw = terrorRaw.rename(columns = {'nkill':'Killed','nwound':'Wounded','iyear':'Year','imonth':'Month',
'iday':'Day','country':'country_no','country_txt':'Country','attacktype1_txt':'AttackType','region_txt':'Region',
'target1':'Target','summary':'Summary','gname':'Group','targtype1_txt':'Target_type','weaptype1_txt':'Weapon_type','motive':'Motive'})
```


```python
terrorRaw['Casualities'] = terrorRaw['Killed'] + terrorRaw['Wounded']
column = ['Year','Month','Day','Country','Region','city','latitude','longitude','AttackType','Killed','Wounded','Target','Summary','Group','Target_type','Weapon_type','Motive','Casualities']
```


```python
terrorRaw = pd.DataFrame(terrorRaw, columns = column)
print(terrorRaw)
```

           Year  Month  Day                   Country                      Region  \
    0      2007      1    1  West Bank and Gaza Strip  Middle East & North Africa   
    1      2007      1    1                  Thailand              Southeast Asia   
    2      2007      1    1                 Sri Lanka                  South Asia   
    3      2007      1    1               Afghanistan                  South Asia   
    4      2007      1    1                  Pakistan                  South Asia   
    5      2007      1    1               Afghanistan                  South Asia   
    6      2007      1    1                     Sudan          Sub-Saharan Africa   
    7      2007      1    1  West Bank and Gaza Strip  Middle East & North Africa   
    8      2007      1    1                  Thailand              Southeast Asia   
    9      2007      1    1                 Sri Lanka                  South Asia   
    10     2007      1    3  West Bank and Gaza Strip  Middle East & North Africa   
    11     2007      1    3                   Tunisia  Middle East & North Africa   
    12     2007      1    4               Afghanistan                  South Asia   
    13     2007      1    4                      Iraq  Middle East & North Africa   
    14     2007      1    5               Philippines              Southeast Asia   
    15     2007      1    5                 Sri Lanka                  South Asia   
    16     2007      1    5                   Nigeria          Sub-Saharan Africa   
    17     2007      1    5                     India                  South Asia   
    18     2007      1    5                      Iraq  Middle East & North Africa   
    19     2007      1    5  West Bank and Gaza Strip  Middle East & North Africa   
    20     2007      1    5  West Bank and Gaza Strip  Middle East & North Africa   
    21     2007      1    6                     India                  South Asia   
    22     2007      1    6                 Sri Lanka                  South Asia   
    23     2007      1    6               Afghanistan                  South Asia   
    24     2007      1    6                      Iraq  Middle East & North Africa   
    25     2007      1    7               Afghanistan                  South Asia   
    26     2007      1    8                      Iraq  Middle East & North Africa   
    27     2007      1    8                      Iraq  Middle East & North Africa   
    28     2007      1    8                      Iraq  Middle East & North Africa   
    29     2007      1    8                     India                  South Asia   
    ...     ...    ...  ...                       ...                         ...   
    99553  2017     12   28                     India                  South Asia   
    99554  2017     12   30               Philippines              Southeast Asia   
    99555  2017     12   30                     India                  South Asia   
    99556  2017     12   30            United Kingdom              Western Europe   
    99557  2017     12   30                     India                  South Asia   
    99558  2017     12   30                   Nigeria          Sub-Saharan Africa   
    99559  2017     12   30                     Syria  Middle East & North Africa   
    99560  2017     12   31                      Iraq  Middle East & North Africa   
    99561  2017     12   30                      Iraq  Middle East & North Africa   
    99562  2017     12   31                      Iraq  Middle East & North Africa   
    99563  2017     12   31                      Iraq  Middle East & North Africa   
    99564  2017     12   31                     India                  South Asia   
    99565  2017     12   31               Afghanistan                  South Asia   
    99566  2017     12   31                      Iraq  Middle East & North Africa   
    99567  2017     12   31                   Somalia          Sub-Saharan Africa   
    99568  2017     12   31               Afghanistan                  South Asia   
    99569  2017     12   31               Philippines              Southeast Asia   
    99570  2017     12   30               Philippines              Southeast Asia   
    99571  2017     12   31                      Iraq  Middle East & North Africa   
    99572  2017     12   31                   Somalia          Sub-Saharan Africa   
    99573  2017     12   31               Philippines              Southeast Asia   
    99574  2017     12   31                     Italy              Western Europe   
    99575  2017     12   31               Afghanistan                  South Asia   
    99576  2017     12   31                     India                  South Asia   
    99577  2017     12   31               Afghanistan                  South Asia   
    99578  2017     12   31                   Somalia          Sub-Saharan Africa   
    99579  2017     12   31                     Syria  Middle East & North Africa   
    99580  2017     12   31               Philippines              Southeast Asia   
    99581  2017     12   31                     India                  South Asia   
    99582  2017     12   31               Philippines              Southeast Asia   
    
                             city   latitude   longitude  \
    0                     Unknown  31.356581   34.326558   
    1                     Bangkok  13.727896  100.524124   
    2                      Jaffna   9.666399   80.020477   
    3                      Behsud  34.467964   70.491493   
    4                  Dera Bugti  29.034412   69.158661   
    5                       Herat  34.346722   62.197315   
    6                       Magwi   4.134965   32.293494   
    7                        Gaza  31.502407   34.459743   
    8                  Chaing Mai  18.787748   98.993131   
    9                 Cheddikulam   8.665596   80.296238   
    10                 Khan Yunis  31.346964   34.301430   
    11                   Sulayman  36.698601   10.488660   
    12                  Ghaziabad  34.715851   70.764224   
    13                    Baghdad  33.303566   44.371773   
    14              Cotabato City   7.209594  124.241966   
    15                 Nittambuwa   7.144084   80.095600   
    16         Rumauakunde Emouha   4.881111    6.859444   
    17                     Sadiya  27.508487   95.177208   
    18                      Basra  30.510054   47.778095   
    19                    Unknown  31.356581   34.326558   
    20                       Gaza  31.502407   34.459743   
    21                    Shopian  33.721287   74.831062   
    22                Meetiyagoda   6.189834   80.095394   
    23                  Woch Khor  33.589051   69.629443   
    24                    Baghdad  33.303566   44.371773   
    25           Nad Ali district  31.640000   64.240000   
    26                    Baghdad  33.303566   44.371773   
    27                    Baghdad  33.303566   44.371773   
    28                    Baghdad  33.303566   44.371773   
    29          Golaghat district  26.520144   93.969867   
    ...                       ...        ...         ...   
    99553               Talacheru  17.001086   81.807490   
    99554               Tarragona   7.042777  126.449221   
    99555           Koothuparamba  11.831902   75.565432   
    99556                 Belfast  54.607712   -5.956210   
    99557                Toylanka  18.802725   81.497666   
    99558        Konduga district  11.492144   12.969724   
    99559                 Harasta  33.561504   36.368763   
    99560                 Shurjah  35.560376   44.524705   
    99561                  Kirkuk  35.452110   44.375465   
    99562            Hawd al-Waqf  33.816111   44.783524   
    99563              Farhatiyah  34.031331   44.070106   
    99564               Lethapora  33.966527   74.964225   
    99565               Jalalabad  34.417122   70.449593   
    99566                    Baaj  36.045059   41.716717   
    99567               Mogadishu   2.059819   45.326115   
    99568  Mohammad Agha district  34.217806   69.109316   
    99569                 Limpogo   6.983953  124.420664   
    99570          Pikit district   7.053143  124.619270   
    99571              Muqdadiyah  33.953167   44.921906   
    99572                   Wajid   3.810951   43.246506   
    99573           Shariff Aguak   6.862806  124.443649   
    99574               Spinetoli  42.888982   13.772795   
    99575       Kohistan district  35.315467   64.815508   
    99576                 Hungrum  25.180162   93.015788   
    99577                 Maymana  35.921051   64.774544   
    99578           Ceelka Geelow   2.359673   45.385034   
    99579                  Jableh  35.407278   35.942679   
    99580                Kubentog   6.900742  124.437908   
    99581                  Imphal  24.798346   93.940430   
    99582           Cotabato City   7.209594  124.241966   
    
                               AttackType  Killed  Wounded  \
    0         Hostage Taking (Kidnapping)     0.0      0.0   
    1                   Bombing/Explosion     3.0     38.0   
    2                   Bombing/Explosion     1.0      4.0   
    3      Facility/Infrastructure Attack     0.0      0.0   
    4                   Bombing/Explosion     0.0      0.0   
    5                   Bombing/Explosion     2.0      1.0   
    6                             Unknown    13.0      8.0   
    7         Hostage Taking (Kidnapping)     0.0      3.0   
    8                   Bombing/Explosion     0.0      1.0   
    9                   Bombing/Explosion     2.0      1.0   
    10                      Armed Assault     5.0     12.0   
    11                      Armed Assault    14.0      NaN   
    12                  Bombing/Explosion     0.0      0.0   
    13                  Bombing/Explosion    13.0     25.0   
    14                  Bombing/Explosion     0.0      3.0   
    15                  Bombing/Explosion     5.0     30.0   
    16        Hostage Taking (Kidnapping)     0.0      0.0   
    17                      Armed Assault    48.0     19.0   
    18        Hostage Taking (Kidnapping)     3.0      0.0   
    19                      Armed Assault     1.0      0.0   
    20                      Armed Assault     7.0      0.0   
    21                  Bombing/Explosion     1.0     25.0   
    22                  Bombing/Explosion    12.0     47.0   
    23                      Armed Assault     1.0      0.0   
    24                      Assassination     1.0      6.0   
    25                      Armed Assault     1.0      0.0   
    26                      Armed Assault     4.0      9.0   
    27                  Bombing/Explosion     3.0      1.0   
    28                  Bombing/Explosion     0.0      3.0   
    29                      Armed Assault     2.0      0.0   
    ...                               ...     ...      ...   
    99553  Facility/Infrastructure Attack     1.0      0.0   
    99554               Bombing/Explosion     NaN      2.0   
    99555               Bombing/Explosion     0.0      0.0   
    99556                   Armed Assault     0.0      2.0   
    99557  Facility/Infrastructure Attack     0.0      0.0   
    99558  Facility/Infrastructure Attack     NaN      NaN   
    99559               Bombing/Explosion     NaN      NaN   
    99560               Bombing/Explosion     0.0      0.0   
    99561               Bombing/Explosion     0.0      5.0   
    99562                         Unknown     1.0      0.0   
    99563               Bombing/Explosion     4.0      9.0   
    99564                   Armed Assault     8.0      3.0   
    99565               Bombing/Explosion    18.0     14.0   
    99566                         Unknown     5.0      0.0   
    99567               Bombing/Explosion     2.0      3.0   
    99568               Bombing/Explosion     5.0      0.0   
    99569  Facility/Infrastructure Attack     0.0      0.0   
    99570               Bombing/Explosion     1.0      1.0   
    99571                   Armed Assault    13.0      0.0   
    99572               Bombing/Explosion     0.0      0.0   
    99573               Bombing/Explosion     1.0      5.0   
    99574  Facility/Infrastructure Attack     0.0      0.0   
    99575                   Armed Assault     6.0      0.0   
    99576     Hostage Taking (Kidnapping)     0.0      0.0   
    99577               Bombing/Explosion     0.0      4.0   
    99578                   Armed Assault     1.0      2.0   
    99579               Bombing/Explosion     2.0      7.0   
    99580  Facility/Infrastructure Attack     0.0      0.0   
    99581               Bombing/Explosion     0.0      0.0   
    99582               Bombing/Explosion     0.0      0.0   
    
                                                      Target  \
    0                                           Jamie Ruzuri   
    1                                                Bangkok   
    2                                       Military Vehicle   
    3                  Behsud (District) UNICEF built school   
    4      Main gas pipeline and tow power pylons in Balo...   
    5                                             Herat City   
    6                                      Southern Sudanese   
    7                                  Hamas Security Forces   
    8                                                 Mosque   
    9                                            Police Jeep   
    10                                 Hamas Security Forces   
    11                                               Unknown   
    12                                   Ghazi Abad district   
    13         Mansour Sunni neighborhood in Western Baghdad   
    14                                              Cotabato   
    15                                            Nittambuwa   
    16                      Telecommunications field workers   
    17                             Hindi-speaking minorities   
    18                                        Ronald Withrow   
    19                                            Adel Nasar   
    20                                           Col. Ghayeb   
    21                                               Shopian   
    22                                           Meetiyagoda   
    23                                         Mursal Mangal   
    24                          Major General Ali al-Yassiri   
    25                         Principle Mohammad Rahim Khan   
    26                                              Janitors   
    27     Shoppers in al-Za'faraniyah market in south Ba...   
    28     Muslims returning from the annual hajj pilgrim...   
    29             Hindi-speaking minority vegetable vendors   
    ...                                                  ...   
    99553                                             Masjid   
    99554                                           Soldiers   
    99555                       Koothuparamba Police Station   
    99556                                          Civilians   
    99557                             Road Construction Site   
    99558                                             Convoy   
    99559                                               Base   
    99560                                             Patrol   
    99561                                               Cafe   
    99562                                            Station   
    99563                                          Civilians   
    99564                                               Camp   
    99565     Funeral Procession of Former District Governor   
    99566                                             Troops   
    99567                                   Burundian Convoy   
    99568                                            Vehicle   
    99569                                               Town   
    99570                                              Store   
    99571                                               Post   
    99572                                     Ethiopian Base   
    99573                                             Patrol   
    99574                                     Migrant Center   
    99575                                    House of Member   
    99576  Personal Security Officer of Council Member Ih...   
    99577                                       Jewelry Shop   
    99578                                         Checkpoint   
    99579                                   Hmeymim Air Base   
    99580                                             Houses   
    99581                                             Office   
    99582                                            Unknown   
    
                                                     Summary  \
    0      01/1/2007: Peruvian photographer, Jamie Ruzuri...   
    1      01/1/2007: Nine bombs in two waves killed two ...   
    2      01/1/2007: The Liberation Tigers of Tamil Eala...   
    3      01/1/2007: Taliban militants torched a school ...   
    4      01/1/2007: Baluchistan Liberation Army (BLA) b...   
    5      01/1/2007: A Roadside bomb exploded and killed...   
    6      01/01/2007: Thirteen people were killed in two...   
    7      01/01/2007: Two civilians were wounded in gunf...   
    8      01/01/2007:  A small bomb was thrown at a mosq...   
    9      01/1/2007: The Liberation Tigers of Tamil Eala...   
    10     01/03/2007: Three officers of the Fatah- domin...   
    11     01/03/207:  More than 25 Islamic extremists en...   
    12     01/04/2007: A rocket attack damaged an Afghan ...   
    13     01/04/2007: Twin car bombs killed 13 people an...   
    14     01/05/2007: A bomb injured two people near a f...   
    15     01/05/2007: Suspected Tamil Tiger (LTTE) rebel...   
    16     01/05/2007: Five Chinese telecommunications wo...   
    17     01/05/2007: Forty-eight Hindi-speaking migrant...   
    18     01/05/2007: An American private contractor of ...   
    19     01/05/2007: An anti-Hamas, mosque preacher, Ad...   
    20     01/05/2007: Seven members of Fatah including, ...   
    21     01/06/2007: At least one person was killed and...   
    22     01/06/2007: A suspected Liberation Tigers of T...   
    23     01/06/2007: Unidentified armed assailants kill...   
    24     01/06/2007: One civilian was killed and six ot...   
    25     01/07/2007: Unidentified armed men killed the ...   
    26     01/08/2007: An ambush by unknown gunmen target...   
    27     01/08/2007: A bomb placed by unknown perpetrat...   
    28     01/08/2007: Three Muslims returning from the a...   
    29     01/08/2007: Two migrant laborers were killed a...   
    ...                                                  ...   
    99553  12/28/2017: Assailants attacked Noorani Masjid...   
    99554  12/30/2017: Assailants opened fire on and deto...   
    99555  12/30/2017: Assailants threw an explosive devi...   
    99556  12/30/2017: Assailants attacked a house on Cav...   
    99557  12/30/2017: Assailants set fire to seven vehic...   
    99558  12/30/2017: Assailants attacked a convoy along...   
    99559  12/30/2017: A suicide bomber detonated an expl...   
    99560  12/31/2017: Assailants fired a rocket-propelle...   
    99561  12/30/2017: Assailants threw grenades at a caf...   
    99562  12/31/2017: Assailants attacked a police stati...   
    99563  12/31/2017: Assailants attacked civilians in F...   
    99564  12/31/2017: Assailants armed with grenades and...   
    99565  12/31/2017: An explosives-laden motorcycle det...   
    99566  12/31/2017: Assailants attacked Baaj, Nineveh,...   
    99567  12/31/2017: An explosive device detonated targ...   
    99568  12/31/2017: An explosive device detonated targ...   
    99569  12/31/2017: Assailants set fire to at least 12...   
    99570  12/30/2017: Assailants threw a grenade at a st...   
    99571  12/31/2017: Assailants attacked volunteer figh...   
    99572  12/31/2017: Assailants fired mortars at an Eth...   
    99573  12/31/2017: A roadside bomb detonated targetin...   
    99574  12/31/2017: Assailants set fire to a migrants'...   
    99575  12/31/2017: Assailants attacked the house of a...   
    99576  12/31/2017: Assailants abducted Prafulla Phuka...   
    99577  12/31/2017: An explosive device detonated at a...   
    99578  12/31/2017: Assailants opened fire on a Somali...   
    99579  12/31/2017: Assailants launched mortars at the...   
    99580  12/31/2017: Assailants set fire to houses in K...   
    99581  12/31/2017: Assailants threw a grenade at a Fo...   
    99582  12/31/2017: An explosive device was discovered...   
    
                                                    Group  \
    0                                             Unknown   
    1                                             Unknown   
    2             Liberation Tigers of Tamil Eelam (LTTE)   
    3                                             Taliban   
    4                        Baloch Liberation Army (BLA)   
    5                                             Taliban   
    6                        Lord's Resistance Army (LRA)   
    7                 Hamas (Islamic Resistance Movement)   
    8                                             Unknown   
    9             Liberation Tigers of Tamil Eelam (LTTE)   
    10                Hamas (Islamic Resistance Movement)   
    11                                            Unknown   
    12                                            Unknown   
    13                                            Unknown   
    14               Moro Islamic Liberation Front (MILF)   
    15            Liberation Tigers of Tamil Eelam (LTTE)   
    16                                            Unknown   
    17            United Liberation Front of Assam (ULFA)   
    18                                            Unknown   
    19                                            Unknown   
    20                Hamas (Islamic Resistance Movement)   
    21                                            Unknown   
    22            Liberation Tigers of Tamil Eelam (LTTE)   
    23                                            Unknown   
    24                                            Unknown   
    25                                            Unknown   
    26                                            Unknown   
    27                                            Unknown   
    28                                            Unknown   
    29            United Liberation Front of Assam (ULFA)   
    ...                                               ...   
    99553                                         Unknown   
    99554                         New People's Army (NPA)   
    99555                                         Unknown   
    99556                                         Unknown   
    99557  Communist Party of India - Maoist (CPI-Maoist)   
    99558                                      Boko Haram   
    99559                           Hay'at Tahrir al-Sham   
    99560                                         Unknown   
    99561                                         Unknown   
    99562     Islamic State of Iraq and the Levant (ISIL)   
    99563     Islamic State of Iraq and the Levant (ISIL)   
    99564                          Jaish-e-Mohammad (JeM)   
    99565           Khorasan Chapter of the Islamic State   
    99566     Islamic State of Iraq and the Levant (ISIL)   
    99567                                      Al-Shabaab   
    99568                                         Taliban   
    99569      Bangsamoro Islamic Freedom Movement (BIFM)   
    99570                                         Unknown   
    99571     Islamic State of Iraq and the Levant (ISIL)   
    99572                                      Al-Shabaab   
    99573      Bangsamoro Islamic Freedom Movement (BIFM)   
    99574                                         Unknown   
    99575                                         Taliban   
    99576                        Zeliangrong United Front   
    99577                                         Unknown   
    99578                                      Al-Shabaab   
    99579                               Muslim extremists   
    99580      Bangsamoro Islamic Freedom Movement (BIFM)   
    99581                                         Unknown   
    99582                                         Unknown   
    
                              Target_type Weapon_type  \
    0                 Journalists & Media    Firearms   
    1         Private Citizens & Property  Explosives   
    2                            Military  Explosives   
    3             Educational Institution  Incendiary   
    4                           Utilities  Explosives   
    5                              Police  Explosives   
    6         Private Citizens & Property     Unknown   
    7                Government (General)    Firearms   
    8      Religious Figures/Institutions  Explosives   
    9                              Police  Explosives   
    10               Government (General)    Firearms   
    11                             Police    Firearms   
    12            Educational Institution  Explosives   
    13        Private Citizens & Property  Explosives   
    14                           Business  Explosives   
    15                     Transportation  Explosives   
    16                           Business    Firearms   
    17        Private Citizens & Property    Firearms   
    18                           Business    Firearms   
    19     Religious Figures/Institutions    Firearms   
    20                             Police    Firearms   
    21                           Military  Explosives   
    22                     Transportation  Explosives   
    23                             Police    Firearms   
    24                             Police  Explosives   
    25            Educational Institution    Firearms   
    26                Airports & Aircraft    Firearms   
    27        Private Citizens & Property  Explosives   
    28        Private Citizens & Property  Explosives   
    29        Private Citizens & Property    Firearms   
    ...                               ...         ...   
    99553  Religious Figures/Institutions  Incendiary   
    99554                        Military  Explosives   
    99555                          Police  Explosives   
    99556     Private Citizens & Property    Firearms   
    99557                        Business    Firearms   
    99558     Private Citizens & Property     Unknown   
    99559                        Military  Explosives   
    99560                        Military  Explosives   
    99561                        Business  Explosives   
    99562                          Police     Unknown   
    99563     Private Citizens & Property  Explosives   
    99564                          Police  Explosives   
    99565     Private Citizens & Property  Explosives   
    99566                        Military     Unknown   
    99567                        Military  Explosives   
    99568                          Police  Explosives   
    99569     Private Citizens & Property    Firearms   
    99570                        Business  Explosives   
    99571                        Military    Firearms   
    99572                        Military  Explosives   
    99573                          Police  Explosives   
    99574     Private Citizens & Property  Incendiary   
    99575    Terrorists/Non-State Militia    Firearms   
    99576            Government (General)    Firearms   
    99577                        Business  Explosives   
    99578                        Military    Firearms   
    99579                        Military  Explosives   
    99580     Private Citizens & Property  Incendiary   
    99581            Government (General)  Explosives   
    99582                         Unknown  Explosives   
    
                                                      Motive  Casualities  
    0                                                Unknown          0.0  
    1                                                Unknown         41.0  
    2                                                Unknown          5.0  
    3                                                Unknown          0.0  
    4                                                Unknown          0.0  
    5                                                Unknown          3.0  
    6                                                Unknown         21.0  
    7                                                Unknown          3.0  
    8                                                    NaN          1.0  
    9                                                Unknown          3.0  
    10                                               Unknown         17.0  
    11                                                   NaN          NaN  
    12                                               Unknown          0.0  
    13                                               Unknown         38.0  
    14                                               Unknown          3.0  
    15     The attack comes two days after the LTTE warne...         35.0  
    16                                               Unknown          0.0  
    17                                               Unknown         67.0  
    18                                               Unknown          3.0  
    19                                               Unknown          1.0  
    20                                               Unknown          7.0  
    21                                               Unknown         26.0  
    22     The attack comes days after the LTTE warned th...         59.0  
    23                                               Unknown          1.0  
    24                                               Unknown          7.0  
    25                                               Unknown          1.0  
    26                                               Unknown         13.0  
    27                                               Unknown          4.0  
    28                                               Unknown          3.0  
    29                                               Unknown          2.0  
    ...                                                  ...          ...  
    99553                                                NaN          1.0  
    99554                                                NaN          NaN  
    99555  The specific motive is unknown; however, sourc...          0.0  
    99556                                                NaN          2.0  
    99557  The specific motive is unknown; however, sourc...          0.0  
    99558                                                NaN          NaN  
    99559                                                NaN          NaN  
    99560                                                NaN          0.0  
    99561                                                NaN          5.0  
    99562                                                NaN          1.0  
    99563                                                NaN         13.0  
    99564  The specific motive is unknown; however, sourc...         11.0  
    99565                                                NaN         32.0  
    99566                                                NaN          5.0  
    99567                                                NaN          5.0  
    99568                                                NaN          5.0  
    99569                                                NaN          0.0  
    99570                                                NaN          2.0  
    99571                                                NaN         13.0  
    99572                                                NaN          0.0  
    99573                                                NaN          6.0  
    99574  The specific motive is unknown; however, sourc...          0.0  
    99575  The specific motive is unknown; however, sourc...          6.0  
    99576                                                NaN          0.0  
    99577                                                NaN          4.0  
    99578                                                NaN          3.0  
    99579                                                NaN          9.0  
    99580                                                NaN          0.0  
    99581                                                NaN          0.0  
    99582                                                NaN          0.0  
    
    [99583 rows x 18 columns]
    

## Checking the number of null values in  the columns


```python
terrorRaw.isnull().sum()
```




    Year               0
    Month              0
    Day                0
    Country            0
    Region             0
    city             380
    latitude         631
    longitude        631
    AttackType         0
    Killed          3939
    Wounded         7048
    Target           132
    Summary            0
    Group              0
    Target_type        0
    Weapon_type        0
    Motive         64591
    Casualities     7324
    dtype: int64



## Getting the top country from each region where maximum number of attacks happened


```python
regions = terrorRaw["Region"].value_counts().index.tolist()
regions
```




    ['Middle East & North Africa',
     'South Asia',
     'Sub-Saharan Africa',
     'Southeast Asia',
     'Eastern Europe',
     'Western Europe',
     'South America',
     'North America',
     'Central Asia',
     'East Asia',
     'Australasia & Oceania',
     'Central America & Caribbean']




```python
country = terrorRaw[["Region", "Country"]]
country = country.groupby("Region")["Country"].value_counts().sort_values(ascending=False).to_frame()
country.head(12)
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
      <th></th>
      <th>Country</th>
    </tr>
    <tr>
      <th>Region</th>
      <th>Country</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Middle East &amp; North Africa</th>
      <th>Iraq</th>
      <td>22576</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">South Asia</th>
      <th>Pakistan</th>
      <td>12066</td>
    </tr>
    <tr>
      <th>Afghanistan</th>
      <td>11916</td>
    </tr>
    <tr>
      <th>India</th>
      <td>7703</td>
    </tr>
    <tr>
      <th>Southeast Asia</th>
      <th>Philippines</th>
      <td>4468</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Sub-Saharan Africa</th>
      <th>Somalia</th>
      <td>3938</td>
    </tr>
    <tr>
      <th>Nigeria</th>
      <td>3748</td>
    </tr>
    <tr>
      <th>Middle East &amp; North Africa</th>
      <th>Yemen</th>
      <td>3197</td>
    </tr>
    <tr>
      <th>Southeast Asia</th>
      <th>Thailand</th>
      <td>3186</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">Middle East &amp; North Africa</th>
      <th>Libya</th>
      <td>2235</td>
    </tr>
    <tr>
      <th>Syria</th>
      <td>2053</td>
    </tr>
    <tr>
      <th>Egypt</th>
      <td>1994</td>
    </tr>
  </tbody>
</table>
</div>



## Getting the list and filtering the data for those countries


```python
cnt = 0
allRegions = []
topCountryEachRegion = []
for x in country.index:
    #print (x[0])
    if (x[0] in allRegions):
        print(x[1])
    else:
        allRegions.append(x[0])
        topCountryEachRegion.append(x[1])
        
print(topCountryEachRegion)
```

    Afghanistan
    India
    Nigeria
    Yemen
    Thailand
    Libya
    Syria
    Egypt
    Turkey
    Russia
    Bangladesh
    West Bank and Gaza Strip
    Nepal
    Sudan
    Israel
    Democratic Republic of the Congo
    Kenya
    Algeria
    Lebanon
    Mali
    Greece
    Sri Lanka
    Myanmar
    Saudi Arabia
    Cameroon
    Central African Republic
    Burundi
    France
    Indonesia
    South Sudan
    Germany
    Bahrain
    Ireland
    Mozambique
    Niger
    Iran
    South Africa
    Mexico
    Tunisia
    Spain
    Chile
    Sweden
    Paraguay
    Ethiopia
    Italy
    Uganda
    Peru
    Chad
    Malaysia
    Kosovo
    Ivory Coast
    Burkina Faso
    Canada
    Tanzania
    Venezuela
    Senegal
    Jordan
    Rwanda
    Cyprus
    Japan
    Macedonia
    Maldives
    Czech Republic
    Bosnia-Herzegovina
    Argentina
    Austria
    Kazakhstan
    Brazil
    Republic of the Congo
    Tajikistan
    Netherlands
    Finland
    Zimbabwe
    Belgium
    Kyrgyzstan
    Ecuador
    Bulgaria
    Azerbaijan
    Serbia
    Mauritania
    Angola
    Albania
    Papua New Guinea
    Denmark
    Morocco
    Laos
    Switzerland
    Belarus
    Guatemala
    Armenia
    New Zealand
    Bolivia
    Madagascar
    Eritrea
    Taiwan
    Hungary
    United Arab Emirates
    Croatia
    Guinea
    Bhutan
    Malta
    Norway
    Trinidad and Tobago
    Guyana
    Poland
    Montenegro
    Jamaica
    Sierra Leone
    Cambodia
    Kuwait
    Liberia
    Gabon
    Uzbekistan
    Djibouti
    Haiti
    Moldova
    East Timor
    Dominican Republic
    Estonia
    Swaziland
    Panama
    Zambia
    Guinea-Bissau
    Nicaragua
    Lesotho
    South Korea
    Ghana
    Vietnam
    Iceland
    Latvia
    Portugal
    Cuba
    Belize
    Bahamas
    Benin
    Uruguay
    Turkmenistan
    Romania
    Slovak Republic
    Hong Kong
    Equatorial Guinea
    Malawi
    Western Sahara
    Qatar
    ['Iraq', 'Pakistan', 'Philippines', 'Somalia', 'Ukraine', 'Colombia', 'United Kingdom', 'United States', 'China', 'Georgia', 'Australia', 'Honduras']
    


```python
terrorRaw = terrorRaw[(terrorRaw["Country"].isin(topCountryEachRegion))]
terrorRaw.head()
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
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Country</th>
      <th>Region</th>
      <th>city</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>AttackType</th>
      <th>Killed</th>
      <th>Wounded</th>
      <th>Target</th>
      <th>Summary</th>
      <th>Group</th>
      <th>Target_type</th>
      <th>Weapon_type</th>
      <th>Motive</th>
      <th>Casualities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>2007</td>
      <td>1</td>
      <td>1</td>
      <td>Pakistan</td>
      <td>South Asia</td>
      <td>Dera Bugti</td>
      <td>29.034412</td>
      <td>69.158661</td>
      <td>Bombing/Explosion</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>Main gas pipeline and tow power pylons in Balo...</td>
      <td>01/1/2007: Baluchistan Liberation Army (BLA) b...</td>
      <td>Baloch Liberation Army (BLA)</td>
      <td>Utilities</td>
      <td>Explosives</td>
      <td>Unknown</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2007</td>
      <td>1</td>
      <td>4</td>
      <td>Iraq</td>
      <td>Middle East &amp; North Africa</td>
      <td>Baghdad</td>
      <td>33.303566</td>
      <td>44.371773</td>
      <td>Bombing/Explosion</td>
      <td>13.0</td>
      <td>25.0</td>
      <td>Mansour Sunni neighborhood in Western Baghdad</td>
      <td>01/04/2007: Twin car bombs killed 13 people an...</td>
      <td>Unknown</td>
      <td>Private Citizens &amp; Property</td>
      <td>Explosives</td>
      <td>Unknown</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2007</td>
      <td>1</td>
      <td>5</td>
      <td>Philippines</td>
      <td>Southeast Asia</td>
      <td>Cotabato City</td>
      <td>7.209594</td>
      <td>124.241966</td>
      <td>Bombing/Explosion</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>Cotabato</td>
      <td>01/05/2007: A bomb injured two people near a f...</td>
      <td>Moro Islamic Liberation Front (MILF)</td>
      <td>Business</td>
      <td>Explosives</td>
      <td>Unknown</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2007</td>
      <td>1</td>
      <td>5</td>
      <td>Iraq</td>
      <td>Middle East &amp; North Africa</td>
      <td>Basra</td>
      <td>30.510054</td>
      <td>47.778095</td>
      <td>Hostage Taking (Kidnapping)</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>Ronald Withrow</td>
      <td>01/05/2007: An American private contractor of ...</td>
      <td>Unknown</td>
      <td>Business</td>
      <td>Firearms</td>
      <td>Unknown</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2007</td>
      <td>1</td>
      <td>6</td>
      <td>Iraq</td>
      <td>Middle East &amp; North Africa</td>
      <td>Baghdad</td>
      <td>33.303566</td>
      <td>44.371773</td>
      <td>Assassination</td>
      <td>1.0</td>
      <td>6.0</td>
      <td>Major General Ali al-Yassiri</td>
      <td>01/06/2007: One civilian was killed and six ot...</td>
      <td>Unknown</td>
      <td>Police</td>
      <td>Explosives</td>
      <td>Unknown</td>
      <td>7.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
terrorRaw.to_csv('GTD_Data/gtd_0717_final.csv')
```


```python
terrorRaw["Country"].value_counts().sort_values(ascending=True)
```




    Honduras             14
    Australia            41
    Georgia              81
    China               113
    United States       300
    United Kingdom      822
    Colombia           1389
    Ukraine            1678
    Somalia            3938
    Philippines        4468
    Pakistan          12066
    Iraq              22576
    Name: Country, dtype: int64




```python
terrorRaw = pd.read_csv('GTD_Data/gtd_0717_final.csv', encoding='ISO-8859-1')
del terrorRaw['Unnamed: 0']
terrorRaw = terrorRaw[(terrorRaw["Year"] >= 2008) & (terrorRaw["Year"] <= 2017)]
terrorRaw = terrorRaw[["Year", "Country", "Casualities"]]
terrorRaw = terrorRaw.reset_index()
del terrorRaw['index']
terrorRaw.head()
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
      <th>Year</th>
      <th>Country</th>
      <th>Casualities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2008</td>
      <td>Philippines</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2008</td>
      <td>Iraq</td>
      <td>67.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2008</td>
      <td>Iraq</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2008</td>
      <td>Iraq</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2008</td>
      <td>Iraq</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



## Reading and filtering the GDP data


```python
gdpRaw = pd.read_csv("GTD_Data/world_gdp.csv")
gdpRaw = gdpRaw[["Country Name", "Country Code", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016", "2017"]]
gdpRaw.head()
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
      <th>Country Name</th>
      <th>Country Code</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aruba</td>
      <td>ABW</td>
      <td>-0.090708</td>
      <td>-10.519748</td>
      <td>-3.685030</td>
      <td>3.446055</td>
      <td>-1.369863</td>
      <td>4.198232</td>
      <td>0.848228</td>
      <td>-0.450586</td>
      <td>-0.211225</td>
      <td>1.330511</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>AFG</td>
      <td>3.924984</td>
      <td>21.390528</td>
      <td>14.362441</td>
      <td>0.426355</td>
      <td>12.752287</td>
      <td>5.600745</td>
      <td>2.724543</td>
      <td>1.451315</td>
      <td>2.260314</td>
      <td>2.665292</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Angola</td>
      <td>AGO</td>
      <td>11.166138</td>
      <td>0.858713</td>
      <td>4.859220</td>
      <td>3.471981</td>
      <td>8.542147</td>
      <td>4.954590</td>
      <td>4.822626</td>
      <td>0.943576</td>
      <td>-2.580097</td>
      <td>-0.147207</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>ALB</td>
      <td>7.499970</td>
      <td>3.349994</td>
      <td>3.706881</td>
      <td>2.545405</td>
      <td>1.417526</td>
      <td>1.001988</td>
      <td>1.770000</td>
      <td>2.230000</td>
      <td>3.350000</td>
      <td>3.836620</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Andorra</td>
      <td>AND</td>
      <td>-8.590004</td>
      <td>-3.690654</td>
      <td>-5.358826</td>
      <td>-4.646543</td>
      <td>-1.615218</td>
      <td>0.351645</td>
      <td>2.277683</td>
      <td>0.842204</td>
      <td>1.889124</td>
      <td>1.724022</td>
    </tr>
  </tbody>
</table>
</div>



## Changing year columns to rows and filtering to same countries GTD dataset have


```python
gdpRaw = gdpRaw.melt(id_vars=["Country Name", "Country Code"], 
        var_name="Year", 
        value_name="GDP")
gdpRaw.head()
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
      <th>Country Name</th>
      <th>Country Code</th>
      <th>Year</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aruba</td>
      <td>ABW</td>
      <td>2008</td>
      <td>-0.090708</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>AFG</td>
      <td>2008</td>
      <td>3.924984</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Angola</td>
      <td>AGO</td>
      <td>2008</td>
      <td>11.166138</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>ALB</td>
      <td>2008</td>
      <td>7.499970</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Andorra</td>
      <td>AND</td>
      <td>2008</td>
      <td>-8.590004</td>
    </tr>
  </tbody>
</table>
</div>




```python
gdpRaw = gdpRaw[(gdpRaw["Country Name"].isin(topCountryEachRegion))]
del gdpRaw['Country Code']
gdpRaw.head()
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
      <th>Country Name</th>
      <th>Year</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11</th>
      <td>Australia</td>
      <td>2008</td>
      <td>3.657944</td>
    </tr>
    <tr>
      <th>38</th>
      <td>China</td>
      <td>2008</td>
      <td>9.654289</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Colombia</td>
      <td>2008</td>
      <td>3.257048</td>
    </tr>
    <tr>
      <th>79</th>
      <td>United Kingdom</td>
      <td>2008</td>
      <td>-0.345861</td>
    </tr>
    <tr>
      <th>80</th>
      <td>Georgia</td>
      <td>2008</td>
      <td>2.418572</td>
    </tr>
  </tbody>
</table>
</div>




```python
groupData = terrorRaw[["Year", "Country", "Casualities"]]
#groupData = groupData.groupby(['Year','Country'])['Casualities'].sum().to_frame()
groupData = groupData.groupby(['Year','Country']).agg({'Country': 'count', 'Casualities': 'sum'}).rename(columns={'Country': 'Total Attacks Count'})
groupData = groupData.reset_index()
groupData.head()
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
      <th>Year</th>
      <th>Country</th>
      <th>Total Attacks Count</th>
      <th>Casualities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2008</td>
      <td>Australia</td>
      <td>3</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2008</td>
      <td>China</td>
      <td>20</td>
      <td>189.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2008</td>
      <td>Colombia</td>
      <td>133</td>
      <td>323.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2008</td>
      <td>Georgia</td>
      <td>33</td>
      <td>75.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2008</td>
      <td>Iraq</td>
      <td>1106</td>
      <td>9414.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
totCount = groupData["Total Attacks Count"].sum()
percOfCountry = (groupData["Total Attacks Count"]/totCount) * 100
groupData["Total Attacks"] = percOfCountry
groupData.head()
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
      <th>Year</th>
      <th>Country</th>
      <th>Total Attacks Count</th>
      <th>Casualities</th>
      <th>Total Attacks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2008</td>
      <td>Australia</td>
      <td>3</td>
      <td>0.0</td>
      <td>0.006536</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2008</td>
      <td>China</td>
      <td>20</td>
      <td>189.0</td>
      <td>0.043574</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2008</td>
      <td>Colombia</td>
      <td>133</td>
      <td>323.0</td>
      <td>0.289767</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2008</td>
      <td>Georgia</td>
      <td>33</td>
      <td>75.0</td>
      <td>0.071897</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2008</td>
      <td>Iraq</td>
      <td>1106</td>
      <td>9414.0</td>
      <td>2.409639</td>
    </tr>
  </tbody>
</table>
</div>



## Changing the column data type  to same for merging datasets


```python
terrorRaw.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 45899 entries, 0 to 45898
    Data columns (total 3 columns):
    Year           45899 non-null int64
    Country        45899 non-null object
    Casualities    43264 non-null float64
    dtypes: float64(1), int64(1), object(1)
    memory usage: 1.1+ MB
    


```python
gdpRaw.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 120 entries, 11 to 2625
    Data columns (total 3 columns):
    Country Name    120 non-null object
    Year            120 non-null object
    GDP             110 non-null float64
    dtypes: float64(1), object(2)
    memory usage: 3.8+ KB
    


```python
gdpRaw['Year'] = gdpRaw['Year'].astype('int64')
gdpRaw.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 120 entries, 11 to 2625
    Data columns (total 3 columns):
    Country Name    120 non-null object
    Year            120 non-null int64
    GDP             110 non-null float64
    dtypes: float64(1), int64(1), object(1)
    memory usage: 3.8+ KB
    


```python
# new_df = pd.merge(A_df, B_df,  how='left', left_on=['A_c1','c2'], right_on = ['B_c1','c2'])
mergedData = pd.merge(groupData, gdpRaw, how='outer', left_on=['Year', 'Country'], right_on=['Year', 'Country Name'])
mergedData = mergedData.sort_values(by=['Year', 'Country'])
mergedData.head()
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
      <th>Year</th>
      <th>Country</th>
      <th>Total Attacks Count</th>
      <th>Casualities</th>
      <th>Total Attacks</th>
      <th>Country Name</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2008</td>
      <td>Australia</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>0.006536</td>
      <td>Australia</td>
      <td>3.657944</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2008</td>
      <td>China</td>
      <td>20.0</td>
      <td>189.0</td>
      <td>0.043574</td>
      <td>China</td>
      <td>9.654289</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2008</td>
      <td>Colombia</td>
      <td>133.0</td>
      <td>323.0</td>
      <td>0.289767</td>
      <td>Colombia</td>
      <td>3.257048</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2008</td>
      <td>Georgia</td>
      <td>33.0</td>
      <td>75.0</td>
      <td>0.071897</td>
      <td>Georgia</td>
      <td>2.418572</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2008</td>
      <td>Iraq</td>
      <td>1106.0</td>
      <td>9414.0</td>
      <td>2.409639</td>
      <td>Iraq</td>
      <td>8.228107</td>
    </tr>
  </tbody>
</table>
</div>




```python
mergedData = mergedData.dropna(axis='columns', how='all')
mergedData = mergedData[['Year', 'Country', 'Total Attacks', 'Total Attacks Count', 'Casualities', 'GDP']]
mergedData.head()
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
      <th>Year</th>
      <th>Country</th>
      <th>Total Attacks</th>
      <th>Total Attacks Count</th>
      <th>Casualities</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2008</td>
      <td>Australia</td>
      <td>0.006536</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>3.657944</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2008</td>
      <td>China</td>
      <td>0.043574</td>
      <td>20.0</td>
      <td>189.0</td>
      <td>9.654289</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2008</td>
      <td>Colombia</td>
      <td>0.289767</td>
      <td>133.0</td>
      <td>323.0</td>
      <td>3.257048</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2008</td>
      <td>Georgia</td>
      <td>0.071897</td>
      <td>33.0</td>
      <td>75.0</td>
      <td>2.418572</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2008</td>
      <td>Iraq</td>
      <td>2.409639</td>
      <td>1106.0</td>
      <td>9414.0</td>
      <td>8.228107</td>
    </tr>
  </tbody>
</table>
</div>




```python
mergedData.to_csv('GTD_Data/gtd_gdp_final_analysis.csv')
```

# Final dataset is ready for the analysis


```python

```
