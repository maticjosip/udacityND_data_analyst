
# PISA Data Findings
## by Josip Matic  

## Introduction

### PISA

> PISA is a worldwide study developed by the Organisation for Economic Co-operation and Development (OECD) to examine the skills of 15-year-old school students around the world. The study assesses students’ maths, science, and reading skills and contains a wealth of information on students’ background, their school and the organisation of the education system. For most countries, the sample is around 5,000 students, but in some countries the number is even higher. [source: https://www.oecd.org/pisa/  ]

This dataset used for this project is from the PISA study in 2012.

## Import and Load


```python
# import all packages and set plots to be embedded inline
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.style as style
style.available
style.use('ggplot')
import seaborn as sb

%matplotlib inline
```

I am using two datasets. *pisa* will be the main dataset with all the records from 2012. and *pisa_dict* will be used as an encryption for the column names.


```python
# Used other encoding as encoding error occured, therefore, default UTF-8 could not be used
# low_memory is used to supress an error notification
pisa = pd.read_csv(r'C:\Users\Josip\Documents\_Udacity\ND_DA\5_Assessment\pisa2012.csv', encoding = "ISO-8859-1", low_memory=False)
pisa_dict = pd.read_csv(r'C:\Users\Josip\Documents\_Udacity\ND_DA\5_Assessment\pisadict2012.csv', encoding = "ISO-8859-1", names=['ColName','Definition'])
```

## Data Assessment  
### What is the structure of your dataset?  


```python
pisa.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 485490 entries, 0 to 485489
    Columns: 636 entries, Unnamed: 0 to VER_STU
    dtypes: float64(250), int64(18), object(368)
    memory usage: 2.3+ GB
    

The dataset contains float, integer and strings and is more than 2.3 GB in size.


```python
pisa_dict.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 636 entries, 0 to 635
    Data columns (total 2 columns):
    ColName       635 non-null object
    Definition    636 non-null object
    dtypes: object(2)
    memory usage: 10.0+ KB
    

This dataset is an additional source of information for the main dataset *pisa*. It describes in detail the column names. The column ColName has one object missing. This will be investigated later.


```python
# As the dataset contains 636 variables this function enables to display all columns and content of each cell
# for the dataset pisa_dict
pd.set_option('display.max_rows', 636)
# for the dataset pisa
pd.set_option('display.max_columns', 636)
# Displays complete content of each cell
pd.set_option('display.max_colwidth', -1)
```


```python
pisa.shape
```




    (485490, 636)



There are in total 636 variables and a little less than half a million records.


```python
pisa.sample(10)
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
      <th>Unnamed: 0</th>
      <th>CNT</th>
      <th>SUBNATIO</th>
      <th>STRATUM</th>
      <th>OECD</th>
      <th>NC</th>
      <th>SCHOOLID</th>
      <th>STIDSTD</th>
      <th>ST01Q01</th>
      <th>ST02Q01</th>
      <th>ST03Q01</th>
      <th>ST03Q02</th>
      <th>ST04Q01</th>
      <th>ST05Q01</th>
      <th>ST06Q01</th>
      <th>ST07Q01</th>
      <th>ST07Q02</th>
      <th>ST07Q03</th>
      <th>ST08Q01</th>
      <th>ST09Q01</th>
      <th>ST115Q01</th>
      <th>ST11Q01</th>
      <th>ST11Q02</th>
      <th>ST11Q03</th>
      <th>ST11Q04</th>
      <th>ST11Q05</th>
      <th>ST11Q06</th>
      <th>ST13Q01</th>
      <th>ST14Q01</th>
      <th>ST14Q02</th>
      <th>ST14Q03</th>
      <th>ST14Q04</th>
      <th>ST15Q01</th>
      <th>ST17Q01</th>
      <th>ST18Q01</th>
      <th>ST18Q02</th>
      <th>ST18Q03</th>
      <th>ST18Q04</th>
      <th>ST19Q01</th>
      <th>ST20Q01</th>
      <th>ST20Q02</th>
      <th>ST20Q03</th>
      <th>ST21Q01</th>
      <th>ST25Q01</th>
      <th>ST26Q01</th>
      <th>ST26Q02</th>
      <th>ST26Q03</th>
      <th>ST26Q04</th>
      <th>ST26Q05</th>
      <th>ST26Q06</th>
      <th>ST26Q07</th>
      <th>ST26Q08</th>
      <th>ST26Q09</th>
      <th>ST26Q10</th>
      <th>ST26Q11</th>
      <th>ST26Q12</th>
      <th>ST26Q13</th>
      <th>ST26Q14</th>
      <th>ST26Q15</th>
      <th>ST26Q16</th>
      <th>ST26Q17</th>
      <th>ST27Q01</th>
      <th>ST27Q02</th>
      <th>ST27Q03</th>
      <th>ST27Q04</th>
      <th>ST27Q05</th>
      <th>ST28Q01</th>
      <th>ST29Q01</th>
      <th>ST29Q02</th>
      <th>ST29Q03</th>
      <th>ST29Q04</th>
      <th>ST29Q05</th>
      <th>ST29Q06</th>
      <th>ST29Q07</th>
      <th>ST29Q08</th>
      <th>ST35Q01</th>
      <th>ST35Q02</th>
      <th>ST35Q03</th>
      <th>ST35Q04</th>
      <th>ST35Q05</th>
      <th>ST35Q06</th>
      <th>ST37Q01</th>
      <th>ST37Q02</th>
      <th>ST37Q03</th>
      <th>ST37Q04</th>
      <th>ST37Q05</th>
      <th>ST37Q06</th>
      <th>ST37Q07</th>
      <th>ST37Q08</th>
      <th>ST42Q01</th>
      <th>ST42Q02</th>
      <th>ST42Q03</th>
      <th>ST42Q04</th>
      <th>ST42Q05</th>
      <th>ST42Q06</th>
      <th>ST42Q07</th>
      <th>ST42Q08</th>
      <th>ST42Q09</th>
      <th>ST42Q10</th>
      <th>ST43Q01</th>
      <th>ST43Q02</th>
      <th>ST43Q03</th>
      <th>ST43Q04</th>
      <th>ST43Q05</th>
      <th>ST43Q06</th>
      <th>ST44Q01</th>
      <th>ST44Q03</th>
      <th>ST44Q04</th>
      <th>ST44Q05</th>
      <th>ST44Q07</th>
      <th>ST44Q08</th>
      <th>ST46Q01</th>
      <th>ST46Q02</th>
      <th>ST46Q03</th>
      <th>ST46Q04</th>
      <th>ST46Q05</th>
      <th>ST46Q06</th>
      <th>ST46Q07</th>
      <th>ST46Q08</th>
      <th>ST46Q09</th>
      <th>ST48Q01</th>
      <th>ST48Q02</th>
      <th>ST48Q03</th>
      <th>ST48Q04</th>
      <th>ST48Q05</th>
      <th>ST49Q01</th>
      <th>ST49Q02</th>
      <th>ST49Q03</th>
      <th>ST49Q04</th>
      <th>ST49Q05</th>
      <th>ST49Q06</th>
      <th>ST49Q07</th>
      <th>ST49Q09</th>
      <th>ST53Q01</th>
      <th>ST53Q02</th>
      <th>ST53Q03</th>
      <th>ST53Q04</th>
      <th>ST55Q01</th>
      <th>ST55Q02</th>
      <th>ST55Q03</th>
      <th>ST55Q04</th>
      <th>ST57Q01</th>
      <th>ST57Q02</th>
      <th>ST57Q03</th>
      <th>ST57Q04</th>
      <th>ST57Q05</th>
      <th>ST57Q06</th>
      <th>ST61Q01</th>
      <th>ST61Q02</th>
      <th>ST61Q03</th>
      <th>ST61Q04</th>
      <th>ST61Q05</th>
      <th>ST61Q06</th>
      <th>ST61Q07</th>
      <th>ST61Q08</th>
      <th>ST61Q09</th>
      <th>ST62Q01</th>
      <th>ST62Q02</th>
      <th>ST62Q03</th>
      <th>ST62Q04</th>
      <th>ST62Q06</th>
      <th>ST62Q07</th>
      <th>ST62Q08</th>
      <th>ST62Q09</th>
      <th>ST62Q10</th>
      <th>ST62Q11</th>
      <th>ST62Q12</th>
      <th>ST62Q13</th>
      <th>ST62Q15</th>
      <th>ST62Q16</th>
      <th>ST62Q17</th>
      <th>ST62Q19</th>
      <th>ST69Q01</th>
      <th>ST69Q02</th>
      <th>ST69Q03</th>
      <th>ST70Q01</th>
      <th>ST70Q02</th>
      <th>ST70Q03</th>
      <th>ST71Q01</th>
      <th>ST72Q01</th>
      <th>ST73Q01</th>
      <th>ST73Q02</th>
      <th>ST74Q01</th>
      <th>ST74Q02</th>
      <th>ST75Q01</th>
      <th>ST75Q02</th>
      <th>ST76Q01</th>
      <th>ST76Q02</th>
      <th>ST77Q01</th>
      <th>ST77Q02</th>
      <th>ST77Q04</th>
      <th>ST77Q05</th>
      <th>ST77Q06</th>
      <th>ST79Q01</th>
      <th>ST79Q02</th>
      <th>ST79Q03</th>
      <th>ST79Q04</th>
      <th>ST79Q05</th>
      <th>ST79Q06</th>
      <th>ST79Q07</th>
      <th>ST79Q08</th>
      <th>ST79Q10</th>
      <th>ST79Q11</th>
      <th>ST79Q12</th>
      <th>ST79Q15</th>
      <th>ST79Q17</th>
      <th>ST80Q01</th>
      <th>ST80Q04</th>
      <th>ST80Q05</th>
      <th>ST80Q06</th>
      <th>ST80Q07</th>
      <th>ST80Q08</th>
      <th>ST80Q09</th>
      <th>ST80Q10</th>
      <th>ST80Q11</th>
      <th>ST81Q01</th>
      <th>ST81Q02</th>
      <th>ST81Q03</th>
      <th>ST81Q04</th>
      <th>ST81Q05</th>
      <th>ST82Q01</th>
      <th>ST82Q02</th>
      <th>ST82Q03</th>
      <th>ST83Q01</th>
      <th>ST83Q02</th>
      <th>ST83Q03</th>
      <th>ST83Q04</th>
      <th>ST84Q01</th>
      <th>ST84Q02</th>
      <th>ST84Q03</th>
      <th>ST85Q01</th>
      <th>ST85Q02</th>
      <th>ST85Q03</th>
      <th>ST85Q04</th>
      <th>ST86Q01</th>
      <th>ST86Q02</th>
      <th>ST86Q03</th>
      <th>ST86Q04</th>
      <th>ST86Q05</th>
      <th>ST87Q01</th>
      <th>ST87Q02</th>
      <th>ST87Q03</th>
      <th>ST87Q04</th>
      <th>ST87Q05</th>
      <th>ST87Q06</th>
      <th>ST87Q07</th>
      <th>ST87Q08</th>
      <th>ST87Q09</th>
      <th>ST88Q01</th>
      <th>ST88Q02</th>
      <th>ST88Q03</th>
      <th>ST88Q04</th>
      <th>ST89Q02</th>
      <th>ST89Q03</th>
      <th>ST89Q04</th>
      <th>ST89Q05</th>
      <th>ST91Q01</th>
      <th>ST91Q02</th>
      <th>ST91Q03</th>
      <th>ST91Q04</th>
      <th>ST91Q05</th>
      <th>ST91Q06</th>
      <th>ST93Q01</th>
      <th>ST93Q03</th>
      <th>ST93Q04</th>
      <th>ST93Q06</th>
      <th>ST93Q07</th>
      <th>ST94Q05</th>
      <th>ST94Q06</th>
      <th>ST94Q09</th>
      <th>ST94Q10</th>
      <th>ST94Q14</th>
      <th>ST96Q01</th>
      <th>ST96Q02</th>
      <th>ST96Q03</th>
      <th>ST96Q05</th>
      <th>ST101Q01</th>
      <th>ST101Q02</th>
      <th>ST101Q03</th>
      <th>ST101Q05</th>
      <th>ST104Q01</th>
      <th>ST104Q04</th>
      <th>ST104Q05</th>
      <th>ST104Q06</th>
      <th>IC01Q01</th>
      <th>IC01Q02</th>
      <th>IC01Q03</th>
      <th>IC01Q04</th>
      <th>IC01Q05</th>
      <th>IC01Q06</th>
      <th>IC01Q07</th>
      <th>IC01Q08</th>
      <th>IC01Q09</th>
      <th>IC01Q10</th>
      <th>IC01Q11</th>
      <th>IC02Q01</th>
      <th>IC02Q02</th>
      <th>IC02Q03</th>
      <th>IC02Q04</th>
      <th>IC02Q05</th>
      <th>IC02Q06</th>
      <th>IC02Q07</th>
      <th>IC03Q01</th>
      <th>IC04Q01</th>
      <th>IC05Q01</th>
      <th>IC06Q01</th>
      <th>IC07Q01</th>
      <th>IC08Q01</th>
      <th>IC08Q02</th>
      <th>IC08Q03</th>
      <th>IC08Q04</th>
      <th>IC08Q05</th>
      <th>IC08Q06</th>
      <th>IC08Q07</th>
      <th>IC08Q08</th>
      <th>IC08Q09</th>
      <th>IC08Q11</th>
      <th>IC09Q01</th>
      <th>IC09Q02</th>
      <th>IC09Q03</th>
      <th>IC09Q04</th>
      <th>IC09Q05</th>
      <th>IC09Q06</th>
      <th>IC09Q07</th>
      <th>IC10Q01</th>
      <th>IC10Q02</th>
      <th>IC10Q03</th>
      <th>IC10Q04</th>
      <th>IC10Q05</th>
      <th>IC10Q06</th>
      <th>IC10Q07</th>
      <th>IC10Q08</th>
      <th>IC10Q09</th>
      <th>IC11Q01</th>
      <th>IC11Q02</th>
      <th>IC11Q03</th>
      <th>IC11Q04</th>
      <th>IC11Q05</th>
      <th>IC11Q06</th>
      <th>IC11Q07</th>
      <th>IC22Q01</th>
      <th>IC22Q02</th>
      <th>IC22Q04</th>
      <th>IC22Q06</th>
      <th>IC22Q07</th>
      <th>IC22Q08</th>
      <th>EC01Q01</th>
      <th>EC02Q01</th>
      <th>EC03Q01</th>
      <th>EC03Q02</th>
      <th>EC03Q03</th>
      <th>EC03Q04</th>
      <th>EC03Q05</th>
      <th>EC03Q06</th>
      <th>EC03Q07</th>
      <th>EC03Q08</th>
      <th>EC03Q09</th>
      <th>EC03Q10</th>
      <th>EC04Q01A</th>
      <th>EC04Q01B</th>
      <th>EC04Q01C</th>
      <th>EC04Q02A</th>
      <th>EC04Q02B</th>
      <th>EC04Q02C</th>
      <th>EC04Q03A</th>
      <th>EC04Q03B</th>
      <th>EC04Q03C</th>
      <th>EC04Q04A</th>
      <th>EC04Q04B</th>
      <th>EC04Q04C</th>
      <th>EC04Q05A</th>
      <th>EC04Q05B</th>
      <th>EC04Q05C</th>
      <th>EC04Q06A</th>
      <th>EC04Q06B</th>
      <th>EC04Q06C</th>
      <th>EC05Q01</th>
      <th>EC06Q01</th>
      <th>EC07Q01</th>
      <th>EC07Q02</th>
      <th>EC07Q03</th>
      <th>EC07Q04</th>
      <th>EC07Q05</th>
      <th>EC08Q01</th>
      <th>EC08Q02</th>
      <th>EC08Q03</th>
      <th>EC08Q04</th>
      <th>EC09Q03</th>
      <th>EC10Q01</th>
      <th>EC11Q02</th>
      <th>EC11Q03</th>
      <th>EC12Q01</th>
      <th>ST22Q01</th>
      <th>ST23Q01</th>
      <th>ST23Q02</th>
      <th>ST23Q03</th>
      <th>ST23Q04</th>
      <th>ST23Q05</th>
      <th>ST23Q06</th>
      <th>ST23Q07</th>
      <th>ST23Q08</th>
      <th>ST24Q01</th>
      <th>ST24Q02</th>
      <th>ST24Q03</th>
      <th>CLCUSE1</th>
      <th>CLCUSE301</th>
      <th>CLCUSE302</th>
      <th>DEFFORT</th>
      <th>QUESTID</th>
      <th>BOOKID</th>
      <th>EASY</th>
      <th>AGE</th>
      <th>GRADE</th>
      <th>PROGN</th>
      <th>ANXMAT</th>
      <th>ATSCHL</th>
      <th>ATTLNACT</th>
      <th>BELONG</th>
      <th>BFMJ2</th>
      <th>BMMJ1</th>
      <th>CLSMAN</th>
      <th>COBN_F</th>
      <th>COBN_M</th>
      <th>COBN_S</th>
      <th>COGACT</th>
      <th>CULTDIST</th>
      <th>CULTPOS</th>
      <th>DISCLIMA</th>
      <th>ENTUSE</th>
      <th>ESCS</th>
      <th>EXAPPLM</th>
      <th>EXPUREM</th>
      <th>FAILMAT</th>
      <th>FAMCON</th>
      <th>FAMCONC</th>
      <th>FAMSTRUC</th>
      <th>FISCED</th>
      <th>HEDRES</th>
      <th>HERITCUL</th>
      <th>HISCED</th>
      <th>HISEI</th>
      <th>HOMEPOS</th>
      <th>HOMSCH</th>
      <th>HOSTCUL</th>
      <th>ICTATTNEG</th>
      <th>ICTATTPOS</th>
      <th>ICTHOME</th>
      <th>ICTRES</th>
      <th>ICTSCH</th>
      <th>IMMIG</th>
      <th>INFOCAR</th>
      <th>INFOJOB1</th>
      <th>INFOJOB2</th>
      <th>INSTMOT</th>
      <th>INTMAT</th>
      <th>ISCEDD</th>
      <th>ISCEDL</th>
      <th>ISCEDO</th>
      <th>LANGCOMM</th>
      <th>LANGN</th>
      <th>LANGRPPD</th>
      <th>LMINS</th>
      <th>MATBEH</th>
      <th>MATHEFF</th>
      <th>MATINTFC</th>
      <th>MATWKETH</th>
      <th>MISCED</th>
      <th>MMINS</th>
      <th>MTSUP</th>
      <th>OCOD1</th>
      <th>OCOD2</th>
      <th>OPENPS</th>
      <th>OUTHOURS</th>
      <th>PARED</th>
      <th>PERSEV</th>
      <th>REPEAT</th>
      <th>SCMAT</th>
      <th>SMINS</th>
      <th>STUDREL</th>
      <th>SUBNORM</th>
      <th>TCHBEHFA</th>
      <th>TCHBEHSO</th>
      <th>TCHBEHTD</th>
      <th>TEACHSUP</th>
      <th>TESTLANG</th>
      <th>TIMEINT</th>
      <th>USEMATH</th>
      <th>USESCH</th>
      <th>WEALTH</th>
      <th>ANCATSCHL</th>
      <th>ANCATTLNACT</th>
      <th>ANCBELONG</th>
      <th>ANCCLSMAN</th>
      <th>ANCCOGACT</th>
      <th>ANCINSTMOT</th>
      <th>ANCINTMAT</th>
      <th>ANCMATWKETH</th>
      <th>ANCMTSUP</th>
      <th>ANCSCMAT</th>
      <th>ANCSTUDREL</th>
      <th>ANCSUBNORM</th>
      <th>PV1MATH</th>
      <th>PV2MATH</th>
      <th>PV3MATH</th>
      <th>PV4MATH</th>
      <th>PV5MATH</th>
      <th>PV1MACC</th>
      <th>PV2MACC</th>
      <th>PV3MACC</th>
      <th>PV4MACC</th>
      <th>PV5MACC</th>
      <th>PV1MACQ</th>
      <th>PV2MACQ</th>
      <th>PV3MACQ</th>
      <th>PV4MACQ</th>
      <th>PV5MACQ</th>
      <th>PV1MACS</th>
      <th>PV2MACS</th>
      <th>PV3MACS</th>
      <th>PV4MACS</th>
      <th>PV5MACS</th>
      <th>PV1MACU</th>
      <th>PV2MACU</th>
      <th>PV3MACU</th>
      <th>PV4MACU</th>
      <th>PV5MACU</th>
      <th>PV1MAPE</th>
      <th>PV2MAPE</th>
      <th>PV3MAPE</th>
      <th>PV4MAPE</th>
      <th>PV5MAPE</th>
      <th>PV1MAPF</th>
      <th>PV2MAPF</th>
      <th>PV3MAPF</th>
      <th>PV4MAPF</th>
      <th>PV5MAPF</th>
      <th>PV1MAPI</th>
      <th>PV2MAPI</th>
      <th>PV3MAPI</th>
      <th>PV4MAPI</th>
      <th>PV5MAPI</th>
      <th>PV1READ</th>
      <th>PV2READ</th>
      <th>PV3READ</th>
      <th>PV4READ</th>
      <th>PV5READ</th>
      <th>PV1SCIE</th>
      <th>PV2SCIE</th>
      <th>PV3SCIE</th>
      <th>PV4SCIE</th>
      <th>PV5SCIE</th>
      <th>W_FSTUWT</th>
      <th>W_FSTR1</th>
      <th>W_FSTR2</th>
      <th>W_FSTR3</th>
      <th>W_FSTR4</th>
      <th>W_FSTR5</th>
      <th>W_FSTR6</th>
      <th>W_FSTR7</th>
      <th>W_FSTR8</th>
      <th>W_FSTR9</th>
      <th>W_FSTR10</th>
      <th>W_FSTR11</th>
      <th>W_FSTR12</th>
      <th>W_FSTR13</th>
      <th>W_FSTR14</th>
      <th>W_FSTR15</th>
      <th>W_FSTR16</th>
      <th>W_FSTR17</th>
      <th>W_FSTR18</th>
      <th>W_FSTR19</th>
      <th>W_FSTR20</th>
      <th>W_FSTR21</th>
      <th>W_FSTR22</th>
      <th>W_FSTR23</th>
      <th>W_FSTR24</th>
      <th>W_FSTR25</th>
      <th>W_FSTR26</th>
      <th>W_FSTR27</th>
      <th>W_FSTR28</th>
      <th>W_FSTR29</th>
      <th>W_FSTR30</th>
      <th>W_FSTR31</th>
      <th>W_FSTR32</th>
      <th>W_FSTR33</th>
      <th>W_FSTR34</th>
      <th>W_FSTR35</th>
      <th>W_FSTR36</th>
      <th>W_FSTR37</th>
      <th>W_FSTR38</th>
      <th>W_FSTR39</th>
      <th>W_FSTR40</th>
      <th>W_FSTR41</th>
      <th>W_FSTR42</th>
      <th>W_FSTR43</th>
      <th>W_FSTR44</th>
      <th>W_FSTR45</th>
      <th>W_FSTR46</th>
      <th>W_FSTR47</th>
      <th>W_FSTR48</th>
      <th>W_FSTR49</th>
      <th>W_FSTR50</th>
      <th>W_FSTR51</th>
      <th>W_FSTR52</th>
      <th>W_FSTR53</th>
      <th>W_FSTR54</th>
      <th>W_FSTR55</th>
      <th>W_FSTR56</th>
      <th>W_FSTR57</th>
      <th>W_FSTR58</th>
      <th>W_FSTR59</th>
      <th>W_FSTR60</th>
      <th>W_FSTR61</th>
      <th>W_FSTR62</th>
      <th>W_FSTR63</th>
      <th>W_FSTR64</th>
      <th>W_FSTR65</th>
      <th>W_FSTR66</th>
      <th>W_FSTR67</th>
      <th>W_FSTR68</th>
      <th>W_FSTR69</th>
      <th>W_FSTR70</th>
      <th>W_FSTR71</th>
      <th>W_FSTR72</th>
      <th>W_FSTR73</th>
      <th>W_FSTR74</th>
      <th>W_FSTR75</th>
      <th>W_FSTR76</th>
      <th>W_FSTR77</th>
      <th>W_FSTR78</th>
      <th>W_FSTR79</th>
      <th>W_FSTR80</th>
      <th>WVARSTRR</th>
      <th>VAR_UNIT</th>
      <th>SENWGT_STU</th>
      <th>VER_STU</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>172961</th>
      <td>172962</td>
      <td>Estonia</td>
      <td>2330000</td>
      <td>EST0002</td>
      <td>OECD</td>
      <td>Estonia</td>
      <td>91</td>
      <td>2066</td>
      <td>9</td>
      <td>1.0</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>Yes, for more than one year</td>
      <td>7.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>NaN</td>
      <td>Three or four times</td>
      <td>None</td>
      <td>4.0</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>&lt;ISCED level 3A&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>&lt;ISCED level 3A&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>233001</td>
      <td>233001</td>
      <td>233001</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>One</td>
      <td>None</td>
      <td>One</td>
      <td>11-25 books</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>relating to known</td>
      <td>Improve understanding</td>
      <td>learning goals</td>
      <td>Repeat examples</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>Less than 2 hours a week</td>
      <td>20.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Never</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Heard of it a few times</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it often</td>
      <td>Heard of it often</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it often</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it often</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>4.0</td>
      <td>36.0</td>
      <td>17.0</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Often</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Often</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Disagree</td>
      <td>Strongly disagree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, but I dont use it</td>
      <td>No</td>
      <td>No</td>
      <td>6 years old or younger</td>
      <td>6 years old or younger</td>
      <td>4</td>
      <td>6</td>
      <td>7</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Never or hardly ever</td>
      <td>Every day</td>
      <td>Every day</td>
      <td>Almost every day</td>
      <td>Once or twice a month</td>
      <td>Every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Once or twice a month</td>
      <td>Once or twice a month</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Once or twice a month</td>
      <td>No</td>
      <td>Yes, students did this</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>No</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A CAS calculator</td>
      <td>8</td>
      <td>9</td>
      <td>1</td>
      <td>StQ Form C</td>
      <td>booklet 12</td>
      <td>Standard set of booklets</td>
      <td>16.00</td>
      <td>0.0</td>
      <td>Estonia: Lower secondary</td>
      <td>-0.20</td>
      <td>-0.95</td>
      <td>-1.9158</td>
      <td>-1.18</td>
      <td>28.48</td>
      <td>32.50</td>
      <td>1.2923</td>
      <td>Estonia</td>
      <td>Estonia</td>
      <td>Estonia</td>
      <td>1.8326</td>
      <td>NaN</td>
      <td>0.25</td>
      <td>-0.08</td>
      <td>0.7450</td>
      <td>-0.76</td>
      <td>0.3220</td>
      <td>-1.5748</td>
      <td>NaN</td>
      <td>1.7020</td>
      <td>-0.48</td>
      <td>2.0</td>
      <td>ISCED 3A, ISCED 4</td>
      <td>1.12</td>
      <td>NaN</td>
      <td>ISCED 3A, ISCED 4</td>
      <td>32.50</td>
      <td>-0.45</td>
      <td>0.6173</td>
      <td>NaN</td>
      <td>0.3419</td>
      <td>0.0279</td>
      <td>0.1502</td>
      <td>-0.40</td>
      <td>-0.4166</td>
      <td>Native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>ISCED level 2</td>
      <td>General</td>
      <td>NaN</td>
      <td>Russian</td>
      <td>NaN</td>
      <td>180.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ISCED 3A, ISCED 4</td>
      <td>270.0</td>
      <td>1.8433</td>
      <td>Stock clerks</td>
      <td>Shop sales assistants</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>12.0</td>
      <td>NaN</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>-0.29</td>
      <td>180.0</td>
      <td>-0.48</td>
      <td>NaN</td>
      <td>-0.5945</td>
      <td>-0.5809</td>
      <td>-0.3204</td>
      <td>0.34</td>
      <td>Russian</td>
      <td>124.0</td>
      <td>0.5798</td>
      <td>1.1277</td>
      <td>-0.80</td>
      <td>0.1565</td>
      <td>-0.1839</td>
      <td>0.1459</td>
      <td>0.6690</td>
      <td>0.9446</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.8270</td>
      <td>0.6513</td>
      <td>0.3536</td>
      <td>NaN</td>
      <td>547.9903</td>
      <td>463.8651</td>
      <td>517.6118</td>
      <td>509.8224</td>
      <td>470.8755</td>
      <td>481.0017</td>
      <td>534.7484</td>
      <td>485.6753</td>
      <td>515.2750</td>
      <td>434.2655</td>
      <td>509.0435</td>
      <td>566.6848</td>
      <td>498.1383</td>
      <td>512.1592</td>
      <td>491.1279</td>
      <td>526.1801</td>
      <td>601.7370</td>
      <td>513.7171</td>
      <td>579.9268</td>
      <td>479.4438</td>
      <td>462.3072</td>
      <td>521.5065</td>
      <td>473.2123</td>
      <td>526.9590</td>
      <td>464.6440</td>
      <td>552.6640</td>
      <td>542.5378</td>
      <td>521.5065</td>
      <td>514.4960</td>
      <td>530.8537</td>
      <td>543.3167</td>
      <td>495.8015</td>
      <td>508.2645</td>
      <td>509.0435</td>
      <td>505.1488</td>
      <td>510.6013</td>
      <td>453.7389</td>
      <td>477.1070</td>
      <td>479.4438</td>
      <td>512.1592</td>
      <td>604.0768</td>
      <td>482.5473</td>
      <td>527.8230</td>
      <td>521.4685</td>
      <td>516.7027</td>
      <td>585.3599</td>
      <td>512.6259</td>
      <td>548.9929</td>
      <td>570.4401</td>
      <td>557.3853</td>
      <td>2.1525</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>1.0762</td>
      <td>1.0762</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>3.2287</td>
      <td>25</td>
      <td>2</td>
      <td>0.1851</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>209449</th>
      <td>209450</td>
      <td>Hong Kong-China</td>
      <td>3440000</td>
      <td>HKG0002</td>
      <td>Non-OECD</td>
      <td>Hong Kong-China</td>
      <td>83</td>
      <td>2549</td>
      <td>9</td>
      <td>1.0</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>Yes, for more than one year</td>
      <td>6.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>NaN</td>
      <td>None</td>
      <td>None</td>
      <td>1.0</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>&lt;ISCED level 3B, 3C&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Other (e.g. home duties, retired)</td>
      <td>&lt;ISCED level 1&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>Other country</td>
      <td>Other country</td>
      <td>Other country</td>
      <td>3.0</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>344001</td>
      <td>344002</td>
      <td>344002</td>
      <td>Three or more</td>
      <td>One</td>
      <td>One</td>
      <td>None</td>
      <td>One</td>
      <td>0-10 books</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Most important</td>
      <td>Improve understanding</td>
      <td>in my sleep</td>
      <td>everyday life</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it a few times</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it a few times</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it often</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>40.0</td>
      <td>40.0</td>
      <td>40.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>45.0</td>
      <td>35.0</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Most Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Every Lesson</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Often</td>
      <td>Often</td>
      <td>Always or almost always</td>
      <td>Never or rarely</td>
      <td>Often</td>
      <td>Often</td>
      <td>Sometimes</td>
      <td>Often</td>
      <td>Often</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, but I dont use it</td>
      <td>No</td>
      <td>Yes, but I dont use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>7-9 years old</td>
      <td>7-9 years old</td>
      <td>1</td>
      <td>4</td>
      <td>7</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Every day</td>
      <td>Every day</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>Yes, students did this</td>
      <td>Yes, students did this</td>
      <td>Yes, students did this</td>
      <td>No</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>No</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>Yes</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>Yes</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>&lt;test language&gt; or &lt;other official national language(s) or d</td>
      <td>0 to 3 years</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No, never</td>
      <td>NaN</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A Scientific calculator</td>
      <td>8</td>
      <td>8</td>
      <td>0</td>
      <td>StQ Form C</td>
      <td>booklet 10</td>
      <td>Standard set of booklets</td>
      <td>15.33</td>
      <td>-1.0</td>
      <td>Hong Kong-China: Lower Secondary in G  and  I Sch.</td>
      <td>0.56</td>
      <td>-0.95</td>
      <td>-0.9394</td>
      <td>-0.56</td>
      <td>43.85</td>
      <td>30.90</td>
      <td>2.1989</td>
      <td>China</td>
      <td>China</td>
      <td>Macao-China</td>
      <td>0.1015</td>
      <td>NaN</td>
      <td>-1.51</td>
      <td>1.85</td>
      <td>-0.7396</td>
      <td>-1.27</td>
      <td>-0.2531</td>
      <td>0.1674</td>
      <td>NaN</td>
      <td>0.9251</td>
      <td>0.41</td>
      <td>2.0</td>
      <td>ISCED 1</td>
      <td>-1.29</td>
      <td>NaN</td>
      <td>ISCED 3B, C</td>
      <td>43.85</td>
      <td>-1.71</td>
      <td>-0.6852</td>
      <td>NaN</td>
      <td>0.3419</td>
      <td>0.5519</td>
      <td>-0.6891</td>
      <td>-1.13</td>
      <td>-0.0836</td>
      <td>First-Generation</td>
      <td>-0.8214</td>
      <td>-0.3076</td>
      <td>-1.7507</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>ISCED level 2</td>
      <td>General</td>
      <td>NaN</td>
      <td>Cantonese</td>
      <td>NaN</td>
      <td>360.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ISCED 3B, C</td>
      <td>360.0</td>
      <td>0.6709</td>
      <td>Cashiers and ticket clerks</td>
      <td>Restaurant managers</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>-0.29</td>
      <td>360.0</td>
      <td>-0.79</td>
      <td>NaN</td>
      <td>0.2509</td>
      <td>-0.5809</td>
      <td>-0.0798</td>
      <td>-0.86</td>
      <td>Cantonese</td>
      <td>81.0</td>
      <td>1.1370</td>
      <td>-0.7854</td>
      <td>-1.38</td>
      <td>-0.6475</td>
      <td>-0.8775</td>
      <td>-0.5633</td>
      <td>-0.0983</td>
      <td>-0.1659</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.3007</td>
      <td>-0.3034</td>
      <td>-0.5138</td>
      <td>NaN</td>
      <td>561.7775</td>
      <td>577.3563</td>
      <td>571.9037</td>
      <td>539.9673</td>
      <td>585.1457</td>
      <td>541.5252</td>
      <td>471.4208</td>
      <td>558.6618</td>
      <td>536.0726</td>
      <td>544.6409</td>
      <td>603.0612</td>
      <td>524.3885</td>
      <td>616.3032</td>
      <td>585.9246</td>
      <td>603.8402</td>
      <td>608.5138</td>
      <td>533.7358</td>
      <td>589.0403</td>
      <td>592.1561</td>
      <td>583.5878</td>
      <td>506.4730</td>
      <td>471.4208</td>
      <td>546.9777</td>
      <td>521.2728</td>
      <td>543.0830</td>
      <td>565.6722</td>
      <td>539.9673</td>
      <td>581.2510</td>
      <td>536.8515</td>
      <td>560.9986</td>
      <td>598.3876</td>
      <td>521.2728</td>
      <td>610.8506</td>
      <td>526.7253</td>
      <td>597.6087</td>
      <td>550.0935</td>
      <td>485.4417</td>
      <td>528.2832</td>
      <td>532.1779</td>
      <td>494.7889</td>
      <td>569.6832</td>
      <td>536.3221</td>
      <td>563.3287</td>
      <td>518.8473</td>
      <td>569.6832</td>
      <td>580.5110</td>
      <td>550.6714</td>
      <td>586.1059</td>
      <td>532.9541</td>
      <td>559.9963</td>
      <td>15.5844</td>
      <td>23.8217</td>
      <td>7.4952</td>
      <td>7.6085</td>
      <td>7.8036</td>
      <td>23.1968</td>
      <td>8.0395</td>
      <td>22.7167</td>
      <td>8.0395</td>
      <td>22.7167</td>
      <td>22.9711</td>
      <td>23.8217</td>
      <td>24.4325</td>
      <td>8.4477</td>
      <td>7.6826</td>
      <td>22.0652</td>
      <td>8.0395</td>
      <td>7.4952</td>
      <td>23.1968</td>
      <td>22.9711</td>
      <td>8.2365</td>
      <td>7.6085</td>
      <td>22.9711</td>
      <td>23.8217</td>
      <td>24.4325</td>
      <td>8.4477</td>
      <td>22.7167</td>
      <td>8.0395</td>
      <td>22.7167</td>
      <td>8.0395</td>
      <td>7.4952</td>
      <td>7.6085</td>
      <td>7.8036</td>
      <td>23.1968</td>
      <td>23.5453</td>
      <td>8.0356</td>
      <td>22.7167</td>
      <td>22.9711</td>
      <td>8.4477</td>
      <td>7.4952</td>
      <td>22.6169</td>
      <td>23.8217</td>
      <td>7.8796</td>
      <td>7.6085</td>
      <td>7.4230</td>
      <td>22.0652</td>
      <td>8.0395</td>
      <td>22.7167</td>
      <td>8.0395</td>
      <td>22.7167</td>
      <td>24.1491</td>
      <td>23.8217</td>
      <td>23.2407</td>
      <td>8.0356</td>
      <td>7.6826</td>
      <td>23.1968</td>
      <td>8.0395</td>
      <td>7.8796</td>
      <td>22.0652</td>
      <td>24.1491</td>
      <td>8.2365</td>
      <td>7.6085</td>
      <td>24.1491</td>
      <td>23.8217</td>
      <td>23.2407</td>
      <td>8.0356</td>
      <td>22.7167</td>
      <td>8.0395</td>
      <td>22.7167</td>
      <td>8.0395</td>
      <td>7.8796</td>
      <td>7.6085</td>
      <td>7.4230</td>
      <td>22.0652</td>
      <td>23.5453</td>
      <td>8.4477</td>
      <td>22.7167</td>
      <td>24.1491</td>
      <td>8.0356</td>
      <td>7.8796</td>
      <td>22.6169</td>
      <td>53</td>
      <td>1</td>
      <td>0.2206</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>65566</th>
      <td>65567</td>
      <td>Brazil</td>
      <td>760000</td>
      <td>BRA2469</td>
      <td>Non-OECD</td>
      <td>Brazil</td>
      <td>454</td>
      <td>10301</td>
      <td>11</td>
      <td>1.0</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>Yes, for one year or less</td>
      <td>7.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>None</td>
      <td>None</td>
      <td>1.0</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>&lt;ISCED level 1&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>&lt;ISCED level 1&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>76001</td>
      <td>76002</td>
      <td>76002</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>One</td>
      <td>One</td>
      <td>One</td>
      <td>0-10 books</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>by heart</td>
      <td>Improve understanding</td>
      <td>learning goals</td>
      <td>Repeat examples</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>5.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>20.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Heard of it once or twice</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Heard of it often</td>
      <td>Never heard of it</td>
      <td>Heard of it once or twice</td>
      <td>Heard of it a few times</td>
      <td>Heard of it a few times</td>
      <td>Heard of it often</td>
      <td>Never heard of it</td>
      <td>Heard of it once or twice</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>Heard of it once or twice</td>
      <td>Heard of it a few times</td>
      <td>Heard of it once or twice</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>20.0</td>
      <td>35.0</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Never</td>
      <td>Never</td>
      <td>Never</td>
      <td>Never</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Never or rarely</td>
      <td>Sometimes</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Sometimes</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly disagree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97</td>
      <td>97</td>
      <td>97</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9</td>
      <td>9</td>
      <td>0</td>
      <td>StQ Form C</td>
      <td>booklet 27</td>
      <td>Easier set of booklets</td>
      <td>15.83</td>
      <td>0.0</td>
      <td>Brazil: Upper secondary education</td>
      <td>0.32</td>
      <td>2.35</td>
      <td>1.2115</td>
      <td>0.56</td>
      <td>22.57</td>
      <td>24.53</td>
      <td>-1.0878</td>
      <td>Brazil</td>
      <td>Brazil</td>
      <td>Brazil</td>
      <td>-1.4306</td>
      <td>NaN</td>
      <td>-0.48</td>
      <td>-0.71</td>
      <td>NaN</td>
      <td>-2.38</td>
      <td>0.5359</td>
      <td>-1.5748</td>
      <td>NaN</td>
      <td>-0.7159</td>
      <td>-0.66</td>
      <td>2.0</td>
      <td>ISCED 1</td>
      <td>0.01</td>
      <td>NaN</td>
      <td>ISCED 1</td>
      <td>24.53</td>
      <td>-0.98</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.40</td>
      <td>NaN</td>
      <td>Native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>ISCED level 3</td>
      <td>General</td>
      <td>NaN</td>
      <td>Portuguese</td>
      <td>NaN</td>
      <td>135.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ISCED 1</td>
      <td>180.0</td>
      <td>-0.6577</td>
      <td>Cooks</td>
      <td>Bricklayers and related workers</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>0.18</td>
      <td>90.0</td>
      <td>-0.02</td>
      <td>NaN</td>
      <td>0.7644</td>
      <td>-0.5809</td>
      <td>0.4297</td>
      <td>0.61</td>
      <td>Portuguese</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-1.03</td>
      <td>0.9305</td>
      <td>0.4908</td>
      <td>0.1459</td>
      <td>-0.3069</td>
      <td>-0.2061</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.2352</td>
      <td>0.1478</td>
      <td>-0.1113</td>
      <td>NaN</td>
      <td>421.7246</td>
      <td>420.9456</td>
      <td>417.0509</td>
      <td>443.5348</td>
      <td>390.5671</td>
      <td>395.2407</td>
      <td>466.9029</td>
      <td>398.3564</td>
      <td>377.3251</td>
      <td>397.5775</td>
      <td>422.5035</td>
      <td>480.1449</td>
      <td>425.6193</td>
      <td>380.4409</td>
      <td>427.9561</td>
      <td>393.6828</td>
      <td>445.8716</td>
      <td>413.1563</td>
      <td>386.6724</td>
      <td>404.5879</td>
      <td>375.7673</td>
      <td>434.9665</td>
      <td>374.9883</td>
      <td>349.2834</td>
      <td>372.6515</td>
      <td>464.5661</td>
      <td>415.4931</td>
      <td>425.6193</td>
      <td>397.5775</td>
      <td>427.9561</td>
      <td>424.0614</td>
      <td>376.5462</td>
      <td>403.8090</td>
      <td>387.4513</td>
      <td>392.1249</td>
      <td>430.2929</td>
      <td>395.2407</td>
      <td>428.7350</td>
      <td>397.5775</td>
      <td>424.8403</td>
      <td>483.1034</td>
      <td>487.8692</td>
      <td>463.2456</td>
      <td>481.5147</td>
      <td>484.6920</td>
      <td>433.6442</td>
      <td>471.8762</td>
      <td>475.6061</td>
      <td>485.8635</td>
      <td>428.0492</td>
      <td>72.3710</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>36.0862</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>109.9358</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>36.0862</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>109.9358</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>36.0862</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>109.9358</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>36.0862</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>109.9358</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>108.9221</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>35.8730</td>
      <td>36.0862</td>
      <td>109.9358</td>
      <td>48</td>
      <td>1</td>
      <td>0.0307</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>296416</th>
      <td>296417</td>
      <td>Lithuania</td>
      <td>4400000</td>
      <td>LTU0003</td>
      <td>Non-OECD</td>
      <td>Lithuania</td>
      <td>12</td>
      <td>231</td>
      <td>9</td>
      <td>4.0</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>Yes, for more than one year</td>
      <td>7.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>NaN</td>
      <td>None</td>
      <td>None</td>
      <td>1.0</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>&lt;ISCED level 3A&gt;</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>&lt;ISCED level 3A&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Not working, but looking for a job</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>440001</td>
      <td>440001</td>
      <td>440001</td>
      <td>Three or more</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>One</td>
      <td>One</td>
      <td>101-200 books</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Strongly disagree</td>
      <td>Disagree</td>
      <td>NaN</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly disagree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>relating to known</td>
      <td>new ways</td>
      <td>in my sleep</td>
      <td>more information</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>14.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>8.0</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>7.0</td>
      <td>32.0</td>
      <td>25.0</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Every Lesson</td>
      <td>Never or Hardly Ever</td>
      <td>Every Lesson</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Sometimes</td>
      <td>Often</td>
      <td>Often</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly disagree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97</td>
      <td>97</td>
      <td>97</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No calculator</td>
      <td>7</td>
      <td>9</td>
      <td>2</td>
      <td>StQ Form C</td>
      <td>booklet 5</td>
      <td>Standard set of booklets</td>
      <td>16.25</td>
      <td>0.0</td>
      <td>Lithuania: Lower Gymnasium</td>
      <td>-1.18</td>
      <td>1.38</td>
      <td>1.2115</td>
      <td>-0.15</td>
      <td>25.95</td>
      <td>70.50</td>
      <td>1.2923</td>
      <td>Lithuania</td>
      <td>Lithuania</td>
      <td>Lithuania</td>
      <td>1.2684</td>
      <td>NaN</td>
      <td>1.27</td>
      <td>-0.33</td>
      <td>NaN</td>
      <td>0.95</td>
      <td>-0.2531</td>
      <td>0.7955</td>
      <td>NaN</td>
      <td>-0.5977</td>
      <td>1.02</td>
      <td>1.0</td>
      <td>ISCED 3A, ISCED 4</td>
      <td>1.12</td>
      <td>NaN</td>
      <td>ISCED 5A, 6</td>
      <td>70.50</td>
      <td>0.74</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.24</td>
      <td>NaN</td>
      <td>Native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>ISCED level 2</td>
      <td>General</td>
      <td>NaN</td>
      <td>Lithuanian</td>
      <td>NaN</td>
      <td>225.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ISCED 5A, 6</td>
      <td>180.0</td>
      <td>1.8433</td>
      <td>Social work and counselling professionals</td>
      <td>Heavy truck and lorry drivers</td>
      <td>NaN</td>
      <td>25.0</td>
      <td>16.0</td>
      <td>NaN</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>0.65</td>
      <td>315.0</td>
      <td>0.81</td>
      <td>NaN</td>
      <td>0.2509</td>
      <td>-0.1057</td>
      <td>0.7228</td>
      <td>0.11</td>
      <td>Lithuanian</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.02</td>
      <td>0.6517</td>
      <td>0.4908</td>
      <td>0.1992</td>
      <td>0.6690</td>
      <td>0.8023</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.8270</td>
      <td>0.6513</td>
      <td>0.4759</td>
      <td>NaN</td>
      <td>465.6566</td>
      <td>525.6348</td>
      <td>485.9090</td>
      <td>459.4251</td>
      <td>466.4356</td>
      <td>458.6462</td>
      <td>418.1415</td>
      <td>460.2041</td>
      <td>461.7620</td>
      <td>453.9726</td>
      <td>496.8141</td>
      <td>453.9726</td>
      <td>475.7828</td>
      <td>496.0352</td>
      <td>459.4251</td>
      <td>481.2354</td>
      <td>408.7942</td>
      <td>476.5618</td>
      <td>460.9830</td>
      <td>420.4783</td>
      <td>452.4147</td>
      <td>437.6149</td>
      <td>438.3938</td>
      <td>454.7515</td>
      <td>455.5305</td>
      <td>468.7724</td>
      <td>476.5618</td>
      <td>488.2458</td>
      <td>444.6253</td>
      <td>509.2771</td>
      <td>456.3094</td>
      <td>441.5096</td>
      <td>465.6566</td>
      <td>402.5627</td>
      <td>470.3303</td>
      <td>460.9830</td>
      <td>457.8673</td>
      <td>501.4878</td>
      <td>431.3834</td>
      <td>499.1510</td>
      <td>472.3274</td>
      <td>479.5449</td>
      <td>482.7527</td>
      <td>457.8924</td>
      <td>464.3079</td>
      <td>444.9273</td>
      <td>493.4166</td>
      <td>485.0242</td>
      <td>453.3197</td>
      <td>465.4420</td>
      <td>7.1547</td>
      <td>10.9293</td>
      <td>10.9293</td>
      <td>11.0093</td>
      <td>10.9293</td>
      <td>3.6451</td>
      <td>3.4417</td>
      <td>10.5138</td>
      <td>3.6825</td>
      <td>3.4555</td>
      <td>10.5138</td>
      <td>10.9293</td>
      <td>3.6451</td>
      <td>3.4555</td>
      <td>3.4417</td>
      <td>3.4417</td>
      <td>10.5835</td>
      <td>3.6825</td>
      <td>10.5138</td>
      <td>3.6284</td>
      <td>10.5476</td>
      <td>10.9293</td>
      <td>10.9293</td>
      <td>11.0093</td>
      <td>10.9293</td>
      <td>3.6451</td>
      <td>3.4417</td>
      <td>10.5138</td>
      <td>3.6825</td>
      <td>3.4555</td>
      <td>10.5138</td>
      <td>10.9293</td>
      <td>3.6451</td>
      <td>3.4555</td>
      <td>3.4417</td>
      <td>3.4417</td>
      <td>10.5835</td>
      <td>3.6825</td>
      <td>10.5138</td>
      <td>3.6284</td>
      <td>10.5476</td>
      <td>10.9293</td>
      <td>10.9293</td>
      <td>11.0093</td>
      <td>10.9293</td>
      <td>3.6451</td>
      <td>3.4417</td>
      <td>10.5138</td>
      <td>3.6825</td>
      <td>3.4555</td>
      <td>10.5138</td>
      <td>10.9293</td>
      <td>3.6451</td>
      <td>3.4555</td>
      <td>3.4417</td>
      <td>3.4417</td>
      <td>10.5835</td>
      <td>3.6825</td>
      <td>10.5138</td>
      <td>3.6284</td>
      <td>10.5476</td>
      <td>10.9293</td>
      <td>10.9293</td>
      <td>11.0093</td>
      <td>10.9293</td>
      <td>3.6451</td>
      <td>3.4417</td>
      <td>10.5138</td>
      <td>3.6825</td>
      <td>3.4555</td>
      <td>10.5138</td>
      <td>10.9293</td>
      <td>3.6451</td>
      <td>3.4555</td>
      <td>3.4417</td>
      <td>3.4417</td>
      <td>10.5835</td>
      <td>3.6825</td>
      <td>10.5138</td>
      <td>3.6284</td>
      <td>10.5476</td>
      <td>71</td>
      <td>1</td>
      <td>0.2165</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>285521</th>
      <td>285522</td>
      <td>Kazakhstan</td>
      <td>3980000</td>
      <td>KAZ0038</td>
      <td>Non-OECD</td>
      <td>Kazakhstan</td>
      <td>16</td>
      <td>470</td>
      <td>10</td>
      <td>4.0</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>Yes, for one year or less</td>
      <td>6.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>NaN</td>
      <td>None</td>
      <td>One or two times</td>
      <td>2.0</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>&lt;ISCED level 3B, 3C&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>Working part-time &lt;for pay&gt;</td>
      <td>&lt;ISCED level 3A&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>398001</td>
      <td>398001</td>
      <td>398001</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>One</td>
      <td>One</td>
      <td>One</td>
      <td>11-25 books</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Most important</td>
      <td>check memory</td>
      <td>learning goals</td>
      <td>Repeat examples</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>2 or more but less than 4 hours a week</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Never heard of it</td>
      <td>Heard of it a few times</td>
      <td>Heard of it once or twice</td>
      <td>Heard of it once or twice</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it a few times</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it a few times</td>
      <td>Heard of it once or twice</td>
      <td>Heard of it often</td>
      <td>Heard of it often</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it a few times</td>
      <td>Heard of it often</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>19.0</td>
      <td>14.0</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Sometimes</td>
      <td>Often</td>
      <td>Often</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>NaN</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97</td>
      <td>97</td>
      <td>97</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A Simple calculator</td>
      <td>10</td>
      <td>9</td>
      <td>-1</td>
      <td>StQ Form C</td>
      <td>booklet 9</td>
      <td>Easier set of booklets</td>
      <td>15.67</td>
      <td>1.0</td>
      <td>Kazakhstan: Programme of technical and vocational education</td>
      <td>1.89</td>
      <td>-1.22</td>
      <td>0.5206</td>
      <td>0.08</td>
      <td>81.92</td>
      <td>68.70</td>
      <td>0.3255</td>
      <td>Kazakhstan</td>
      <td>Kazakhstan</td>
      <td>Kazakhstan</td>
      <td>0.1202</td>
      <td>NaN</td>
      <td>1.27</td>
      <td>-0.71</td>
      <td>NaN</td>
      <td>0.55</td>
      <td>-0.0681</td>
      <td>-0.2503</td>
      <td>NaN</td>
      <td>-0.2052</td>
      <td>-0.78</td>
      <td>2.0</td>
      <td>ISCED 5B</td>
      <td>1.12</td>
      <td>NaN</td>
      <td>ISCED 5B</td>
      <td>81.92</td>
      <td>-0.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.40</td>
      <td>NaN</td>
      <td>Native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>ISCED level 3</td>
      <td>Vocational</td>
      <td>NaN</td>
      <td>Kazakh</td>
      <td>NaN</td>
      <td>90.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ISCED 5B</td>
      <td>135.0</td>
      <td>0.6709</td>
      <td>Nursing professionals</td>
      <td>Specialist medical practitioners</td>
      <td>NaN</td>
      <td>10.0</td>
      <td>14.0</td>
      <td>NaN</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>-0.29</td>
      <td>225.0</td>
      <td>0.81</td>
      <td>NaN</td>
      <td>1.0416</td>
      <td>1.3823</td>
      <td>0.4297</td>
      <td>0.11</td>
      <td>Kazakh</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.61</td>
      <td>-2.7779</td>
      <td>-1.5921</td>
      <td>-1.7271</td>
      <td>-0.9781</td>
      <td>-1.6958</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-1.5787</td>
      <td>-2.0134</td>
      <td>-1.6365</td>
      <td>NaN</td>
      <td>360.0327</td>
      <td>405.9900</td>
      <td>437.9265</td>
      <td>367.0432</td>
      <td>385.7377</td>
      <td>391.1902</td>
      <td>388.8534</td>
      <td>430.1371</td>
      <td>402.8743</td>
      <td>384.1798</td>
      <td>396.6428</td>
      <td>377.1693</td>
      <td>404.4322</td>
      <td>418.4530</td>
      <td>365.4853</td>
      <td>408.3268</td>
      <td>398.2007</td>
      <td>444.1580</td>
      <td>464.4103</td>
      <td>395.8638</td>
      <td>403.6532</td>
      <td>390.4113</td>
      <td>416.8952</td>
      <td>423.9056</td>
      <td>395.8638</td>
      <td>372.4957</td>
      <td>456.6210</td>
      <td>350.6855</td>
      <td>430.9160</td>
      <td>342.8961</td>
      <td>458.1788</td>
      <td>483.1048</td>
      <td>342.1172</td>
      <td>469.8629</td>
      <td>374.8325</td>
      <td>353.8012</td>
      <td>413.7794</td>
      <td>295.3809</td>
      <td>363.9274</td>
      <td>338.2225</td>
      <td>295.0975</td>
      <td>346.4220</td>
      <td>349.6298</td>
      <td>327.1753</td>
      <td>345.6201</td>
      <td>323.3308</td>
      <td>387.6725</td>
      <td>415.6471</td>
      <td>355.0354</td>
      <td>423.1070</td>
      <td>72.2963</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>36.1482</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>108.4445</td>
      <td>72</td>
      <td>2</td>
      <td>0.3469</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>151658</th>
      <td>151659</td>
      <td>Spain</td>
      <td>7241300</td>
      <td>ESP1325</td>
      <td>OECD</td>
      <td>Spain</td>
      <td>215</td>
      <td>6076</td>
      <td>9</td>
      <td>1.0</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>Yes, for more than one year</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>Yes, once</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>1.0</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>&lt;ISCED level 2&gt;</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Working part-time &lt;for pay&gt;</td>
      <td>&lt;ISCED level 3A&gt;</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>724001</td>
      <td>724002</td>
      <td>724001</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>Two</td>
      <td>101-200 books</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Very confident</td>
      <td>Very confident</td>
      <td>Confident</td>
      <td>Very confident</td>
      <td>Confident</td>
      <td>Very confident</td>
      <td>Not very confident</td>
      <td>Very confident</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Very   Likely</td>
      <td>Likely</td>
      <td>Very   Likely</td>
      <td>Not at all likely</td>
      <td>Slightly likely</td>
      <td>Very   Likely</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Courses after school Math</td>
      <td>Major in college Math</td>
      <td>Study harder Math</td>
      <td>Maximum classes Math</td>
      <td>Pursuing a career Math</td>
      <td>Always or almost always</td>
      <td>Often</td>
      <td>Always or almost always</td>
      <td>Sometimes</td>
      <td>Always or almost always</td>
      <td>Often</td>
      <td>Always or almost always</td>
      <td>Sometimes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>NaN</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Always or almost always</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Strongly disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Very much like me</td>
      <td>Somewhat like me</td>
      <td>Mostly like me</td>
      <td>Very much like me</td>
      <td>Mostly like me</td>
      <td>Very much like me</td>
      <td>Somewhat like me</td>
      <td>Mostly like me</td>
      <td>Very much like me</td>
      <td>Somewhat like me</td>
      <td>definitely do this</td>
      <td>probably do this</td>
      <td>definitely do this</td>
      <td>probably not do this</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, but I dont use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, but I dont use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>7-9 years old</td>
      <td>10-12 years old</td>
      <td>2</td>
      <td>2</td>
      <td>7</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Every day</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Almost every day</td>
      <td>Once or twice a month</td>
      <td>Once or twice a month</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Yes, students did this</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>Yes, students did this</td>
      <td>No</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No calculator</td>
      <td>5</td>
      <td>10</td>
      <td>5</td>
      <td>StQ Form B</td>
      <td>booklet 3</td>
      <td>Standard set of booklets</td>
      <td>15.92</td>
      <td>-1.0</td>
      <td>Spain: Compulsory Secondary Education</td>
      <td>0.79</td>
      <td>-0.24</td>
      <td>1.2115</td>
      <td>1.84</td>
      <td>43.33</td>
      <td>16.38</td>
      <td>0.7640</td>
      <td>Madrid (ESP)</td>
      <td>Madrid (ESP)</td>
      <td>Madrid (ESP)</td>
      <td>3.2019</td>
      <td>NaN</td>
      <td>0.25</td>
      <td>-0.08</td>
      <td>-3.9749</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.6400</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>ISCED 5B</td>
      <td>0.04</td>
      <td>NaN</td>
      <td>ISCED 5B</td>
      <td>43.33</td>
      <td>0.62</td>
      <td>0.3007</td>
      <td>NaN</td>
      <td>1.3219</td>
      <td>0.5519</td>
      <td>1.0551</td>
      <td>0.24</td>
      <td>0.2340</td>
      <td>Native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.50</td>
      <td>1.51</td>
      <td>A</td>
      <td>ISCED level 2</td>
      <td>General</td>
      <td>NaN</td>
      <td>Spanish</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.2022</td>
      <td>0.54</td>
      <td>1.4565</td>
      <td>0.4684</td>
      <td>ISCED 5B</td>
      <td>NaN</td>
      <td>0.6709</td>
      <td>Domestic cleaners and helpers</td>
      <td>General office clerks</td>
      <td>0.4639</td>
      <td>NaN</td>
      <td>13.0</td>
      <td>0.0511</td>
      <td>Repeated a &lt;grade&gt;</td>
      <td>0.65</td>
      <td>NaN</td>
      <td>-0.02</td>
      <td>1.7943</td>
      <td>0.9766</td>
      <td>2.3831</td>
      <td>0.4297</td>
      <td>0.61</td>
      <td>Spanish</td>
      <td>73.0</td>
      <td>0.8695</td>
      <td>0.7571</td>
      <td>0.45</td>
      <td>-1.8636</td>
      <td>-1.2391</td>
      <td>-1.0822</td>
      <td>-1.3537</td>
      <td>-0.5365</td>
      <td>-1.3050</td>
      <td>-1.0475</td>
      <td>-1.4853</td>
      <td>-1.5787</td>
      <td>-1.1235</td>
      <td>-1.6365</td>
      <td>-1.3358</td>
      <td>457.7115</td>
      <td>394.6175</td>
      <td>396.1754</td>
      <td>381.3756</td>
      <td>410.1963</td>
      <td>400.0701</td>
      <td>414.0910</td>
      <td>417.2067</td>
      <td>375.1441</td>
      <td>426.5540</td>
      <td>379.8177</td>
      <td>415.6489</td>
      <td>411.7542</td>
      <td>359.5654</td>
      <td>386.8282</td>
      <td>397.7333</td>
      <td>386.8282</td>
      <td>405.5227</td>
      <td>372.8073</td>
      <td>349.4392</td>
      <td>358.0075</td>
      <td>379.8177</td>
      <td>381.3756</td>
      <td>328.4079</td>
      <td>364.2390</td>
      <td>409.4174</td>
      <td>374.3652</td>
      <td>388.3860</td>
      <td>424.2172</td>
      <td>385.2703</td>
      <td>363.4600</td>
      <td>385.2703</td>
      <td>375.1441</td>
      <td>383.7124</td>
      <td>333.0815</td>
      <td>378.2599</td>
      <td>350.2181</td>
      <td>421.8804</td>
      <td>388.3860</td>
      <td>347.8813</td>
      <td>329.5010</td>
      <td>352.7574</td>
      <td>347.9457</td>
      <td>337.5204</td>
      <td>314.2640</td>
      <td>366.3185</td>
      <td>353.2637</td>
      <td>280.5297</td>
      <td>321.5591</td>
      <td>353.2637</td>
      <td>32.8599</td>
      <td>50.2478</td>
      <td>49.2899</td>
      <td>49.4173</td>
      <td>50.0570</td>
      <td>16.9681</td>
      <td>16.2478</td>
      <td>48.5725</td>
      <td>16.3741</td>
      <td>16.6453</td>
      <td>48.4068</td>
      <td>48.5725</td>
      <td>16.4300</td>
      <td>16.4300</td>
      <td>16.3741</td>
      <td>15.8485</td>
      <td>49.6898</td>
      <td>15.8485</td>
      <td>51.0420</td>
      <td>16.2628</td>
      <td>50.2478</td>
      <td>50.2478</td>
      <td>49.2899</td>
      <td>49.4173</td>
      <td>50.0570</td>
      <td>16.9681</td>
      <td>16.2478</td>
      <td>48.5725</td>
      <td>16.3741</td>
      <td>16.6453</td>
      <td>48.4068</td>
      <td>48.5725</td>
      <td>16.4300</td>
      <td>16.4300</td>
      <td>16.3741</td>
      <td>15.8485</td>
      <td>49.6898</td>
      <td>15.8485</td>
      <td>51.0420</td>
      <td>16.2628</td>
      <td>50.2478</td>
      <td>50.2478</td>
      <td>49.2899</td>
      <td>49.4173</td>
      <td>50.0570</td>
      <td>16.9681</td>
      <td>16.2478</td>
      <td>48.5725</td>
      <td>16.3741</td>
      <td>16.6453</td>
      <td>48.4068</td>
      <td>48.5725</td>
      <td>16.4300</td>
      <td>16.4300</td>
      <td>16.3741</td>
      <td>15.8485</td>
      <td>49.6898</td>
      <td>15.8485</td>
      <td>51.0420</td>
      <td>16.2628</td>
      <td>50.2478</td>
      <td>50.2478</td>
      <td>49.2899</td>
      <td>49.4173</td>
      <td>50.0570</td>
      <td>16.9681</td>
      <td>16.2478</td>
      <td>48.5725</td>
      <td>16.3741</td>
      <td>16.6453</td>
      <td>48.4068</td>
      <td>48.5725</td>
      <td>16.4300</td>
      <td>16.4300</td>
      <td>16.3741</td>
      <td>15.8485</td>
      <td>49.6898</td>
      <td>15.8485</td>
      <td>51.0420</td>
      <td>16.2628</td>
      <td>50.2478</td>
      <td>68</td>
      <td>1</td>
      <td>0.0879</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>428613</th>
      <td>428614</td>
      <td>Serbia</td>
      <td>6880000</td>
      <td>SRB0004</td>
      <td>Non-OECD</td>
      <td>Serbia</td>
      <td>10</td>
      <td>292</td>
      <td>9</td>
      <td>6.0</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>No</td>
      <td>7.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>None</td>
      <td>None</td>
      <td>2.0</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>&lt;ISCED level 3B, 3C&gt;</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>&lt;ISCED level 3B, 3C&gt;</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>9999999</td>
      <td>9999999</td>
      <td>9999999</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>One</td>
      <td>One</td>
      <td>One</td>
      <td>11-25 books</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Not very confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Not very confident</td>
      <td>Confident</td>
      <td>Not very confident</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Likely</td>
      <td>Likely</td>
      <td>Likely</td>
      <td>Very   Likely</td>
      <td>Very   Likely</td>
      <td>Likely</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Courses after school Test Language</td>
      <td>Major in college Science</td>
      <td>Study harder Test Language</td>
      <td>Maximum classes Science</td>
      <td>Pursuing a career Science</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Often</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Most important</td>
      <td>Improve understanding</td>
      <td>learning goals</td>
      <td>Repeat examples</td>
      <td>Less than 2 hours a week</td>
      <td>2 or more but less than 4 hours a week</td>
      <td>2 or more but less than 4 hours a week</td>
      <td>4 or more but less than 6 hours a week</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>NaN</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it once or twice</td>
      <td>Heard of it often</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Heard of it often</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>45.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>36.0</td>
      <td>35.0</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not at all like me</td>
      <td>Not at all like me</td>
      <td>Not at all like me</td>
      <td>Somewhat like me</td>
      <td>Not much like me</td>
      <td>Mostly like me</td>
      <td>Mostly like me</td>
      <td>Somewhat like me</td>
      <td>Mostly like me</td>
      <td>Not much like me</td>
      <td>definitely not do this</td>
      <td>definitely do this</td>
      <td>definitely do this</td>
      <td>definitely do this</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>7-9 years old</td>
      <td>10-12 years old</td>
      <td>1</td>
      <td>3</td>
      <td>3</td>
      <td>Almost every day</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Almost every day</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a month</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Disagree</td>
      <td>Strongly disagree</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No, never</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>&lt;test language&gt; or &lt;other official national language(s) or d</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No, never</td>
      <td>NaN</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>NaN</td>
      <td>No</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>A Simple calculator</td>
      <td>10</td>
      <td>10</td>
      <td>0</td>
      <td>StQ Form A</td>
      <td>booklet 26</td>
      <td>Easier set of booklets</td>
      <td>15.58</td>
      <td>0.0</td>
      <td>Serbia: Economic</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>26.62</td>
      <td>44.14</td>
      <td>NaN</td>
      <td>Serbia</td>
      <td>One of the other former Yugoslav republics (SRB)</td>
      <td>Serbia</td>
      <td>NaN</td>
      <td>-0.0511</td>
      <td>1.27</td>
      <td>NaN</td>
      <td>-0.3632</td>
      <td>-0.20</td>
      <td>-0.4371</td>
      <td>-1.5599</td>
      <td>1.2219</td>
      <td>0.0820</td>
      <td>-0.01</td>
      <td>NaN</td>
      <td>ISCED 5B</td>
      <td>0.87</td>
      <td>-0.4661</td>
      <td>ISCED 5B</td>
      <td>44.14</td>
      <td>-0.32</td>
      <td>-1.4670</td>
      <td>-0.5116</td>
      <td>-1.3202</td>
      <td>0.0279</td>
      <td>-1.3991</td>
      <td>-0.40</td>
      <td>-0.0836</td>
      <td>Native</td>
      <td>-0.0586</td>
      <td>-1.5392</td>
      <td>-1.7872</td>
      <td>0.05</td>
      <td>0.30</td>
      <td>B</td>
      <td>ISCED level 3</td>
      <td>Pre-Vocational</td>
      <td>NaN</td>
      <td>Serbian</td>
      <td>NaN</td>
      <td>135.0</td>
      <td>-0.4567</td>
      <td>-0.63</td>
      <td>-1.5329</td>
      <td>1.4298</td>
      <td>ISCED 3B, C</td>
      <td>135.0</td>
      <td>NaN</td>
      <td>Shop supervisors</td>
      <td>Carpenters and joiners</td>
      <td>-0.1465</td>
      <td>3.0</td>
      <td>14.5</td>
      <td>-0.1475</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>NaN</td>
      <td>90.0</td>
      <td>NaN</td>
      <td>-0.3852</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Serbian</td>
      <td>13.0</td>
      <td>-0.7749</td>
      <td>-0.1388</td>
      <td>-0.76</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>521.1949</td>
      <td>453.4273</td>
      <td>479.9112</td>
      <td>500.9425</td>
      <td>496.2689</td>
      <td>506.3951</td>
      <td>485.3638</td>
      <td>543.0051</td>
      <td>511.8476</td>
      <td>539.8894</td>
      <td>477.5744</td>
      <td>421.4909</td>
      <td>518.0791</td>
      <td>490.8163</td>
      <td>523.5317</td>
      <td>405.1332</td>
      <td>372.4178</td>
      <td>423.0488</td>
      <td>440.9643</td>
      <td>417.5962</td>
      <td>434.7328</td>
      <td>432.3960</td>
      <td>494.7110</td>
      <td>461.2167</td>
      <td>473.6797</td>
      <td>476.7955</td>
      <td>510.2898</td>
      <td>521.9738</td>
      <td>454.2063</td>
      <td>497.0478</td>
      <td>501.7215</td>
      <td>500.1636</td>
      <td>508.7319</td>
      <td>473.6797</td>
      <td>458.8799</td>
      <td>454.9852</td>
      <td>568.7101</td>
      <td>553.9103</td>
      <td>487.7006</td>
      <td>521.9738</td>
      <td>528.3834</td>
      <td>476.2569</td>
      <td>466.6336</td>
      <td>469.0394</td>
      <td>482.6725</td>
      <td>609.6046</td>
      <td>469.7314</td>
      <td>493.0436</td>
      <td>510.7609</td>
      <td>514.4909</td>
      <td>15.2494</td>
      <td>23.1665</td>
      <td>23.1665</td>
      <td>22.7955</td>
      <td>20.9985</td>
      <td>22.6217</td>
      <td>7.6520</td>
      <td>8.6112</td>
      <td>25.4436</td>
      <td>6.9706</td>
      <td>7.5985</td>
      <td>25.1490</td>
      <td>20.9117</td>
      <td>6.9239</td>
      <td>8.2778</td>
      <td>8.4812</td>
      <td>7.7222</td>
      <td>22.6217</td>
      <td>6.9483</td>
      <td>22.6217</td>
      <td>7.5985</td>
      <td>7.5406</td>
      <td>7.5406</td>
      <td>7.6520</td>
      <td>8.2778</td>
      <td>7.7222</td>
      <td>22.7955</td>
      <td>20.7718</td>
      <td>6.9483</td>
      <td>25.1490</td>
      <td>22.9561</td>
      <td>6.9706</td>
      <td>8.3830</td>
      <td>25.8337</td>
      <td>20.9985</td>
      <td>20.8448</td>
      <td>22.6217</td>
      <td>7.7222</td>
      <td>25.4436</td>
      <td>7.7222</td>
      <td>22.9561</td>
      <td>23.1665</td>
      <td>23.1665</td>
      <td>22.7955</td>
      <td>20.9985</td>
      <td>22.6217</td>
      <td>7.6520</td>
      <td>8.6112</td>
      <td>25.4436</td>
      <td>6.9706</td>
      <td>7.5985</td>
      <td>25.1490</td>
      <td>20.9117</td>
      <td>6.9239</td>
      <td>8.2778</td>
      <td>8.4812</td>
      <td>7.7222</td>
      <td>22.6217</td>
      <td>6.9483</td>
      <td>22.6217</td>
      <td>7.5985</td>
      <td>7.5406</td>
      <td>7.5406</td>
      <td>7.6520</td>
      <td>8.2778</td>
      <td>7.7222</td>
      <td>22.7955</td>
      <td>20.7718</td>
      <td>6.9483</td>
      <td>25.1490</td>
      <td>22.9561</td>
      <td>6.9706</td>
      <td>8.3830</td>
      <td>25.8337</td>
      <td>20.9985</td>
      <td>20.8448</td>
      <td>22.6217</td>
      <td>7.7222</td>
      <td>25.4436</td>
      <td>7.7222</td>
      <td>22.9561</td>
      <td>66</td>
      <td>1</td>
      <td>0.2245</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>200657</th>
      <td>200658</td>
      <td>United Kingdom</td>
      <td>8262000</td>
      <td>GBR2005</td>
      <td>OECD</td>
      <td>United Kingdom (Scotland)</td>
      <td>463</td>
      <td>11541</td>
      <td>11</td>
      <td>1.0</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>Yes, for more than one year</td>
      <td>4.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>None</td>
      <td>None</td>
      <td>1.0</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>&lt;ISCED level 3A&gt;</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>&lt;ISCED level 3B, 3C&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>0.0</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>826201</td>
      <td>826201</td>
      <td>826201</td>
      <td>Three or more</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>Two</td>
      <td>Three or more</td>
      <td>11-25 books</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Not very confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Not very confident</td>
      <td>Confident</td>
      <td>Not very confident</td>
      <td>Disagree</td>
      <td>Strongly disagree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Not at all likely</td>
      <td>Slightly likely</td>
      <td>Likely</td>
      <td>Not at all likely</td>
      <td>Slightly likely</td>
      <td>Very   Likely</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Courses after school Math</td>
      <td>Major in college Math</td>
      <td>Study harder Math</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Sometimes</td>
      <td>Often</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Sometimes</td>
      <td>Often</td>
      <td>Sometimes</td>
      <td>Always or almost always</td>
      <td>Often</td>
      <td>Sometimes</td>
      <td>Often</td>
      <td>Sometimes</td>
      <td>Always or almost always</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Not much like me</td>
      <td>Not much like me</td>
      <td>Not much like me</td>
      <td>Mostly like me</td>
      <td>Somewhat like me</td>
      <td>Mostly like me</td>
      <td>Mostly like me</td>
      <td>Mostly like me</td>
      <td>Mostly like me</td>
      <td>Mostly like me</td>
      <td>definitely do this</td>
      <td>probably do this</td>
      <td>definitely not do this</td>
      <td>probably do this</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97</td>
      <td>97</td>
      <td>97</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A Scientific calculator</td>
      <td>9</td>
      <td>10</td>
      <td>1</td>
      <td>StQ Form B</td>
      <td>booklet 5</td>
      <td>Standard set of booklets</td>
      <td>15.50</td>
      <td>0.0</td>
      <td>Scotland: Standard Grades or Access 3 or Intermediates</td>
      <td>-0.47</td>
      <td>-0.64</td>
      <td>-0.9394</td>
      <td>-0.90</td>
      <td>53.60</td>
      <td>24.98</td>
      <td>-0.0784</td>
      <td>United Kingdom (Scotland)</td>
      <td>United Kingdom (Scotland)</td>
      <td>United Kingdom (excl.Scotland)</td>
      <td>0.1015</td>
      <td>NaN</td>
      <td>0.25</td>
      <td>0.81</td>
      <td>NaN</td>
      <td>0.72</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.5300</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>ISCED 3B, C</td>
      <td>1.12</td>
      <td>NaN</td>
      <td>ISCED 5A, 6</td>
      <td>53.60</td>
      <td>0.86</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.24</td>
      <td>NaN</td>
      <td>Native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.39</td>
      <td>0.30</td>
      <td>C</td>
      <td>ISCED level 3</td>
      <td>General</td>
      <td>NaN</td>
      <td>English</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.4486</td>
      <td>-0.63</td>
      <td>1.1091</td>
      <td>0.4684</td>
      <td>ISCED 5A, 6</td>
      <td>NaN</td>
      <td>-0.9508</td>
      <td>Teachers aides</td>
      <td>Physical and engineering science technicians</td>
      <td>0.4639</td>
      <td>NaN</td>
      <td>16.0</td>
      <td>0.0511</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>1.12</td>
      <td>NaN</td>
      <td>-0.02</td>
      <td>-0.0455</td>
      <td>-1.4597</td>
      <td>-0.5809</td>
      <td>-1.0685</td>
      <td>-0.28</td>
      <td>English</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.27</td>
      <td>0.1565</td>
      <td>0.4908</td>
      <td>0.0064</td>
      <td>0.9208</td>
      <td>0.3408</td>
      <td>0.2969</td>
      <td>0.3516</td>
      <td>1.2423</td>
      <td>-0.1687</td>
      <td>1.7169</td>
      <td>1.0099</td>
      <td>0.4646</td>
      <td>627.6757</td>
      <td>655.7174</td>
      <td>623.7810</td>
      <td>599.6339</td>
      <td>601.1918</td>
      <td>583.2762</td>
      <td>575.4868</td>
      <td>612.8758</td>
      <td>618.3284</td>
      <td>655.7174</td>
      <td>628.4546</td>
      <td>657.2753</td>
      <td>690.7696</td>
      <td>665.8436</td>
      <td>674.4119</td>
      <td>573.9290</td>
      <td>594.9603</td>
      <td>610.5390</td>
      <td>598.0760</td>
      <td>623.0020</td>
      <td>629.2335</td>
      <td>580.1605</td>
      <td>626.8967</td>
      <td>605.8654</td>
      <td>645.5912</td>
      <td>617.5495</td>
      <td>571.5921</td>
      <td>643.2544</td>
      <td>623.7810</td>
      <td>606.6443</td>
      <td>658.8332</td>
      <td>576.2658</td>
      <td>698.5590</td>
      <td>675.1908</td>
      <td>697.7800</td>
      <td>580.9394</td>
      <td>538.8768</td>
      <td>672.0751</td>
      <td>641.6965</td>
      <td>617.5495</td>
      <td>600.6613</td>
      <td>614.1645</td>
      <td>588.7466</td>
      <td>590.3352</td>
      <td>578.4206</td>
      <td>579.2055</td>
      <td>567.0832</td>
      <td>551.2309</td>
      <td>568.9482</td>
      <td>560.5558</td>
      <td>19.6072</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>10.4827</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>27.5046</td>
      <td>37</td>
      <td>2</td>
      <td>0.0285</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>323215</th>
      <td>323216</td>
      <td>Mexico</td>
      <td>4840000</td>
      <td>MEX2573</td>
      <td>OECD</td>
      <td>Mexico</td>
      <td>333</td>
      <td>7513</td>
      <td>10</td>
      <td>5.0</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>Yes, for more than one year</td>
      <td>6.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>None</td>
      <td>None</td>
      <td>1.0</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>&lt;ISCED level 3B, 3C&gt;</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Working part-time &lt;for pay&gt;</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>484001</td>
      <td>484001</td>
      <td>484001</td>
      <td>Three or more</td>
      <td>Two</td>
      <td>One</td>
      <td>Two</td>
      <td>Two</td>
      <td>11-25 books</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Confident</td>
      <td>Not very confident</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Very   Likely</td>
      <td>Slightly likely</td>
      <td>Likely</td>
      <td>Slightly likely</td>
      <td>Slightly likely</td>
      <td>Slightly likely</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Courses after school Math</td>
      <td>Major in college Science</td>
      <td>Study harder Test Language</td>
      <td>Maximum classes Science</td>
      <td>Pursuing a career Science</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Sometimes</td>
      <td>Never or rarely</td>
      <td>Never or rarely</td>
      <td>Most important</td>
      <td>new ways</td>
      <td>Relating to other subjects</td>
      <td>everyday life</td>
      <td>2 or more but less than 4 hours a week</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>Less than 2 hours a week</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Sometimes</td>
      <td>Rarely</td>
      <td>Never heard of it</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it often</td>
      <td>Know it well,  understand the concept</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it often</td>
      <td>Know it well,  understand the concept</td>
      <td>50.0</td>
      <td>50.0</td>
      <td>50.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>40.0</td>
      <td>15.0</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Very much like me</td>
      <td>Very much like me</td>
      <td>Very much like me</td>
      <td>Mostly like me</td>
      <td>Very much like me</td>
      <td>Mostly like me</td>
      <td>Somewhat like me</td>
      <td>Somewhat like me</td>
      <td>Not much like me</td>
      <td>Not at all like me</td>
      <td>probably do this</td>
      <td>probably do this</td>
      <td>definitely do this</td>
      <td>definitely do this</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Yes, and I use it</td>
      <td>Yes, but I dont use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, but I dont use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>7-9 years old</td>
      <td>7-9 years old</td>
      <td>3</td>
      <td>2</td>
      <td>5</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Almost every day</td>
      <td>Every day</td>
      <td>Every day</td>
      <td>Every day</td>
      <td>Every day</td>
      <td>Every day</td>
      <td>Every day</td>
      <td>Every day</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>Yes, but only the teacher demonstrated this</td>
      <td>Strongly agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A Scientific calculator</td>
      <td>10</td>
      <td>10</td>
      <td>0</td>
      <td>StQ Form A</td>
      <td>booklet 27</td>
      <td>Easier set of booklets</td>
      <td>15.67</td>
      <td>0.0</td>
      <td>Mexico: General Baccalaureate or Upper Secondary</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44.94</td>
      <td>NaN</td>
      <td>Missing</td>
      <td>Mexico</td>
      <td>Missing</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.27</td>
      <td>NaN</td>
      <td>0.0883</td>
      <td>0.36</td>
      <td>-0.2531</td>
      <td>-1.5748</td>
      <td>-0.0760</td>
      <td>1.4899</td>
      <td>-1.13</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.12</td>
      <td>NaN</td>
      <td>ISCED 5A, 6</td>
      <td>44.94</td>
      <td>0.39</td>
      <td>3.7332</td>
      <td>NaN</td>
      <td>1.0091</td>
      <td>0.5519</td>
      <td>0.4160</td>
      <td>-0.40</td>
      <td>1.5045</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.80</td>
      <td>0.91</td>
      <td>A</td>
      <td>ISCED level 3</td>
      <td>General</td>
      <td>NaN</td>
      <td>Spanish</td>
      <td>NaN</td>
      <td>200.0</td>
      <td>0.2171</td>
      <td>-0.33</td>
      <td>-0.7332</td>
      <td>-0.4017</td>
      <td>ISCED 5A, 6</td>
      <td>200.0</td>
      <td>NaN</td>
      <td>Secretaries (general)</td>
      <td>Missing</td>
      <td>-0.9492</td>
      <td>5.0</td>
      <td>16.0</td>
      <td>-0.1475</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>NaN</td>
      <td>250.0</td>
      <td>NaN</td>
      <td>1.4014</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Spanish</td>
      <td>34.0</td>
      <td>0.4067</td>
      <td>-1.6104</td>
      <td>0.15</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>380.4409</td>
      <td>341.4940</td>
      <td>360.1885</td>
      <td>449.7663</td>
      <td>396.7986</td>
      <td>345.3887</td>
      <td>442.7559</td>
      <td>337.5993</td>
      <td>397.5775</td>
      <td>329.0310</td>
      <td>392.9039</td>
      <td>464.5661</td>
      <td>374.2094</td>
      <td>410.8194</td>
      <td>374.9883</td>
      <td>403.8090</td>
      <td>452.8821</td>
      <td>367.1989</td>
      <td>378.1041</td>
      <td>397.5775</td>
      <td>339.1572</td>
      <td>383.5566</td>
      <td>350.0623</td>
      <td>383.5566</td>
      <td>342.2729</td>
      <td>361.7464</td>
      <td>363.3043</td>
      <td>396.7986</td>
      <td>367.9779</td>
      <td>375.7673</td>
      <td>381.9988</td>
      <td>367.9779</td>
      <td>397.5775</td>
      <td>364.8621</td>
      <td>371.0936</td>
      <td>354.7359</td>
      <td>360.1885</td>
      <td>410.8194</td>
      <td>339.9361</td>
      <td>322.7995</td>
      <td>475.1603</td>
      <td>412.4098</td>
      <td>419.5585</td>
      <td>525.2018</td>
      <td>432.2675</td>
      <td>369.3025</td>
      <td>341.3279</td>
      <td>403.8046</td>
      <td>449.4965</td>
      <td>400.0746</td>
      <td>45.3566</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>22.6783</td>
      <td>68.0349</td>
      <td>68.0349</td>
      <td>22.6783</td>
      <td>10</td>
      <td>2</td>
      <td>0.0342</td>
      <td>22NOV13</td>
    </tr>
    <tr>
      <th>341559</th>
      <td>341560</td>
      <td>Mexico</td>
      <td>4840000</td>
      <td>MEX0204</td>
      <td>OECD</td>
      <td>Mexico</td>
      <td>1112</td>
      <td>25857</td>
      <td>10</td>
      <td>5.0</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>Yes, for more than one year</td>
      <td>6.0</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>No, never</td>
      <td>One or two times</td>
      <td>None</td>
      <td>1.0</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>She did not complete &lt;ISCED level 1&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>&lt;ISCED level 2&gt;</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Working full-time &lt;for pay&gt;</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>484001</td>
      <td>484002</td>
      <td>484001</td>
      <td>One</td>
      <td>One</td>
      <td>One</td>
      <td>None</td>
      <td>One</td>
      <td>0-10 books</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>Strongly disagree</td>
      <td>Strongly agree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Most important</td>
      <td>Improve understanding</td>
      <td>learning goals</td>
      <td>more information</td>
      <td>Less than 2 hours a week</td>
      <td>2 or more but less than 4 hours a week</td>
      <td>Less than 2 hours a week</td>
      <td>I do not attend &lt;out-of-school time lessons&gt; in this subject</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Rarely</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Heard of it once or twice</td>
      <td>Know it well,  understand the concept</td>
      <td>Heard of it once or twice</td>
      <td>Heard of it often</td>
      <td>Heard of it often</td>
      <td>Heard of it once or twice</td>
      <td>Heard of it a few times</td>
      <td>Heard of it often</td>
      <td>Heard of it often</td>
      <td>Heard of it once or twice</td>
      <td>Heard of it often</td>
      <td>Heard of it a few times</td>
      <td>Heard of it often</td>
      <td>Heard of it often</td>
      <td>Heard of it often</td>
      <td>Heard of it often</td>
      <td>50.0</td>
      <td>50.0</td>
      <td>50.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>30.0</td>
      <td>41.0</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Frequently</td>
      <td>Sometimes</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Most Lessons</td>
      <td>Every Lesson</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Every Lesson</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Most Lessons</td>
      <td>Some Lessons</td>
      <td>Some Lessons</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Sometimes</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Never or Hardly Ever</td>
      <td>Some Lessons</td>
      <td>Never or Hardly Ever</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, but I dont use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>No</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>Yes, and I use it</td>
      <td>No</td>
      <td>7-9 years old</td>
      <td>7-9 years old</td>
      <td>2</td>
      <td>4</td>
      <td>4</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Once or twice a week</td>
      <td>Once or twice a week</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Almost every day</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Never or hardly ever</td>
      <td>Once or twice a week</td>
      <td>Never or hardly ever</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Strongly agree</td>
      <td>Agree</td>
      <td>Strongly agree</td>
      <td>Disagree</td>
      <td>Agree</td>
      <td>Disagree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A Scientific calculator</td>
      <td>9</td>
      <td>10</td>
      <td>1</td>
      <td>StQ Form C</td>
      <td>booklet 22</td>
      <td>Easier set of booklets</td>
      <td>16.00</td>
      <td>0.0</td>
      <td>Mexico: General Baccalaureate or Upper Secondary</td>
      <td>1.26</td>
      <td>-0.24</td>
      <td>-0.9394</td>
      <td>-0.15</td>
      <td>30.34</td>
      <td>21.24</td>
      <td>-0.0784</td>
      <td>Mexico</td>
      <td>Mexico</td>
      <td>Mexico</td>
      <td>-0.9083</td>
      <td>NaN</td>
      <td>-0.48</td>
      <td>1.19</td>
      <td>-0.4549</td>
      <td>-1.78</td>
      <td>-0.2531</td>
      <td>0.7955</td>
      <td>NaN</td>
      <td>0.1427</td>
      <td>-0.72</td>
      <td>1.0</td>
      <td>ISCED 2</td>
      <td>-0.69</td>
      <td>NaN</td>
      <td>ISCED 2</td>
      <td>30.34</td>
      <td>-2.03</td>
      <td>0.1820</td>
      <td>NaN</td>
      <td>0.3419</td>
      <td>0.5519</td>
      <td>-1.5824</td>
      <td>-1.13</td>
      <td>0.5423</td>
      <td>Native</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>ISCED level 3</td>
      <td>General</td>
      <td>NaN</td>
      <td>Spanish</td>
      <td>NaN</td>
      <td>200.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>250.0</td>
      <td>-0.2395</td>
      <td>Sewing, embroidery and related workers</td>
      <td>Car, taxi and van drivers</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>9.0</td>
      <td>NaN</td>
      <td>Did not repeat a &lt;grade&gt;</td>
      <td>-1.28</td>
      <td>250.0</td>
      <td>-0.02</td>
      <td>NaN</td>
      <td>-0.5945</td>
      <td>-0.1057</td>
      <td>-0.0798</td>
      <td>0.34</td>
      <td>Spanish</td>
      <td>28.0</td>
      <td>-0.7749</td>
      <td>0.5749</td>
      <td>-2.31</td>
      <td>0.9305</td>
      <td>0.4908</td>
      <td>0.9963</td>
      <td>0.9208</td>
      <td>-0.5365</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.8270</td>
      <td>-1.1235</td>
      <td>1.0099</td>
      <td>NaN</td>
      <td>335.9635</td>
      <td>373.3525</td>
      <td>376.4683</td>
      <td>388.1524</td>
      <td>367.9000</td>
      <td>379.5840</td>
      <td>335.9635</td>
      <td>382.6998</td>
      <td>349.9844</td>
      <td>382.6998</td>
      <td>376.4683</td>
      <td>345.3108</td>
      <td>360.1106</td>
      <td>378.8051</td>
      <td>381.9209</td>
      <td>379.5840</td>
      <td>342.9740</td>
      <td>374.9104</td>
      <td>340.6372</td>
      <td>382.6998</td>
      <td>417.7520</td>
      <td>389.7102</td>
      <td>454.3621</td>
      <td>421.6467</td>
      <td>414.6362</td>
      <td>336.7425</td>
      <td>388.1524</td>
      <td>371.7947</td>
      <td>373.3525</td>
      <td>394.3839</td>
      <td>328.9531</td>
      <td>364.7842</td>
      <td>371.0157</td>
      <td>361.6685</td>
      <td>352.3212</td>
      <td>355.4370</td>
      <td>406.8469</td>
      <td>381.9209</td>
      <td>381.9209</td>
      <td>412.2994</td>
      <td>421.2266</td>
      <td>417.2550</td>
      <td>462.5307</td>
      <td>462.5307</td>
      <td>447.4388</td>
      <td>402.8721</td>
      <td>394.4797</td>
      <td>422.4543</td>
      <td>433.6442</td>
      <td>424.3193</td>
      <td>25.1813</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>37.7720</td>
      <td>37.7720</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>12.5907</td>
      <td>54</td>
      <td>2</td>
      <td>0.0190</td>
      <td>22NOV13</td>
    </tr>
  </tbody>
</table>
</div>




```python
pisa_dict
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
      <th>ColName</th>
      <th>Definition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>x</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CNT</td>
      <td>Country code 3-character</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SUBNATIO</td>
      <td>Adjudicated sub-region code 7-digit code (3-digit country code + region ID + stratum ID)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>STRATUM</td>
      <td>Stratum ID 7-character (cnt + region ID + original stratum ID)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>OECD</td>
      <td>OECD country</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NC</td>
      <td>National Centre 6-digit Code</td>
    </tr>
    <tr>
      <th>6</th>
      <td>SCHOOLID</td>
      <td>School ID 7-digit (region ID + stratum ID + 3-digit school ID)</td>
    </tr>
    <tr>
      <th>7</th>
      <td>STIDSTD</td>
      <td>Student ID</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ST01Q01</td>
      <td>International Grade</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ST02Q01</td>
      <td>National Study Programme</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ST03Q01</td>
      <td>Birth - Month</td>
    </tr>
    <tr>
      <th>11</th>
      <td>ST03Q02</td>
      <td>Birth -Year</td>
    </tr>
    <tr>
      <th>12</th>
      <td>ST04Q01</td>
      <td>Gender</td>
    </tr>
    <tr>
      <th>13</th>
      <td>ST05Q01</td>
      <td>Attend &lt;ISCED 0&gt;</td>
    </tr>
    <tr>
      <th>14</th>
      <td>ST06Q01</td>
      <td>Age at &lt;ISCED 1&gt;</td>
    </tr>
    <tr>
      <th>15</th>
      <td>ST07Q01</td>
      <td>Repeat - &lt;ISCED 1&gt;</td>
    </tr>
    <tr>
      <th>16</th>
      <td>ST07Q02</td>
      <td>Repeat - &lt;ISCED 2&gt;</td>
    </tr>
    <tr>
      <th>17</th>
      <td>ST07Q03</td>
      <td>Repeat - &lt;ISCED 3&gt;</td>
    </tr>
    <tr>
      <th>18</th>
      <td>ST08Q01</td>
      <td>Truancy - Late for School</td>
    </tr>
    <tr>
      <th>19</th>
      <td>ST09Q01</td>
      <td>Truancy - Skip whole school day</td>
    </tr>
    <tr>
      <th>20</th>
      <td>ST115Q01</td>
      <td>Truancy - Skip classes within school day</td>
    </tr>
    <tr>
      <th>21</th>
      <td>ST11Q01</td>
      <td>At Home - Mother</td>
    </tr>
    <tr>
      <th>22</th>
      <td>ST11Q02</td>
      <td>At Home - Father</td>
    </tr>
    <tr>
      <th>23</th>
      <td>ST11Q03</td>
      <td>At Home - Brothers</td>
    </tr>
    <tr>
      <th>24</th>
      <td>ST11Q04</td>
      <td>At Home - Sisters</td>
    </tr>
    <tr>
      <th>25</th>
      <td>ST11Q05</td>
      <td>At Home - Grandparents</td>
    </tr>
    <tr>
      <th>26</th>
      <td>ST11Q06</td>
      <td>At Home - Others</td>
    </tr>
    <tr>
      <th>27</th>
      <td>ST13Q01</td>
      <td>Mother&lt;Highest Schooling&gt;</td>
    </tr>
    <tr>
      <th>28</th>
      <td>ST14Q01</td>
      <td>Mother Qualifications - &lt;ISCED level 6&gt;</td>
    </tr>
    <tr>
      <th>29</th>
      <td>ST14Q02</td>
      <td>Mother Qualifications - &lt;ISCED level 5A&gt;</td>
    </tr>
    <tr>
      <th>30</th>
      <td>ST14Q03</td>
      <td>Mother Qualifications - &lt;ISCED level 5B&gt;</td>
    </tr>
    <tr>
      <th>31</th>
      <td>ST14Q04</td>
      <td>Mother Qualifications - &lt;ISCED level 4&gt;</td>
    </tr>
    <tr>
      <th>32</th>
      <td>ST15Q01</td>
      <td>Mother Current Job Status</td>
    </tr>
    <tr>
      <th>33</th>
      <td>ST17Q01</td>
      <td>Father&lt;Highest Schooling&gt;</td>
    </tr>
    <tr>
      <th>34</th>
      <td>ST18Q01</td>
      <td>Father Qualifications - &lt;ISCED level 6&gt;</td>
    </tr>
    <tr>
      <th>35</th>
      <td>ST18Q02</td>
      <td>Father Qualifications - &lt;ISCED level 5A&gt;</td>
    </tr>
    <tr>
      <th>36</th>
      <td>ST18Q03</td>
      <td>Father Qualifications - &lt;ISCED level 5B&gt;</td>
    </tr>
    <tr>
      <th>37</th>
      <td>ST18Q04</td>
      <td>Father Qualifications - &lt;ISCED level 4&gt;</td>
    </tr>
    <tr>
      <th>38</th>
      <td>ST19Q01</td>
      <td>Father Current Job Status</td>
    </tr>
    <tr>
      <th>39</th>
      <td>ST20Q01</td>
      <td>Country of Birth International - Self</td>
    </tr>
    <tr>
      <th>40</th>
      <td>ST20Q02</td>
      <td>Country of Birth International - Mother</td>
    </tr>
    <tr>
      <th>41</th>
      <td>ST20Q03</td>
      <td>Country of Birth International - Father</td>
    </tr>
    <tr>
      <th>42</th>
      <td>ST21Q01</td>
      <td>Age of arrival in &lt;country of test&gt;</td>
    </tr>
    <tr>
      <th>43</th>
      <td>ST25Q01</td>
      <td>International Language at Home</td>
    </tr>
    <tr>
      <th>44</th>
      <td>ST26Q01</td>
      <td>Possessions - desk</td>
    </tr>
    <tr>
      <th>45</th>
      <td>ST26Q02</td>
      <td>Possessions - own room</td>
    </tr>
    <tr>
      <th>46</th>
      <td>ST26Q03</td>
      <td>Possessions - study place</td>
    </tr>
    <tr>
      <th>47</th>
      <td>ST26Q04</td>
      <td>Possessions - computer</td>
    </tr>
    <tr>
      <th>48</th>
      <td>ST26Q05</td>
      <td>Possessions - software</td>
    </tr>
    <tr>
      <th>49</th>
      <td>ST26Q06</td>
      <td>Possessions - Internet</td>
    </tr>
    <tr>
      <th>50</th>
      <td>ST26Q07</td>
      <td>Possessions - literature</td>
    </tr>
    <tr>
      <th>51</th>
      <td>ST26Q08</td>
      <td>Possessions - poetry</td>
    </tr>
    <tr>
      <th>52</th>
      <td>ST26Q09</td>
      <td>Possessions - art</td>
    </tr>
    <tr>
      <th>53</th>
      <td>ST26Q10</td>
      <td>Possessions - textbooks</td>
    </tr>
    <tr>
      <th>54</th>
      <td>ST26Q11</td>
      <td>Possessions - &lt;technical reference books&gt;</td>
    </tr>
    <tr>
      <th>55</th>
      <td>ST26Q12</td>
      <td>Possessions - dictionary</td>
    </tr>
    <tr>
      <th>56</th>
      <td>ST26Q13</td>
      <td>Possessions - dishwasher</td>
    </tr>
    <tr>
      <th>57</th>
      <td>ST26Q14</td>
      <td>Possessions - &lt;DVD&gt;</td>
    </tr>
    <tr>
      <th>58</th>
      <td>ST26Q15</td>
      <td>Possessions - &lt;Country item 1&gt;</td>
    </tr>
    <tr>
      <th>59</th>
      <td>ST26Q16</td>
      <td>Possessions - &lt;Country item 2&gt;</td>
    </tr>
    <tr>
      <th>60</th>
      <td>ST26Q17</td>
      <td>Possessions - &lt;Country item 3&gt;</td>
    </tr>
    <tr>
      <th>61</th>
      <td>ST27Q01</td>
      <td>How many - cellular phones</td>
    </tr>
    <tr>
      <th>62</th>
      <td>ST27Q02</td>
      <td>How many - televisions</td>
    </tr>
    <tr>
      <th>63</th>
      <td>ST27Q03</td>
      <td>How many - computers</td>
    </tr>
    <tr>
      <th>64</th>
      <td>ST27Q04</td>
      <td>How many - cars</td>
    </tr>
    <tr>
      <th>65</th>
      <td>ST27Q05</td>
      <td>How many - rooms bath or shower</td>
    </tr>
    <tr>
      <th>66</th>
      <td>ST28Q01</td>
      <td>How many books at home</td>
    </tr>
    <tr>
      <th>67</th>
      <td>ST29Q01</td>
      <td>Math Interest - Enjoy Reading</td>
    </tr>
    <tr>
      <th>68</th>
      <td>ST29Q02</td>
      <td>Instrumental Motivation - Worthwhile for Work</td>
    </tr>
    <tr>
      <th>69</th>
      <td>ST29Q03</td>
      <td>Math Interest - Look Forward to Lessons</td>
    </tr>
    <tr>
      <th>70</th>
      <td>ST29Q04</td>
      <td>Math Interest - Enjoy Maths</td>
    </tr>
    <tr>
      <th>71</th>
      <td>ST29Q05</td>
      <td>Instrumental Motivation - Worthwhile for Career Chances</td>
    </tr>
    <tr>
      <th>72</th>
      <td>ST29Q06</td>
      <td>Math Interest - Interested</td>
    </tr>
    <tr>
      <th>73</th>
      <td>ST29Q07</td>
      <td>Instrumental Motivation - Important for Future Study</td>
    </tr>
    <tr>
      <th>74</th>
      <td>ST29Q08</td>
      <td>Instrumental Motivation - Helps to Get a Job</td>
    </tr>
    <tr>
      <th>75</th>
      <td>ST35Q01</td>
      <td>Subjective Norms -Friends Do Well in Mathematics</td>
    </tr>
    <tr>
      <th>76</th>
      <td>ST35Q02</td>
      <td>Subjective Norms -Friends Work Hard on Mathematics</td>
    </tr>
    <tr>
      <th>77</th>
      <td>ST35Q03</td>
      <td>Subjective Norms - Friends Enjoy Mathematics Tests</td>
    </tr>
    <tr>
      <th>78</th>
      <td>ST35Q04</td>
      <td>Subjective Norms - Parents Believe Studying Mathematics Is Important</td>
    </tr>
    <tr>
      <th>79</th>
      <td>ST35Q05</td>
      <td>Subjective Norms - Parents Believe Mathematics Is Important for Career</td>
    </tr>
    <tr>
      <th>80</th>
      <td>ST35Q06</td>
      <td>Subjective Norms - Parents Like Mathematics</td>
    </tr>
    <tr>
      <th>81</th>
      <td>ST37Q01</td>
      <td>Math Self-Efficacy - Using a &lt;Train Timetable&gt;</td>
    </tr>
    <tr>
      <th>82</th>
      <td>ST37Q02</td>
      <td>Math Self-Efficacy - Calculating TV Discount</td>
    </tr>
    <tr>
      <th>83</th>
      <td>ST37Q03</td>
      <td>Math Self-Efficacy - Calculating Square Metres of Tiles</td>
    </tr>
    <tr>
      <th>84</th>
      <td>ST37Q04</td>
      <td>Math Self-Efficacy - Understanding Graphs in Newspapers</td>
    </tr>
    <tr>
      <th>85</th>
      <td>ST37Q05</td>
      <td>Math Self-Efficacy - Solving Equation 1</td>
    </tr>
    <tr>
      <th>86</th>
      <td>ST37Q06</td>
      <td>Math Self-Efficacy - Distance to Scale</td>
    </tr>
    <tr>
      <th>87</th>
      <td>ST37Q07</td>
      <td>Math Self-Efficacy - Solving Equation 2</td>
    </tr>
    <tr>
      <th>88</th>
      <td>ST37Q08</td>
      <td>Math Self-Efficacy - Calculate Petrol Consumption Rate</td>
    </tr>
    <tr>
      <th>89</th>
      <td>ST42Q01</td>
      <td>Math Anxiety - Worry That It Will Be Difficult</td>
    </tr>
    <tr>
      <th>90</th>
      <td>ST42Q02</td>
      <td>Math Self-Concept - Not Good at Maths</td>
    </tr>
    <tr>
      <th>91</th>
      <td>ST42Q03</td>
      <td>Math Anxiety - Get Very Tense</td>
    </tr>
    <tr>
      <th>92</th>
      <td>ST42Q04</td>
      <td>Math Self-Concept- Get Good &lt;Grades&gt;</td>
    </tr>
    <tr>
      <th>93</th>
      <td>ST42Q05</td>
      <td>Math Anxiety - Get Very Nervous</td>
    </tr>
    <tr>
      <th>94</th>
      <td>ST42Q06</td>
      <td>Math Self-Concept - Learn Quickly</td>
    </tr>
    <tr>
      <th>95</th>
      <td>ST42Q07</td>
      <td>Math Self-Concept - One of Best Subjects</td>
    </tr>
    <tr>
      <th>96</th>
      <td>ST42Q08</td>
      <td>Math Anxiety - Feel Helpless</td>
    </tr>
    <tr>
      <th>97</th>
      <td>ST42Q09</td>
      <td>Math Self-Concept - Understand Difficult Work</td>
    </tr>
    <tr>
      <th>98</th>
      <td>ST42Q10</td>
      <td>Math Anxiety - Worry About Getting Poor &lt;Grades&gt;</td>
    </tr>
    <tr>
      <th>99</th>
      <td>ST43Q01</td>
      <td>Perceived Control - Can Succeed with Enough Effort</td>
    </tr>
    <tr>
      <th>100</th>
      <td>ST43Q02</td>
      <td>Perceived Control - Doing Well is Completely Up to Me</td>
    </tr>
    <tr>
      <th>101</th>
      <td>ST43Q03</td>
      <td>Perceived Control - Family Demands and Problems</td>
    </tr>
    <tr>
      <th>102</th>
      <td>ST43Q04</td>
      <td>Perceived Control - Different Teachers</td>
    </tr>
    <tr>
      <th>103</th>
      <td>ST43Q05</td>
      <td>Perceived Control - If I Wanted I Could Perform Well</td>
    </tr>
    <tr>
      <th>104</th>
      <td>ST43Q06</td>
      <td>Perceived Control - Perform Poorly Regardless</td>
    </tr>
    <tr>
      <th>105</th>
      <td>ST44Q01</td>
      <td>Attributions to Failure - Not Good at Maths Problems</td>
    </tr>
    <tr>
      <th>106</th>
      <td>ST44Q03</td>
      <td>Attributions to Failure - Teacher Did Not Explain Well</td>
    </tr>
    <tr>
      <th>107</th>
      <td>ST44Q04</td>
      <td>Attributions to Failure - Bad Guesses</td>
    </tr>
    <tr>
      <th>108</th>
      <td>ST44Q05</td>
      <td>Attributions to Failure - Material Too Hard</td>
    </tr>
    <tr>
      <th>109</th>
      <td>ST44Q07</td>
      <td>Attributions to Failure - Teacher Didnt Get Students Interested</td>
    </tr>
    <tr>
      <th>110</th>
      <td>ST44Q08</td>
      <td>Attributions to Failure - Unlucky</td>
    </tr>
    <tr>
      <th>111</th>
      <td>ST46Q01</td>
      <td>Math Work Ethic - Homework Completed in Time</td>
    </tr>
    <tr>
      <th>112</th>
      <td>ST46Q02</td>
      <td>Math Work Ethic - Work Hard on Homework</td>
    </tr>
    <tr>
      <th>113</th>
      <td>ST46Q03</td>
      <td>Math Work Ethic - Prepared for Exams</td>
    </tr>
    <tr>
      <th>114</th>
      <td>ST46Q04</td>
      <td>Math Work Ethic - Study Hard for Quizzes</td>
    </tr>
    <tr>
      <th>115</th>
      <td>ST46Q05</td>
      <td>Math Work Ethic - Study Until I Understand Everything</td>
    </tr>
    <tr>
      <th>116</th>
      <td>ST46Q06</td>
      <td>Math Work Ethic - Pay Attention in Classes</td>
    </tr>
    <tr>
      <th>117</th>
      <td>ST46Q07</td>
      <td>Math Work Ethic - Listen in Classes</td>
    </tr>
    <tr>
      <th>118</th>
      <td>ST46Q08</td>
      <td>Math Work Ethic - Avoid Distractions When Studying</td>
    </tr>
    <tr>
      <th>119</th>
      <td>ST46Q09</td>
      <td>Math Work Ethic - Keep Work Organized</td>
    </tr>
    <tr>
      <th>120</th>
      <td>ST48Q01</td>
      <td>Math Intentions - Mathematics vs. Language Courses After School</td>
    </tr>
    <tr>
      <th>121</th>
      <td>ST48Q02</td>
      <td>Math Intentions - Mathematics vs. Science Related Major in College</td>
    </tr>
    <tr>
      <th>122</th>
      <td>ST48Q03</td>
      <td>Math Intentions - Study Harder in Mathematics vs. Language Classes</td>
    </tr>
    <tr>
      <th>123</th>
      <td>ST48Q04</td>
      <td>Math Intentions - Take Maximum Number of Mathematics vs. Science Classes</td>
    </tr>
    <tr>
      <th>124</th>
      <td>ST48Q05</td>
      <td>Math Intentions - Pursuing a Career That Involves Mathematics vs. Science</td>
    </tr>
    <tr>
      <th>125</th>
      <td>ST49Q01</td>
      <td>Math Behaviour - Talk about Maths with Friends</td>
    </tr>
    <tr>
      <th>126</th>
      <td>ST49Q02</td>
      <td>Math Behaviour - Help Friends with Maths</td>
    </tr>
    <tr>
      <th>127</th>
      <td>ST49Q03</td>
      <td>Math Behaviour - &lt;Extracurricular&gt; Activity</td>
    </tr>
    <tr>
      <th>128</th>
      <td>ST49Q04</td>
      <td>Math Behaviour - Participate in Competitions</td>
    </tr>
    <tr>
      <th>129</th>
      <td>ST49Q05</td>
      <td>Math Behaviour - Study More Than 2 Extra Hours a Day</td>
    </tr>
    <tr>
      <th>130</th>
      <td>ST49Q06</td>
      <td>Math Behaviour - Play Chess</td>
    </tr>
    <tr>
      <th>131</th>
      <td>ST49Q07</td>
      <td>Math Behaviour - Computer programming</td>
    </tr>
    <tr>
      <th>132</th>
      <td>ST49Q09</td>
      <td>Math Behaviour - Participate in Math Club</td>
    </tr>
    <tr>
      <th>133</th>
      <td>ST53Q01</td>
      <td>Learning Strategies- Important Parts vs. Existing Knowledge vs. Learn by Heart</td>
    </tr>
    <tr>
      <th>134</th>
      <td>ST53Q02</td>
      <td>Learning Strategies- Improve Understanding vs. New Ways vs. Memory</td>
    </tr>
    <tr>
      <th>135</th>
      <td>ST53Q03</td>
      <td>Learning Strategies - Other Subjects vs. Learning Goals vs. Rehearse Problems</td>
    </tr>
    <tr>
      <th>136</th>
      <td>ST53Q04</td>
      <td>Learning Strategies - Repeat Examples vs. Everyday Applications vs. More Information</td>
    </tr>
    <tr>
      <th>137</th>
      <td>ST55Q01</td>
      <td>Out of school lessons - &lt;test lang&gt;</td>
    </tr>
    <tr>
      <th>138</th>
      <td>ST55Q02</td>
      <td>Out of school lessons - &lt;maths&gt;</td>
    </tr>
    <tr>
      <th>139</th>
      <td>ST55Q03</td>
      <td>Out of school lessons - &lt;science&gt;</td>
    </tr>
    <tr>
      <th>140</th>
      <td>ST55Q04</td>
      <td>Out of school lessons - other</td>
    </tr>
    <tr>
      <th>141</th>
      <td>ST57Q01</td>
      <td>Out-of-School Study Time - Homework</td>
    </tr>
    <tr>
      <th>142</th>
      <td>ST57Q02</td>
      <td>Out-of-School Study Time - Guided Homework</td>
    </tr>
    <tr>
      <th>143</th>
      <td>ST57Q03</td>
      <td>Out-of-School Study Time - Personal Tutor</td>
    </tr>
    <tr>
      <th>144</th>
      <td>ST57Q04</td>
      <td>Out-of-School Study Time - Commercial Company</td>
    </tr>
    <tr>
      <th>145</th>
      <td>ST57Q05</td>
      <td>Out-of-School Study Time - With Parent</td>
    </tr>
    <tr>
      <th>146</th>
      <td>ST57Q06</td>
      <td>Out-of-School Study Time - Computer</td>
    </tr>
    <tr>
      <th>147</th>
      <td>ST61Q01</td>
      <td>Experience with Applied Maths Tasks - Use &lt;Train Timetable&gt;</td>
    </tr>
    <tr>
      <th>148</th>
      <td>ST61Q02</td>
      <td>Experience with Applied Maths Tasks - Calculate Price including Tax</td>
    </tr>
    <tr>
      <th>149</th>
      <td>ST61Q03</td>
      <td>Experience with Applied Maths Tasks - Calculate Square Metres</td>
    </tr>
    <tr>
      <th>150</th>
      <td>ST61Q04</td>
      <td>Experience with Applied Maths Tasks - Understand Scientific Tables</td>
    </tr>
    <tr>
      <th>151</th>
      <td>ST61Q05</td>
      <td>Experience with Pure Maths Tasks - Solve Equation 1</td>
    </tr>
    <tr>
      <th>152</th>
      <td>ST61Q06</td>
      <td>Experience with Applied Maths Tasks - Use a Map to Calculate Distance</td>
    </tr>
    <tr>
      <th>153</th>
      <td>ST61Q07</td>
      <td>Experience with Pure Maths Tasks - Solve Equation 2</td>
    </tr>
    <tr>
      <th>154</th>
      <td>ST61Q08</td>
      <td>Experience with Applied Maths Tasks - Calculate Power Consumption Rate</td>
    </tr>
    <tr>
      <th>155</th>
      <td>ST61Q09</td>
      <td>Experience with Applied Maths Tasks - Solve Equation 3</td>
    </tr>
    <tr>
      <th>156</th>
      <td>ST62Q01</td>
      <td>Familiarity with Math Concepts - Exponential Function</td>
    </tr>
    <tr>
      <th>157</th>
      <td>ST62Q02</td>
      <td>Familiarity with Math Concepts - Divisor</td>
    </tr>
    <tr>
      <th>158</th>
      <td>ST62Q03</td>
      <td>Familiarity with Math Concepts - Quadratic Function</td>
    </tr>
    <tr>
      <th>159</th>
      <td>ST62Q04</td>
      <td>Overclaiming - Proper Number</td>
    </tr>
    <tr>
      <th>160</th>
      <td>ST62Q06</td>
      <td>Familiarity with Math Concepts - Linear Equation</td>
    </tr>
    <tr>
      <th>161</th>
      <td>ST62Q07</td>
      <td>Familiarity with Math Concepts - Vectors</td>
    </tr>
    <tr>
      <th>162</th>
      <td>ST62Q08</td>
      <td>Familiarity with Math Concepts - Complex Number</td>
    </tr>
    <tr>
      <th>163</th>
      <td>ST62Q09</td>
      <td>Familiarity with Math Concepts - Rational Number</td>
    </tr>
    <tr>
      <th>164</th>
      <td>ST62Q10</td>
      <td>Familiarity with Math Concepts - Radicals</td>
    </tr>
    <tr>
      <th>165</th>
      <td>ST62Q11</td>
      <td>Overclaiming - Subjunctive Scaling</td>
    </tr>
    <tr>
      <th>166</th>
      <td>ST62Q12</td>
      <td>Familiarity with Math Concepts - Polygon</td>
    </tr>
    <tr>
      <th>167</th>
      <td>ST62Q13</td>
      <td>Overclaiming - Declarative Fraction</td>
    </tr>
    <tr>
      <th>168</th>
      <td>ST62Q15</td>
      <td>Familiarity with Math Concepts - Congruent Figure</td>
    </tr>
    <tr>
      <th>169</th>
      <td>ST62Q16</td>
      <td>Familiarity with Math Concepts - Cosine</td>
    </tr>
    <tr>
      <th>170</th>
      <td>ST62Q17</td>
      <td>Familiarity with Math Concepts - Arithmetic Mean</td>
    </tr>
    <tr>
      <th>171</th>
      <td>ST62Q19</td>
      <td>Familiarity with Math Concepts - Probability</td>
    </tr>
    <tr>
      <th>172</th>
      <td>ST69Q01</td>
      <td>Min in &lt;class period&gt; - &lt;test lang&gt;</td>
    </tr>
    <tr>
      <th>173</th>
      <td>ST69Q02</td>
      <td>Min in &lt;class period&gt; - &lt;Maths&gt;</td>
    </tr>
    <tr>
      <th>174</th>
      <td>ST69Q03</td>
      <td>Min in &lt;class period&gt; - &lt;Science&gt;</td>
    </tr>
    <tr>
      <th>175</th>
      <td>ST70Q01</td>
      <td>No of &lt;class period&gt; p/wk - &lt;test lang&gt;</td>
    </tr>
    <tr>
      <th>176</th>
      <td>ST70Q02</td>
      <td>No of &lt;class period&gt; p/wk - &lt;Maths&gt;</td>
    </tr>
    <tr>
      <th>177</th>
      <td>ST70Q03</td>
      <td>No of &lt;class period&gt; p/wk - &lt;Science&gt;</td>
    </tr>
    <tr>
      <th>178</th>
      <td>ST71Q01</td>
      <td>No of ALL &lt;class period&gt; a week</td>
    </tr>
    <tr>
      <th>179</th>
      <td>ST72Q01</td>
      <td>Class Size - No of Students in &lt;Test Language&gt; Class</td>
    </tr>
    <tr>
      <th>180</th>
      <td>ST73Q01</td>
      <td>OTL - Algebraic Word Problem in Math Lesson</td>
    </tr>
    <tr>
      <th>181</th>
      <td>ST73Q02</td>
      <td>OTL - Algebraic Word Problem in Tests</td>
    </tr>
    <tr>
      <th>182</th>
      <td>ST74Q01</td>
      <td>OTL - Procedural Task in Math Lesson</td>
    </tr>
    <tr>
      <th>183</th>
      <td>ST74Q02</td>
      <td>OTL - Procedural Task in Tests</td>
    </tr>
    <tr>
      <th>184</th>
      <td>ST75Q01</td>
      <td>OTL - Pure Math Reasoning in Math Lesson</td>
    </tr>
    <tr>
      <th>185</th>
      <td>ST75Q02</td>
      <td>OTL - Pure Math Reasoning in Tests</td>
    </tr>
    <tr>
      <th>186</th>
      <td>ST76Q01</td>
      <td>OTL - Applied Math Reasoning in Math Lesson</td>
    </tr>
    <tr>
      <th>187</th>
      <td>ST76Q02</td>
      <td>OTL - Applied Math Reasoning in Tests</td>
    </tr>
    <tr>
      <th>188</th>
      <td>ST77Q01</td>
      <td>Math Teaching - Teacher shows interest</td>
    </tr>
    <tr>
      <th>189</th>
      <td>ST77Q02</td>
      <td>Math Teaching - Extra help</td>
    </tr>
    <tr>
      <th>190</th>
      <td>ST77Q04</td>
      <td>Math Teaching - Teacher helps</td>
    </tr>
    <tr>
      <th>191</th>
      <td>ST77Q05</td>
      <td>Math Teaching - Teacher continues</td>
    </tr>
    <tr>
      <th>192</th>
      <td>ST77Q06</td>
      <td>Math Teaching - Express opinions</td>
    </tr>
    <tr>
      <th>193</th>
      <td>ST79Q01</td>
      <td>Teacher-Directed Instruction - Sets Clear Goals</td>
    </tr>
    <tr>
      <th>194</th>
      <td>ST79Q02</td>
      <td>Teacher-Directed Instruction - Encourages Thinking and Reasoning</td>
    </tr>
    <tr>
      <th>195</th>
      <td>ST79Q03</td>
      <td>Student Orientation - Differentiates Between Students When Giving Tasks</td>
    </tr>
    <tr>
      <th>196</th>
      <td>ST79Q04</td>
      <td>Student Orientation - Assigns Complex Projects</td>
    </tr>
    <tr>
      <th>197</th>
      <td>ST79Q05</td>
      <td>Formative Assessment - Gives Feedback</td>
    </tr>
    <tr>
      <th>198</th>
      <td>ST79Q06</td>
      <td>Teacher-Directed Instruction - Checks Understanding</td>
    </tr>
    <tr>
      <th>199</th>
      <td>ST79Q07</td>
      <td>Student Orientation - Has Students Work in Small Groups</td>
    </tr>
    <tr>
      <th>200</th>
      <td>ST79Q08</td>
      <td>Teacher-Directed Instruction - Summarizes Previous Lessons</td>
    </tr>
    <tr>
      <th>201</th>
      <td>ST79Q10</td>
      <td>Student Orientation - Plans Classroom Activities</td>
    </tr>
    <tr>
      <th>202</th>
      <td>ST79Q11</td>
      <td>Formative Assessment - Gives Feedback on Strengths and Weaknesses</td>
    </tr>
    <tr>
      <th>203</th>
      <td>ST79Q12</td>
      <td>Formative Assessment - Informs about Expectations</td>
    </tr>
    <tr>
      <th>204</th>
      <td>ST79Q15</td>
      <td>Teacher-Directed Instruction - Informs about Learning Goals</td>
    </tr>
    <tr>
      <th>205</th>
      <td>ST79Q17</td>
      <td>Formative Assessment - Tells How to Get Better</td>
    </tr>
    <tr>
      <th>206</th>
      <td>ST80Q01</td>
      <td>Cognitive Activation - Teacher Encourages to Reflect Problems</td>
    </tr>
    <tr>
      <th>207</th>
      <td>ST80Q04</td>
      <td>Cognitive Activation - Gives Problems that Require to Think</td>
    </tr>
    <tr>
      <th>208</th>
      <td>ST80Q05</td>
      <td>Cognitive Activation - Asks to Use Own Procedures</td>
    </tr>
    <tr>
      <th>209</th>
      <td>ST80Q06</td>
      <td>Cognitive Activation - Presents Problems with No Obvious Solutions</td>
    </tr>
    <tr>
      <th>210</th>
      <td>ST80Q07</td>
      <td>Cognitive Activation - Presents Problems in Different Contexts</td>
    </tr>
    <tr>
      <th>211</th>
      <td>ST80Q08</td>
      <td>Cognitive Activation - Helps Learn from Mistakes</td>
    </tr>
    <tr>
      <th>212</th>
      <td>ST80Q09</td>
      <td>Cognitive Activation - Asks for Explanations</td>
    </tr>
    <tr>
      <th>213</th>
      <td>ST80Q10</td>
      <td>Cognitive Activation - Apply What We Learned</td>
    </tr>
    <tr>
      <th>214</th>
      <td>ST80Q11</td>
      <td>Cognitive Activation - Problems with Multiple Solutions</td>
    </tr>
    <tr>
      <th>215</th>
      <td>ST81Q01</td>
      <td>Disciplinary Climate - Students Dont Listen</td>
    </tr>
    <tr>
      <th>216</th>
      <td>ST81Q02</td>
      <td>Disciplinary Climate - Noise and Disorder</td>
    </tr>
    <tr>
      <th>217</th>
      <td>ST81Q03</td>
      <td>Disciplinary Climate - Teacher Has to Wait Until its Quiet</td>
    </tr>
    <tr>
      <th>218</th>
      <td>ST81Q04</td>
      <td>Disciplinary Climate - Students Dont Work Well</td>
    </tr>
    <tr>
      <th>219</th>
      <td>ST81Q05</td>
      <td>Disciplinary Climate - Students Start Working Late</td>
    </tr>
    <tr>
      <th>220</th>
      <td>ST82Q01</td>
      <td>Vignette Teacher Support -Homework Every Other Day/Back in Time</td>
    </tr>
    <tr>
      <th>221</th>
      <td>ST82Q02</td>
      <td>Vignette Teacher Support - Homework Once a Week/Back in Time</td>
    </tr>
    <tr>
      <th>222</th>
      <td>ST82Q03</td>
      <td>Vignette Teacher Support - Homework Once a Week/Not Back in Time</td>
    </tr>
    <tr>
      <th>223</th>
      <td>ST83Q01</td>
      <td>Teacher Support - Lets Us Know We Have to Work Hard</td>
    </tr>
    <tr>
      <th>224</th>
      <td>ST83Q02</td>
      <td>Teacher Support - Provides Extra Help When Needed</td>
    </tr>
    <tr>
      <th>225</th>
      <td>ST83Q03</td>
      <td>Teacher Support - Helps Students with Learning</td>
    </tr>
    <tr>
      <th>226</th>
      <td>ST83Q04</td>
      <td>Teacher Support - Gives Opportunity to Express Opinions</td>
    </tr>
    <tr>
      <th>227</th>
      <td>ST84Q01</td>
      <td>Vignette Classroom Management - Students Frequently Interrupt/Teacher Arrives Early</td>
    </tr>
    <tr>
      <th>228</th>
      <td>ST84Q02</td>
      <td>Vignette Classroom Management - Students Are Calm/Teacher Arrives on Time</td>
    </tr>
    <tr>
      <th>229</th>
      <td>ST84Q03</td>
      <td>Vignette Classroom Management - Students Frequently Interrupt/Teacher Arrives Late</td>
    </tr>
    <tr>
      <th>230</th>
      <td>ST85Q01</td>
      <td>Classroom Management - Students Listen</td>
    </tr>
    <tr>
      <th>231</th>
      <td>ST85Q02</td>
      <td>Classroom Management - Teacher Keeps Class Orderly</td>
    </tr>
    <tr>
      <th>232</th>
      <td>ST85Q03</td>
      <td>Classroom Management - Teacher Starts On Time</td>
    </tr>
    <tr>
      <th>233</th>
      <td>ST85Q04</td>
      <td>Classroom Management - Wait Long to &lt;Quiet Down&gt;</td>
    </tr>
    <tr>
      <th>234</th>
      <td>ST86Q01</td>
      <td>Student-Teacher Relation - Get Along with Teachers</td>
    </tr>
    <tr>
      <th>235</th>
      <td>ST86Q02</td>
      <td>Student-Teacher Relation - Teachers Are Interested</td>
    </tr>
    <tr>
      <th>236</th>
      <td>ST86Q03</td>
      <td>Student-Teacher Relation - Teachers Listen to Students</td>
    </tr>
    <tr>
      <th>237</th>
      <td>ST86Q04</td>
      <td>Student-Teacher Relation - Teachers Help Students</td>
    </tr>
    <tr>
      <th>238</th>
      <td>ST86Q05</td>
      <td>Student-Teacher Relation - Teachers Treat Students Fair</td>
    </tr>
    <tr>
      <th>239</th>
      <td>ST87Q01</td>
      <td>Sense of Belonging - Feel Like Outsider</td>
    </tr>
    <tr>
      <th>240</th>
      <td>ST87Q02</td>
      <td>Sense of Belonging - Make Friends Easily</td>
    </tr>
    <tr>
      <th>241</th>
      <td>ST87Q03</td>
      <td>Sense of Belonging - Belong at School</td>
    </tr>
    <tr>
      <th>242</th>
      <td>ST87Q04</td>
      <td>Sense of Belonging - Feel Awkward at School</td>
    </tr>
    <tr>
      <th>243</th>
      <td>ST87Q05</td>
      <td>Sense of Belonging - Liked by Other Students</td>
    </tr>
    <tr>
      <th>244</th>
      <td>ST87Q06</td>
      <td>Sense of Belonging - Feel Lonely at School</td>
    </tr>
    <tr>
      <th>245</th>
      <td>ST87Q07</td>
      <td>Sense of Belonging - Feel Happy at School</td>
    </tr>
    <tr>
      <th>246</th>
      <td>ST87Q08</td>
      <td>Sense of Belonging - Things Are Ideal at School</td>
    </tr>
    <tr>
      <th>247</th>
      <td>ST87Q09</td>
      <td>Sense of Belonging - Satisfied at School</td>
    </tr>
    <tr>
      <th>248</th>
      <td>ST88Q01</td>
      <td>Attitude towards School - Does Little to Prepare Me for Life</td>
    </tr>
    <tr>
      <th>249</th>
      <td>ST88Q02</td>
      <td>Attitude towards School - Waste of Time</td>
    </tr>
    <tr>
      <th>250</th>
      <td>ST88Q03</td>
      <td>Attitude towards School - Gave Me Confidence</td>
    </tr>
    <tr>
      <th>251</th>
      <td>ST88Q04</td>
      <td>Attitude towards School- Useful for Job</td>
    </tr>
    <tr>
      <th>252</th>
      <td>ST89Q02</td>
      <td>Attitude toward School - Helps to Get a Job</td>
    </tr>
    <tr>
      <th>253</th>
      <td>ST89Q03</td>
      <td>Attitude toward School - Prepare for College</td>
    </tr>
    <tr>
      <th>254</th>
      <td>ST89Q04</td>
      <td>Attitude toward School - Enjoy Good Grades</td>
    </tr>
    <tr>
      <th>255</th>
      <td>ST89Q05</td>
      <td>Attitude toward School - Trying Hard is Important</td>
    </tr>
    <tr>
      <th>256</th>
      <td>ST91Q01</td>
      <td>Perceived Control - Can Succeed with Enough Effort</td>
    </tr>
    <tr>
      <th>257</th>
      <td>ST91Q02</td>
      <td>Perceived Control - My Choice Whether I Will Be Good</td>
    </tr>
    <tr>
      <th>258</th>
      <td>ST91Q03</td>
      <td>Perceived Control - Problems Prevent from Putting Effort into School</td>
    </tr>
    <tr>
      <th>259</th>
      <td>ST91Q04</td>
      <td>Perceived Control - Different Teachers Would Make Me Try Harder</td>
    </tr>
    <tr>
      <th>260</th>
      <td>ST91Q05</td>
      <td>Perceived Control - Could Perform Well if I Wanted</td>
    </tr>
    <tr>
      <th>261</th>
      <td>ST91Q06</td>
      <td>Perceived Control - Perform Poor Regardless</td>
    </tr>
    <tr>
      <th>262</th>
      <td>ST93Q01</td>
      <td>Perseverance - Give up easily</td>
    </tr>
    <tr>
      <th>263</th>
      <td>ST93Q03</td>
      <td>Perseverance - Put off difficult problems</td>
    </tr>
    <tr>
      <th>264</th>
      <td>ST93Q04</td>
      <td>Perseverance - Remain interested</td>
    </tr>
    <tr>
      <th>265</th>
      <td>ST93Q06</td>
      <td>Perseverance - Continue to perfection</td>
    </tr>
    <tr>
      <th>266</th>
      <td>ST93Q07</td>
      <td>Perseverance - Exceed expectations</td>
    </tr>
    <tr>
      <th>267</th>
      <td>ST94Q05</td>
      <td>Openness for Problem Solving - Can Handle a Lot of Information</td>
    </tr>
    <tr>
      <th>268</th>
      <td>ST94Q06</td>
      <td>Openness for Problem Solving - Quick to Understand</td>
    </tr>
    <tr>
      <th>269</th>
      <td>ST94Q09</td>
      <td>Openness for Problem Solving - Seek Explanations</td>
    </tr>
    <tr>
      <th>270</th>
      <td>ST94Q10</td>
      <td>Openness for Problem Solving - Can Link Facts</td>
    </tr>
    <tr>
      <th>271</th>
      <td>ST94Q14</td>
      <td>Openness for Problem Solving - Like to Solve Complex Problems</td>
    </tr>
    <tr>
      <th>272</th>
      <td>ST96Q01</td>
      <td>Problem Text Message - Press every button</td>
    </tr>
    <tr>
      <th>273</th>
      <td>ST96Q02</td>
      <td>Problem Text Message - Trace steps</td>
    </tr>
    <tr>
      <th>274</th>
      <td>ST96Q03</td>
      <td>Problem Text Message - Manual</td>
    </tr>
    <tr>
      <th>275</th>
      <td>ST96Q05</td>
      <td>Problem Text Message - Ask a friend</td>
    </tr>
    <tr>
      <th>276</th>
      <td>ST101Q01</td>
      <td>Problem Route Selection - Read brochure</td>
    </tr>
    <tr>
      <th>277</th>
      <td>ST101Q02</td>
      <td>Problem Route Selection - Study map</td>
    </tr>
    <tr>
      <th>278</th>
      <td>ST101Q03</td>
      <td>Problem Route Selection - Leave it to brother</td>
    </tr>
    <tr>
      <th>279</th>
      <td>ST101Q05</td>
      <td>Problem Route Selection - Just drive</td>
    </tr>
    <tr>
      <th>280</th>
      <td>ST104Q01</td>
      <td>Problem Ticket Machine - Similarities</td>
    </tr>
    <tr>
      <th>281</th>
      <td>ST104Q04</td>
      <td>Problem Ticket Machine - Try buttons</td>
    </tr>
    <tr>
      <th>282</th>
      <td>ST104Q05</td>
      <td>Problem Ticket Machine - Ask for help</td>
    </tr>
    <tr>
      <th>283</th>
      <td>ST104Q06</td>
      <td>Problem Ticket Machine - Find ticket office</td>
    </tr>
    <tr>
      <th>284</th>
      <td>IC01Q01</td>
      <td>At Home - Desktop Computer</td>
    </tr>
    <tr>
      <th>285</th>
      <td>IC01Q02</td>
      <td>At Home - Portable laptop</td>
    </tr>
    <tr>
      <th>286</th>
      <td>IC01Q03</td>
      <td>At Home - Tablet computer</td>
    </tr>
    <tr>
      <th>287</th>
      <td>IC01Q04</td>
      <td>At Home - Internet connection</td>
    </tr>
    <tr>
      <th>288</th>
      <td>IC01Q05</td>
      <td>At Home - Video games console</td>
    </tr>
    <tr>
      <th>289</th>
      <td>IC01Q06</td>
      <td>At Home - Cell phone w/o Internet</td>
    </tr>
    <tr>
      <th>290</th>
      <td>IC01Q07</td>
      <td>At Home - Cell phone with Internet</td>
    </tr>
    <tr>
      <th>291</th>
      <td>IC01Q08</td>
      <td>At Home - Mp3/Mp4 player</td>
    </tr>
    <tr>
      <th>292</th>
      <td>IC01Q09</td>
      <td>At Home - Printer</td>
    </tr>
    <tr>
      <th>293</th>
      <td>IC01Q10</td>
      <td>At Home - USB (memory) stick</td>
    </tr>
    <tr>
      <th>294</th>
      <td>IC01Q11</td>
      <td>At Home - Ebook reader</td>
    </tr>
    <tr>
      <th>295</th>
      <td>IC02Q01</td>
      <td>At school - Desktop Computer</td>
    </tr>
    <tr>
      <th>296</th>
      <td>IC02Q02</td>
      <td>At school - Portable laptop</td>
    </tr>
    <tr>
      <th>297</th>
      <td>IC02Q03</td>
      <td>At school - Tablet computer</td>
    </tr>
    <tr>
      <th>298</th>
      <td>IC02Q04</td>
      <td>At school - Internet connection</td>
    </tr>
    <tr>
      <th>299</th>
      <td>IC02Q05</td>
      <td>At school - Printer</td>
    </tr>
    <tr>
      <th>300</th>
      <td>IC02Q06</td>
      <td>At school - USB (memory) stick</td>
    </tr>
    <tr>
      <th>301</th>
      <td>IC02Q07</td>
      <td>At school - Ebook reader</td>
    </tr>
    <tr>
      <th>302</th>
      <td>IC03Q01</td>
      <td>First use of computers</td>
    </tr>
    <tr>
      <th>303</th>
      <td>IC04Q01</td>
      <td>First access to Internet</td>
    </tr>
    <tr>
      <th>304</th>
      <td>IC05Q01</td>
      <td>Internet at School</td>
    </tr>
    <tr>
      <th>305</th>
      <td>IC06Q01</td>
      <td>Internet out-of-school - Weekday</td>
    </tr>
    <tr>
      <th>306</th>
      <td>IC07Q01</td>
      <td>Internet out-of-school - Weekend</td>
    </tr>
    <tr>
      <th>307</th>
      <td>IC08Q01</td>
      <td>Out-of-school 8 - One player games.</td>
    </tr>
    <tr>
      <th>308</th>
      <td>IC08Q02</td>
      <td>Out-of-school 8 - ColLabourative games.</td>
    </tr>
    <tr>
      <th>309</th>
      <td>IC08Q03</td>
      <td>Out-of-school 8 - Use email</td>
    </tr>
    <tr>
      <th>310</th>
      <td>IC08Q04</td>
      <td>Out-of-school 8 - Chat on line</td>
    </tr>
    <tr>
      <th>311</th>
      <td>IC08Q05</td>
      <td>Out-of-school 8 - Social networks</td>
    </tr>
    <tr>
      <th>312</th>
      <td>IC08Q06</td>
      <td>Out-of-school 8 - Browse the Internet for fun</td>
    </tr>
    <tr>
      <th>313</th>
      <td>IC08Q07</td>
      <td>Out-of-school 8 - Read news</td>
    </tr>
    <tr>
      <th>314</th>
      <td>IC08Q08</td>
      <td>Out-of-school 8 - Obtain practical information from the Internet</td>
    </tr>
    <tr>
      <th>315</th>
      <td>IC08Q09</td>
      <td>Out-of-school 8 - Download music</td>
    </tr>
    <tr>
      <th>316</th>
      <td>IC08Q11</td>
      <td>Out-of-school 8 - Upload content</td>
    </tr>
    <tr>
      <th>317</th>
      <td>IC09Q01</td>
      <td>Out-of-school 9 - Internet for school</td>
    </tr>
    <tr>
      <th>318</th>
      <td>IC09Q02</td>
      <td>Out-of-school 9 - Email students</td>
    </tr>
    <tr>
      <th>319</th>
      <td>IC09Q03</td>
      <td>Out-of-school 9 - Email teachers</td>
    </tr>
    <tr>
      <th>320</th>
      <td>IC09Q04</td>
      <td>Out-of-school 9 - Download from School</td>
    </tr>
    <tr>
      <th>321</th>
      <td>IC09Q05</td>
      <td>Out-of-school 9 - Announcements</td>
    </tr>
    <tr>
      <th>322</th>
      <td>IC09Q06</td>
      <td>Out-of-school 9 - Homework</td>
    </tr>
    <tr>
      <th>323</th>
      <td>IC09Q07</td>
      <td>Out-of-school 9 - Share school material</td>
    </tr>
    <tr>
      <th>324</th>
      <td>IC10Q01</td>
      <td>At School - Chat on line</td>
    </tr>
    <tr>
      <th>325</th>
      <td>IC10Q02</td>
      <td>At School - Email</td>
    </tr>
    <tr>
      <th>326</th>
      <td>IC10Q03</td>
      <td>At School - Browse for schoolwork</td>
    </tr>
    <tr>
      <th>327</th>
      <td>IC10Q04</td>
      <td>At School - Download from website</td>
    </tr>
    <tr>
      <th>328</th>
      <td>IC10Q05</td>
      <td>At School - Post on website</td>
    </tr>
    <tr>
      <th>329</th>
      <td>IC10Q06</td>
      <td>At School - Simulations</td>
    </tr>
    <tr>
      <th>330</th>
      <td>IC10Q07</td>
      <td>At School - Practice and drilling</td>
    </tr>
    <tr>
      <th>331</th>
      <td>IC10Q08</td>
      <td>At School - Homework</td>
    </tr>
    <tr>
      <th>332</th>
      <td>IC10Q09</td>
      <td>At School - Group work</td>
    </tr>
    <tr>
      <th>333</th>
      <td>IC11Q01</td>
      <td>Maths lessons - Draw graph</td>
    </tr>
    <tr>
      <th>334</th>
      <td>IC11Q02</td>
      <td>Maths lessons - Calculation with numbers</td>
    </tr>
    <tr>
      <th>335</th>
      <td>IC11Q03</td>
      <td>Maths lessons - Geometric figures</td>
    </tr>
    <tr>
      <th>336</th>
      <td>IC11Q04</td>
      <td>Maths lessons - Spreadsheet</td>
    </tr>
    <tr>
      <th>337</th>
      <td>IC11Q05</td>
      <td>Maths lessons - Algebra</td>
    </tr>
    <tr>
      <th>338</th>
      <td>IC11Q06</td>
      <td>Maths lessons - Histograms</td>
    </tr>
    <tr>
      <th>339</th>
      <td>IC11Q07</td>
      <td>Maths lessons - Change in graphs</td>
    </tr>
    <tr>
      <th>340</th>
      <td>IC22Q01</td>
      <td>Attitudes - Useful for schoolwork</td>
    </tr>
    <tr>
      <th>341</th>
      <td>IC22Q02</td>
      <td>Attitudes - Homework more fun</td>
    </tr>
    <tr>
      <th>342</th>
      <td>IC22Q04</td>
      <td>Attitudes - Source of information</td>
    </tr>
    <tr>
      <th>343</th>
      <td>IC22Q06</td>
      <td>Attitudes - Troublesome</td>
    </tr>
    <tr>
      <th>344</th>
      <td>IC22Q07</td>
      <td>Attitudes - Not suitable for schoolwork</td>
    </tr>
    <tr>
      <th>345</th>
      <td>IC22Q08</td>
      <td>Attitudes - Too unreliable</td>
    </tr>
    <tr>
      <th>346</th>
      <td>EC01Q01</td>
      <td>Miss 2 months of &lt;ISCED 1&gt;</td>
    </tr>
    <tr>
      <th>347</th>
      <td>EC02Q01</td>
      <td>Miss 2 months of &lt;ISCED 2&gt;</td>
    </tr>
    <tr>
      <th>348</th>
      <td>EC03Q01</td>
      <td>Future Orientation - Internship</td>
    </tr>
    <tr>
      <th>349</th>
      <td>EC03Q02</td>
      <td>Future Orientation - Work-site visits</td>
    </tr>
    <tr>
      <th>350</th>
      <td>EC03Q03</td>
      <td>Future Orientation - Job fair</td>
    </tr>
    <tr>
      <th>351</th>
      <td>EC03Q04</td>
      <td>Future Orientation - Career advisor at school</td>
    </tr>
    <tr>
      <th>352</th>
      <td>EC03Q05</td>
      <td>Future Orientation - Career advisor outside school</td>
    </tr>
    <tr>
      <th>353</th>
      <td>EC03Q06</td>
      <td>Future Orientation - Questionnaire</td>
    </tr>
    <tr>
      <th>354</th>
      <td>EC03Q07</td>
      <td>Future Orientation - Internet search</td>
    </tr>
    <tr>
      <th>355</th>
      <td>EC03Q08</td>
      <td>Future Orientation - Tour&lt;ISCED 3-5&gt; institution</td>
    </tr>
    <tr>
      <th>356</th>
      <td>EC03Q09</td>
      <td>Future Orientation - web search &lt;ISCED 3-5&gt; prog</td>
    </tr>
    <tr>
      <th>357</th>
      <td>EC03Q10</td>
      <td>Future Orientation - &lt;country specific item&gt;</td>
    </tr>
    <tr>
      <th>358</th>
      <td>EC04Q01A</td>
      <td>Acquired skills - Find job info - Yes, at school</td>
    </tr>
    <tr>
      <th>359</th>
      <td>EC04Q01B</td>
      <td>Acquired skills - Find job info - Yes, out of school</td>
    </tr>
    <tr>
      <th>360</th>
      <td>EC04Q01C</td>
      <td>Acquired skills - Find job info - No, never</td>
    </tr>
    <tr>
      <th>361</th>
      <td>EC04Q02A</td>
      <td>Acquired skills - Search for job - Yes, at school</td>
    </tr>
    <tr>
      <th>362</th>
      <td>EC04Q02B</td>
      <td>Acquired skills - Search for job - Yes, out of school</td>
    </tr>
    <tr>
      <th>363</th>
      <td>EC04Q02C</td>
      <td>Acquired skills - Search for job - No, never</td>
    </tr>
    <tr>
      <th>364</th>
      <td>EC04Q03A</td>
      <td>Acquired skills - Write resume - Yes, at school</td>
    </tr>
    <tr>
      <th>365</th>
      <td>EC04Q03B</td>
      <td>Acquired skills - Write resume - Yes, out of school</td>
    </tr>
    <tr>
      <th>366</th>
      <td>EC04Q03C</td>
      <td>Acquired skills - Write resume - No, never</td>
    </tr>
    <tr>
      <th>367</th>
      <td>EC04Q04A</td>
      <td>Acquired skills - Job interview - Yes, at school</td>
    </tr>
    <tr>
      <th>368</th>
      <td>EC04Q04B</td>
      <td>Acquired skills - Job interview - Yes, out of school</td>
    </tr>
    <tr>
      <th>369</th>
      <td>EC04Q04C</td>
      <td>Acquired skills - Job interview - No, never</td>
    </tr>
    <tr>
      <th>370</th>
      <td>EC04Q05A</td>
      <td>Acquired skills - ISCED 3-5 programs - Yes, at school</td>
    </tr>
    <tr>
      <th>371</th>
      <td>EC04Q05B</td>
      <td>Acquired skills - ISCED 3-5 programs - Yes, out of school</td>
    </tr>
    <tr>
      <th>372</th>
      <td>EC04Q05C</td>
      <td>Acquired skills - ISCED 3-5 programs - No, never</td>
    </tr>
    <tr>
      <th>373</th>
      <td>EC04Q06A</td>
      <td>Acquired skills - Student financing - Yes, at school</td>
    </tr>
    <tr>
      <th>374</th>
      <td>EC04Q06B</td>
      <td>Acquired skills - Student financing - Yes, out of school</td>
    </tr>
    <tr>
      <th>375</th>
      <td>EC04Q06C</td>
      <td>Acquired skills - Student financing - No, never</td>
    </tr>
    <tr>
      <th>376</th>
      <td>EC05Q01</td>
      <td>First language learned</td>
    </tr>
    <tr>
      <th>377</th>
      <td>EC06Q01</td>
      <td>Age started learning &lt;test language&gt;</td>
    </tr>
    <tr>
      <th>378</th>
      <td>EC07Q01</td>
      <td>Language spoken - Mother</td>
    </tr>
    <tr>
      <th>379</th>
      <td>EC07Q02</td>
      <td>Language spoken - Father</td>
    </tr>
    <tr>
      <th>380</th>
      <td>EC07Q03</td>
      <td>Language spoken - Siblings</td>
    </tr>
    <tr>
      <th>381</th>
      <td>EC07Q04</td>
      <td>Language spoken - Best friend</td>
    </tr>
    <tr>
      <th>382</th>
      <td>EC07Q05</td>
      <td>Language spoken - Schoolmates</td>
    </tr>
    <tr>
      <th>383</th>
      <td>EC08Q01</td>
      <td>Activities language - Reading</td>
    </tr>
    <tr>
      <th>384</th>
      <td>EC08Q02</td>
      <td>Activities language - Watching TV</td>
    </tr>
    <tr>
      <th>385</th>
      <td>EC08Q03</td>
      <td>Activities language - Internet surfing</td>
    </tr>
    <tr>
      <th>386</th>
      <td>EC08Q04</td>
      <td>Activities language - Writing emails</td>
    </tr>
    <tr>
      <th>387</th>
      <td>EC09Q03</td>
      <td>Types of support &lt;test language&gt; - remedial lessons</td>
    </tr>
    <tr>
      <th>388</th>
      <td>EC10Q01</td>
      <td>Amount of support &lt;test language&gt;</td>
    </tr>
    <tr>
      <th>389</th>
      <td>EC11Q02</td>
      <td>Attend lessons &lt;heritage language&gt; - focused</td>
    </tr>
    <tr>
      <th>390</th>
      <td>EC11Q03</td>
      <td>Attend lessons &lt;heritage language&gt; - school subjects</td>
    </tr>
    <tr>
      <th>391</th>
      <td>EC12Q01</td>
      <td>Instruction in &lt;heritage language&gt;</td>
    </tr>
    <tr>
      <th>392</th>
      <td>ST22Q01</td>
      <td>Acculturation - Mother Immigrant (Filter)</td>
    </tr>
    <tr>
      <th>393</th>
      <td>ST23Q01</td>
      <td>Acculturation - Enjoy &lt;Host Culture&gt; Friends</td>
    </tr>
    <tr>
      <th>394</th>
      <td>ST23Q02</td>
      <td>Acculturation - Enjoy &lt;Heritage Culture&gt; Friends</td>
    </tr>
    <tr>
      <th>395</th>
      <td>ST23Q03</td>
      <td>Acculturation - Enjoy &lt;Host Culture&gt; Celebrations</td>
    </tr>
    <tr>
      <th>396</th>
      <td>ST23Q04</td>
      <td>Acculturation - Enjoy &lt;Heritage Culture&gt; Celebrations</td>
    </tr>
    <tr>
      <th>397</th>
      <td>ST23Q05</td>
      <td>Acculturation - Spend Time with &lt;Host Culture&gt; Friends</td>
    </tr>
    <tr>
      <th>398</th>
      <td>ST23Q06</td>
      <td>Acculturation - Spend Time with &lt;Heritage Culture&gt; Friends</td>
    </tr>
    <tr>
      <th>399</th>
      <td>ST23Q07</td>
      <td>Acculturation - Participate in &lt;Host Culture&gt; Celebrations</td>
    </tr>
    <tr>
      <th>400</th>
      <td>ST23Q08</td>
      <td>Acculturation - Participate in &lt;Heritage Culture&gt; Celebrations</td>
    </tr>
    <tr>
      <th>401</th>
      <td>ST24Q01</td>
      <td>Acculturation - Perceived Host-Heritage Cultural Differences - Values</td>
    </tr>
    <tr>
      <th>402</th>
      <td>ST24Q02</td>
      <td>Acculturation - Perceived Host-Heritage Cultural Differences - Mother Treatment</td>
    </tr>
    <tr>
      <th>403</th>
      <td>ST24Q03</td>
      <td>Acculturation - Perceived Host-Heritage Cultural Differences - Teacher Treatment</td>
    </tr>
    <tr>
      <th>404</th>
      <td>CLCUSE1</td>
      <td>Calculator Use</td>
    </tr>
    <tr>
      <th>405</th>
      <td>CLCUSE301</td>
      <td>Effort-real 1</td>
    </tr>
    <tr>
      <th>406</th>
      <td>CLCUSE302</td>
      <td>Effort-real 2</td>
    </tr>
    <tr>
      <th>407</th>
      <td>DEFFORT</td>
      <td>Difference in Effort</td>
    </tr>
    <tr>
      <th>408</th>
      <td>QUESTID</td>
      <td>Student Questionnaire Form</td>
    </tr>
    <tr>
      <th>409</th>
      <td>BOOKID</td>
      <td>Booklet ID</td>
    </tr>
    <tr>
      <th>410</th>
      <td>EASY</td>
      <td>Standard or simplified set of booklets</td>
    </tr>
    <tr>
      <th>411</th>
      <td>AGE</td>
      <td>Age of student</td>
    </tr>
    <tr>
      <th>412</th>
      <td>GRADE</td>
      <td>Grade compared to modal grade in country</td>
    </tr>
    <tr>
      <th>413</th>
      <td>PROGN</td>
      <td>Unique national study programme code</td>
    </tr>
    <tr>
      <th>414</th>
      <td>ANXMAT</td>
      <td>Mathematics Anxiety</td>
    </tr>
    <tr>
      <th>415</th>
      <td>ATSCHL</td>
      <td>Attitude towards School: Learning Outcomes</td>
    </tr>
    <tr>
      <th>416</th>
      <td>ATTLNACT</td>
      <td>Attitude towards School: Learning Activities</td>
    </tr>
    <tr>
      <th>417</th>
      <td>BELONG</td>
      <td>Sense of Belonging to School</td>
    </tr>
    <tr>
      <th>418</th>
      <td>BFMJ2</td>
      <td>Father SQ ISEI</td>
    </tr>
    <tr>
      <th>419</th>
      <td>BMMJ1</td>
      <td>Mother SQ ISEI</td>
    </tr>
    <tr>
      <th>420</th>
      <td>CLSMAN</td>
      <td>Mathematics Teacher's Classroom Management</td>
    </tr>
    <tr>
      <th>421</th>
      <td>COBN_F</td>
      <td>Country of Birth National Categories- Father</td>
    </tr>
    <tr>
      <th>422</th>
      <td>COBN_M</td>
      <td>Country of Birth National Categories- Mother</td>
    </tr>
    <tr>
      <th>423</th>
      <td>COBN_S</td>
      <td>Country of Birth National Categories- Self</td>
    </tr>
    <tr>
      <th>424</th>
      <td>COGACT</td>
      <td>Cognitive Activation in Mathematics Lessons</td>
    </tr>
    <tr>
      <th>425</th>
      <td>CULTDIST</td>
      <td>Cultural Distance between Host and Heritage Culture</td>
    </tr>
    <tr>
      <th>426</th>
      <td>CULTPOS</td>
      <td>Cultural Possessions</td>
    </tr>
    <tr>
      <th>427</th>
      <td>DISCLIMA</td>
      <td>Disciplinary Climate</td>
    </tr>
    <tr>
      <th>428</th>
      <td>ENTUSE</td>
      <td>ICT Entertainment Use</td>
    </tr>
    <tr>
      <th>429</th>
      <td>ESCS</td>
      <td>Index of economic, social and cultural status</td>
    </tr>
    <tr>
      <th>430</th>
      <td>EXAPPLM</td>
      <td>Experience with Applied Mathematics Tasks at School</td>
    </tr>
    <tr>
      <th>431</th>
      <td>EXPUREM</td>
      <td>Experience with Pure Mathematics Tasks at School</td>
    </tr>
    <tr>
      <th>432</th>
      <td>FAILMAT</td>
      <td>Attributions to Failure in Mathematics</td>
    </tr>
    <tr>
      <th>433</th>
      <td>FAMCON</td>
      <td>Familiarity with Mathematical Concepts</td>
    </tr>
    <tr>
      <th>434</th>
      <td>FAMCONC</td>
      <td>Familiarity with Mathematical Concepts (Signal Detection  Adjusted)</td>
    </tr>
    <tr>
      <th>435</th>
      <td>FAMSTRUC</td>
      <td>Family Structure</td>
    </tr>
    <tr>
      <th>436</th>
      <td>FISCED</td>
      <td>Educational level of father (ISCED)</td>
    </tr>
    <tr>
      <th>437</th>
      <td>HEDRES</td>
      <td>Home educational resources</td>
    </tr>
    <tr>
      <th>438</th>
      <td>HERITCUL</td>
      <td>Acculturation: Heritage Culture Oriented  Strategies</td>
    </tr>
    <tr>
      <th>439</th>
      <td>HISCED</td>
      <td>Highest educational level of parents</td>
    </tr>
    <tr>
      <th>440</th>
      <td>HISEI</td>
      <td>Highest parental occupational status</td>
    </tr>
    <tr>
      <th>441</th>
      <td>HOMEPOS</td>
      <td>Home Possessions</td>
    </tr>
    <tr>
      <th>442</th>
      <td>HOMSCH</td>
      <td>ICT Use at Home for School-related Tasks</td>
    </tr>
    <tr>
      <th>443</th>
      <td>HOSTCUL</td>
      <td>Acculturation: Host Culture Oriented Strategies</td>
    </tr>
    <tr>
      <th>444</th>
      <td>ICTATTNEG</td>
      <td>Attitudes Towards Computers: Limitations of the Computer as a Tool for School Learning</td>
    </tr>
    <tr>
      <th>445</th>
      <td>ICTATTPOS</td>
      <td>Attitudes Towards Computers: Computer as a Tool for School Learning</td>
    </tr>
    <tr>
      <th>446</th>
      <td>ICTHOME</td>
      <td>ICT Availability at Home</td>
    </tr>
    <tr>
      <th>447</th>
      <td>ICTRES</td>
      <td>ICT resources</td>
    </tr>
    <tr>
      <th>448</th>
      <td>ICTSCH</td>
      <td>ICT Availability at School</td>
    </tr>
    <tr>
      <th>449</th>
      <td>IMMIG</td>
      <td>Immigration status</td>
    </tr>
    <tr>
      <th>450</th>
      <td>INFOCAR</td>
      <td>Information about Careers</td>
    </tr>
    <tr>
      <th>451</th>
      <td>INFOJOB1</td>
      <td>Information about the Labour Market provided by the School</td>
    </tr>
    <tr>
      <th>452</th>
      <td>INFOJOB2</td>
      <td>Information about the Labour Market provided outside of School</td>
    </tr>
    <tr>
      <th>453</th>
      <td>INSTMOT</td>
      <td>Instrumental Motivation for Mathematics</td>
    </tr>
    <tr>
      <th>454</th>
      <td>INTMAT</td>
      <td>Mathematics Interest</td>
    </tr>
    <tr>
      <th>455</th>
      <td>ISCEDD</td>
      <td>ISCED designation</td>
    </tr>
    <tr>
      <th>456</th>
      <td>ISCEDL</td>
      <td>ISCED level</td>
    </tr>
    <tr>
      <th>457</th>
      <td>ISCEDO</td>
      <td>ISCED orientation</td>
    </tr>
    <tr>
      <th>458</th>
      <td>LANGCOMM</td>
      <td>Preference for Heritage Language in Conversations with Family and Friends</td>
    </tr>
    <tr>
      <th>459</th>
      <td>LANGN</td>
      <td>Language at home (3-digit code)</td>
    </tr>
    <tr>
      <th>460</th>
      <td>LANGRPPD</td>
      <td>Preference for Heritage Language in Language Reception and Production</td>
    </tr>
    <tr>
      <th>461</th>
      <td>LMINS</td>
      <td>Learning time (minutes per week)  - &lt;test language&gt;</td>
    </tr>
    <tr>
      <th>462</th>
      <td>MATBEH</td>
      <td>Mathematics Behaviour</td>
    </tr>
    <tr>
      <th>463</th>
      <td>MATHEFF</td>
      <td>Mathematics Self-Efficacy</td>
    </tr>
    <tr>
      <th>464</th>
      <td>MATINTFC</td>
      <td>Mathematics Intentions</td>
    </tr>
    <tr>
      <th>465</th>
      <td>MATWKETH</td>
      <td>Mathematics Work Ethic</td>
    </tr>
    <tr>
      <th>466</th>
      <td>MISCED</td>
      <td>Educational level of mother (ISCED)</td>
    </tr>
    <tr>
      <th>467</th>
      <td>MMINS</td>
      <td>Learning time (minutes per week)- &lt;Mathematics&gt;</td>
    </tr>
    <tr>
      <th>468</th>
      <td>MTSUP</td>
      <td>Mathematics Teacher's Support</td>
    </tr>
    <tr>
      <th>469</th>
      <td>OCOD1</td>
      <td>ISCO-08 Occupation code - Mother</td>
    </tr>
    <tr>
      <th>470</th>
      <td>OCOD2</td>
      <td>ISCO-08 Occupation code - Father</td>
    </tr>
    <tr>
      <th>471</th>
      <td>OPENPS</td>
      <td>Openness for Problem Solving</td>
    </tr>
    <tr>
      <th>472</th>
      <td>OUTHOURS</td>
      <td>Out-of-School Study Time</td>
    </tr>
    <tr>
      <th>473</th>
      <td>PARED</td>
      <td>Highest parental education in years</td>
    </tr>
    <tr>
      <th>474</th>
      <td>PERSEV</td>
      <td>Perseverance</td>
    </tr>
    <tr>
      <th>475</th>
      <td>REPEAT</td>
      <td>Grade Repetition</td>
    </tr>
    <tr>
      <th>476</th>
      <td>SCMAT</td>
      <td>Mathematics Self-Concept</td>
    </tr>
    <tr>
      <th>477</th>
      <td>SMINS</td>
      <td>Learning time (minutes per week) - &lt;Science&gt;</td>
    </tr>
    <tr>
      <th>478</th>
      <td>STUDREL</td>
      <td>Teacher Student Relations</td>
    </tr>
    <tr>
      <th>479</th>
      <td>SUBNORM</td>
      <td>Subjective Norms in Mathematics</td>
    </tr>
    <tr>
      <th>480</th>
      <td>TCHBEHFA</td>
      <td>Teacher Behaviour: Formative Assessment</td>
    </tr>
    <tr>
      <th>481</th>
      <td>TCHBEHSO</td>
      <td>Teacher Behaviour: Student Orientation</td>
    </tr>
    <tr>
      <th>482</th>
      <td>TCHBEHTD</td>
      <td>Teacher Behaviour: Teacher-directed Instruction</td>
    </tr>
    <tr>
      <th>483</th>
      <td>TEACHSUP</td>
      <td>Teacher Support</td>
    </tr>
    <tr>
      <th>484</th>
      <td>TESTLANG</td>
      <td>Language of the test</td>
    </tr>
    <tr>
      <th>485</th>
      <td>TIMEINT</td>
      <td>Time of computer use (mins)</td>
    </tr>
    <tr>
      <th>486</th>
      <td>USEMATH</td>
      <td>Use of ICT in Mathematic Lessons</td>
    </tr>
    <tr>
      <th>487</th>
      <td>USESCH</td>
      <td>Use of ICT at School</td>
    </tr>
    <tr>
      <th>488</th>
      <td>WEALTH</td>
      <td>Wealth</td>
    </tr>
    <tr>
      <th>489</th>
      <td>ANCATSCHL</td>
      <td>Attitude towards School: Learning Outcomes (Anchored)</td>
    </tr>
    <tr>
      <th>490</th>
      <td>ANCATTLNACT</td>
      <td>Attitude towards School: Learning Activities (Anchored)</td>
    </tr>
    <tr>
      <th>491</th>
      <td>ANCBELONG</td>
      <td>Sense of Belonging to School (Anchored)</td>
    </tr>
    <tr>
      <th>492</th>
      <td>ANCCLSMAN</td>
      <td>Mathematics Teacher's Classroom Management (Anchored)</td>
    </tr>
    <tr>
      <th>493</th>
      <td>ANCCOGACT</td>
      <td>Cognitive Activation in Mathematics Lessons (Anchored)</td>
    </tr>
    <tr>
      <th>494</th>
      <td>ANCINSTMOT</td>
      <td>Instrumental Motivation for Mathematics (Anchored)</td>
    </tr>
    <tr>
      <th>495</th>
      <td>ANCINTMAT</td>
      <td>Mathematics Interest (Anchored)</td>
    </tr>
    <tr>
      <th>496</th>
      <td>ANCMATWKETH</td>
      <td>Mathematics Work Ethic (Anchored)</td>
    </tr>
    <tr>
      <th>497</th>
      <td>ANCMTSUP</td>
      <td>Mathematics Teacher's Support (Anchored)</td>
    </tr>
    <tr>
      <th>498</th>
      <td>ANCSCMAT</td>
      <td>Mathematics Self-Concept (Anchored)</td>
    </tr>
    <tr>
      <th>499</th>
      <td>ANCSTUDREL</td>
      <td>Teacher Student Relations (Anchored)</td>
    </tr>
    <tr>
      <th>500</th>
      <td>ANCSUBNORM</td>
      <td>Subjective Norms in Mathematics (Anchored)</td>
    </tr>
    <tr>
      <th>501</th>
      <td>PV1MATH</td>
      <td>Plausible value 1 in mathematics</td>
    </tr>
    <tr>
      <th>502</th>
      <td>PV2MATH</td>
      <td>Plausible value 2 in mathematics</td>
    </tr>
    <tr>
      <th>503</th>
      <td>PV3MATH</td>
      <td>Plausible value 3 in mathematics</td>
    </tr>
    <tr>
      <th>504</th>
      <td>PV4MATH</td>
      <td>Plausible value 4 in mathematics</td>
    </tr>
    <tr>
      <th>505</th>
      <td>PV5MATH</td>
      <td>Plausible value 5 in mathematics</td>
    </tr>
    <tr>
      <th>506</th>
      <td>PV1MACC</td>
      <td>Plausible value 1 in content subscale of math - Change and Relationships</td>
    </tr>
    <tr>
      <th>507</th>
      <td>PV2MACC</td>
      <td>Plausible value 2 in content subscale of math - Change and Relationships</td>
    </tr>
    <tr>
      <th>508</th>
      <td>PV3MACC</td>
      <td>Plausible value 3 in content subscale of math - Change and Relationships</td>
    </tr>
    <tr>
      <th>509</th>
      <td>PV4MACC</td>
      <td>Plausible value 4 in content subscale of math - Change and Relationships</td>
    </tr>
    <tr>
      <th>510</th>
      <td>PV5MACC</td>
      <td>Plausible value 5 in content subscale of math - Change and Relationships</td>
    </tr>
    <tr>
      <th>511</th>
      <td>PV1MACQ</td>
      <td>Plausible value 1 in content subscale of math - Quantity</td>
    </tr>
    <tr>
      <th>512</th>
      <td>PV2MACQ</td>
      <td>Plausible value 2 in content subscale of math - Quantity</td>
    </tr>
    <tr>
      <th>513</th>
      <td>PV3MACQ</td>
      <td>Plausible value 3 in content subscale of math - Quantity</td>
    </tr>
    <tr>
      <th>514</th>
      <td>PV4MACQ</td>
      <td>Plausible value 4 in content subscale of math - Quantity</td>
    </tr>
    <tr>
      <th>515</th>
      <td>PV5MACQ</td>
      <td>Plausible value 5 in content subscale of math - Quantity</td>
    </tr>
    <tr>
      <th>516</th>
      <td>PV1MACS</td>
      <td>Plausible value 1 in content subscale of math - Space and Shape</td>
    </tr>
    <tr>
      <th>517</th>
      <td>PV2MACS</td>
      <td>Plausible value 2 in content subscale of math - Space and Shape</td>
    </tr>
    <tr>
      <th>518</th>
      <td>PV3MACS</td>
      <td>Plausible value 3 in content subscale of math - Space and Shape</td>
    </tr>
    <tr>
      <th>519</th>
      <td>PV4MACS</td>
      <td>Plausible value 4 in content subscale of math - Space and Shape</td>
    </tr>
    <tr>
      <th>520</th>
      <td>PV5MACS</td>
      <td>Plausible value 5 in content subscale of math - Space and Shape</td>
    </tr>
    <tr>
      <th>521</th>
      <td>PV1MACU</td>
      <td>Plausible value 1 in content subscale of math - Uncertainty and Data</td>
    </tr>
    <tr>
      <th>522</th>
      <td>PV2MACU</td>
      <td>Plausible value 2 in content subscale of math - Uncertainty and Data</td>
    </tr>
    <tr>
      <th>523</th>
      <td>PV3MACU</td>
      <td>Plausible value 3 in content subscale of math - Uncertainty and Data</td>
    </tr>
    <tr>
      <th>524</th>
      <td>PV4MACU</td>
      <td>Plausible value 4 in content subscale of math - Uncertainty and Data</td>
    </tr>
    <tr>
      <th>525</th>
      <td>PV5MACU</td>
      <td>Plausible value 5 in content subscale of math - Uncertainty and Data</td>
    </tr>
    <tr>
      <th>526</th>
      <td>PV1MAPE</td>
      <td>Plausible value 1 in process subscale of math - Employ</td>
    </tr>
    <tr>
      <th>527</th>
      <td>PV2MAPE</td>
      <td>Plausible value 2 in process subscale of math - Employ</td>
    </tr>
    <tr>
      <th>528</th>
      <td>PV3MAPE</td>
      <td>Plausible value 3 in process subscale of math - Employ</td>
    </tr>
    <tr>
      <th>529</th>
      <td>PV4MAPE</td>
      <td>Plausible value 4 in process subscale of math - Employ</td>
    </tr>
    <tr>
      <th>530</th>
      <td>PV5MAPE</td>
      <td>Plausible value 5 in process subscale of math - Employ</td>
    </tr>
    <tr>
      <th>531</th>
      <td>PV1MAPF</td>
      <td>Plausible value 1 in process subscale of math - Formulate</td>
    </tr>
    <tr>
      <th>532</th>
      <td>PV2MAPF</td>
      <td>Plausible value 2 in process subscale of math - Formulate</td>
    </tr>
    <tr>
      <th>533</th>
      <td>PV3MAPF</td>
      <td>Plausible value 3 in process subscale of math - Formulate</td>
    </tr>
    <tr>
      <th>534</th>
      <td>PV4MAPF</td>
      <td>Plausible value 4 in process subscale of math - Formulate</td>
    </tr>
    <tr>
      <th>535</th>
      <td>PV5MAPF</td>
      <td>Plausible value 5 in process subscale of math - Formulate</td>
    </tr>
    <tr>
      <th>536</th>
      <td>PV1MAPI</td>
      <td>Plausible value 1 in process subscale of math - Interpret</td>
    </tr>
    <tr>
      <th>537</th>
      <td>PV2MAPI</td>
      <td>Plausible value 2 in process subscale of math - Interpret</td>
    </tr>
    <tr>
      <th>538</th>
      <td>PV3MAPI</td>
      <td>Plausible value 3 in process subscale of math - Interpret</td>
    </tr>
    <tr>
      <th>539</th>
      <td>PV4MAPI</td>
      <td>Plausible value 4 in process subscale of math - Interpret</td>
    </tr>
    <tr>
      <th>540</th>
      <td>PV5MAPI</td>
      <td>Plausible value 5 in process subscale of math - Interpret</td>
    </tr>
    <tr>
      <th>541</th>
      <td>PV1READ</td>
      <td>Plausible value 1 in reading</td>
    </tr>
    <tr>
      <th>542</th>
      <td>PV2READ</td>
      <td>Plausible value 2 in reading</td>
    </tr>
    <tr>
      <th>543</th>
      <td>PV3READ</td>
      <td>Plausible value 3 in reading</td>
    </tr>
    <tr>
      <th>544</th>
      <td>PV4READ</td>
      <td>Plausible value 4 in reading</td>
    </tr>
    <tr>
      <th>545</th>
      <td>PV5READ</td>
      <td>Plausible value 5 in reading</td>
    </tr>
    <tr>
      <th>546</th>
      <td>PV1SCIE</td>
      <td>Plausible value 1 in science</td>
    </tr>
    <tr>
      <th>547</th>
      <td>PV2SCIE</td>
      <td>Plausible value 2 in science</td>
    </tr>
    <tr>
      <th>548</th>
      <td>PV3SCIE</td>
      <td>Plausible value 3 in science</td>
    </tr>
    <tr>
      <th>549</th>
      <td>PV4SCIE</td>
      <td>Plausible value 4 in science</td>
    </tr>
    <tr>
      <th>550</th>
      <td>PV5SCIE</td>
      <td>Plausible value 5 in science</td>
    </tr>
    <tr>
      <th>551</th>
      <td>W_FSTUWT</td>
      <td>FINAL STUDENT WEIGHT</td>
    </tr>
    <tr>
      <th>552</th>
      <td>W_FSTR1</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT1</td>
    </tr>
    <tr>
      <th>553</th>
      <td>W_FSTR2</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT2</td>
    </tr>
    <tr>
      <th>554</th>
      <td>W_FSTR3</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT3</td>
    </tr>
    <tr>
      <th>555</th>
      <td>W_FSTR4</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT4</td>
    </tr>
    <tr>
      <th>556</th>
      <td>W_FSTR5</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT5</td>
    </tr>
    <tr>
      <th>557</th>
      <td>W_FSTR6</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT6</td>
    </tr>
    <tr>
      <th>558</th>
      <td>W_FSTR7</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT7</td>
    </tr>
    <tr>
      <th>559</th>
      <td>W_FSTR8</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT8</td>
    </tr>
    <tr>
      <th>560</th>
      <td>W_FSTR9</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT9</td>
    </tr>
    <tr>
      <th>561</th>
      <td>W_FSTR10</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT10</td>
    </tr>
    <tr>
      <th>562</th>
      <td>W_FSTR11</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT11</td>
    </tr>
    <tr>
      <th>563</th>
      <td>W_FSTR12</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT12</td>
    </tr>
    <tr>
      <th>564</th>
      <td>W_FSTR13</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT13</td>
    </tr>
    <tr>
      <th>565</th>
      <td>W_FSTR14</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT14</td>
    </tr>
    <tr>
      <th>566</th>
      <td>W_FSTR15</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT15</td>
    </tr>
    <tr>
      <th>567</th>
      <td>W_FSTR16</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT16</td>
    </tr>
    <tr>
      <th>568</th>
      <td>W_FSTR17</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT17</td>
    </tr>
    <tr>
      <th>569</th>
      <td>W_FSTR18</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT18</td>
    </tr>
    <tr>
      <th>570</th>
      <td>W_FSTR19</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT19</td>
    </tr>
    <tr>
      <th>571</th>
      <td>W_FSTR20</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT20</td>
    </tr>
    <tr>
      <th>572</th>
      <td>W_FSTR21</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT21</td>
    </tr>
    <tr>
      <th>573</th>
      <td>W_FSTR22</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT22</td>
    </tr>
    <tr>
      <th>574</th>
      <td>W_FSTR23</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT23</td>
    </tr>
    <tr>
      <th>575</th>
      <td>W_FSTR24</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT24</td>
    </tr>
    <tr>
      <th>576</th>
      <td>W_FSTR25</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT25</td>
    </tr>
    <tr>
      <th>577</th>
      <td>W_FSTR26</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT26</td>
    </tr>
    <tr>
      <th>578</th>
      <td>W_FSTR27</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT27</td>
    </tr>
    <tr>
      <th>579</th>
      <td>W_FSTR28</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT28</td>
    </tr>
    <tr>
      <th>580</th>
      <td>W_FSTR29</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT29</td>
    </tr>
    <tr>
      <th>581</th>
      <td>W_FSTR30</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT30</td>
    </tr>
    <tr>
      <th>582</th>
      <td>W_FSTR31</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT31</td>
    </tr>
    <tr>
      <th>583</th>
      <td>W_FSTR32</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT32</td>
    </tr>
    <tr>
      <th>584</th>
      <td>W_FSTR33</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT33</td>
    </tr>
    <tr>
      <th>585</th>
      <td>W_FSTR34</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT34</td>
    </tr>
    <tr>
      <th>586</th>
      <td>W_FSTR35</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT35</td>
    </tr>
    <tr>
      <th>587</th>
      <td>W_FSTR36</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT36</td>
    </tr>
    <tr>
      <th>588</th>
      <td>W_FSTR37</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT37</td>
    </tr>
    <tr>
      <th>589</th>
      <td>W_FSTR38</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT38</td>
    </tr>
    <tr>
      <th>590</th>
      <td>W_FSTR39</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT39</td>
    </tr>
    <tr>
      <th>591</th>
      <td>W_FSTR40</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT40</td>
    </tr>
    <tr>
      <th>592</th>
      <td>W_FSTR41</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT41</td>
    </tr>
    <tr>
      <th>593</th>
      <td>W_FSTR42</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT42</td>
    </tr>
    <tr>
      <th>594</th>
      <td>W_FSTR43</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT43</td>
    </tr>
    <tr>
      <th>595</th>
      <td>W_FSTR44</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT44</td>
    </tr>
    <tr>
      <th>596</th>
      <td>W_FSTR45</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT45</td>
    </tr>
    <tr>
      <th>597</th>
      <td>W_FSTR46</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT46</td>
    </tr>
    <tr>
      <th>598</th>
      <td>W_FSTR47</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT47</td>
    </tr>
    <tr>
      <th>599</th>
      <td>W_FSTR48</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT48</td>
    </tr>
    <tr>
      <th>600</th>
      <td>W_FSTR49</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT49</td>
    </tr>
    <tr>
      <th>601</th>
      <td>W_FSTR50</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT50</td>
    </tr>
    <tr>
      <th>602</th>
      <td>W_FSTR51</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT51</td>
    </tr>
    <tr>
      <th>603</th>
      <td>W_FSTR52</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT52</td>
    </tr>
    <tr>
      <th>604</th>
      <td>W_FSTR53</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT53</td>
    </tr>
    <tr>
      <th>605</th>
      <td>W_FSTR54</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT54</td>
    </tr>
    <tr>
      <th>606</th>
      <td>W_FSTR55</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT55</td>
    </tr>
    <tr>
      <th>607</th>
      <td>W_FSTR56</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT56</td>
    </tr>
    <tr>
      <th>608</th>
      <td>W_FSTR57</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT57</td>
    </tr>
    <tr>
      <th>609</th>
      <td>W_FSTR58</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT58</td>
    </tr>
    <tr>
      <th>610</th>
      <td>W_FSTR59</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT59</td>
    </tr>
    <tr>
      <th>611</th>
      <td>W_FSTR60</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT60</td>
    </tr>
    <tr>
      <th>612</th>
      <td>W_FSTR61</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT61</td>
    </tr>
    <tr>
      <th>613</th>
      <td>W_FSTR62</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT62</td>
    </tr>
    <tr>
      <th>614</th>
      <td>W_FSTR63</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT63</td>
    </tr>
    <tr>
      <th>615</th>
      <td>W_FSTR64</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT64</td>
    </tr>
    <tr>
      <th>616</th>
      <td>W_FSTR65</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT65</td>
    </tr>
    <tr>
      <th>617</th>
      <td>W_FSTR66</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT66</td>
    </tr>
    <tr>
      <th>618</th>
      <td>W_FSTR67</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT67</td>
    </tr>
    <tr>
      <th>619</th>
      <td>W_FSTR68</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT68</td>
    </tr>
    <tr>
      <th>620</th>
      <td>W_FSTR69</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT69</td>
    </tr>
    <tr>
      <th>621</th>
      <td>W_FSTR70</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT70</td>
    </tr>
    <tr>
      <th>622</th>
      <td>W_FSTR71</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT71</td>
    </tr>
    <tr>
      <th>623</th>
      <td>W_FSTR72</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT72</td>
    </tr>
    <tr>
      <th>624</th>
      <td>W_FSTR73</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT73</td>
    </tr>
    <tr>
      <th>625</th>
      <td>W_FSTR74</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT74</td>
    </tr>
    <tr>
      <th>626</th>
      <td>W_FSTR75</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT75</td>
    </tr>
    <tr>
      <th>627</th>
      <td>W_FSTR76</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT76</td>
    </tr>
    <tr>
      <th>628</th>
      <td>W_FSTR77</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT77</td>
    </tr>
    <tr>
      <th>629</th>
      <td>W_FSTR78</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT78</td>
    </tr>
    <tr>
      <th>630</th>
      <td>W_FSTR79</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT79</td>
    </tr>
    <tr>
      <th>631</th>
      <td>W_FSTR80</td>
      <td>FINAL STUDENT REPLICATE BRR-FAY WEIGHT80</td>
    </tr>
    <tr>
      <th>632</th>
      <td>WVARSTRR</td>
      <td>RANDOMIZED FINAL VARIANCE STRATUM (1-80)</td>
    </tr>
    <tr>
      <th>633</th>
      <td>VAR_UNIT</td>
      <td>RANDOMLY ASSIGNED VARIANCE UNIT</td>
    </tr>
    <tr>
      <th>634</th>
      <td>SENWGT_STU</td>
      <td>Senate weight - sum of weight within the country is 1000</td>
    </tr>
    <tr>
      <th>635</th>
      <td>VER_STU</td>
      <td>Date of the database creation</td>
    </tr>
  </tbody>
</table>
</div>



There are a lot of columns. After I have decided what questions this project will answer, the redundant columns will be removed.  
It is visible that there are 3 major grading areas, math, reading and science. It appears that math has a higher weighting as there are subscales where the students were deeper tested. To keep the analysis even, only the main areas will be used. All subscales of math will be neglected.


```python
# A count of each country, how many students participated
pisa.groupby('NC').count()['CNT'].sort_values(ascending=False)
```




    NC
    Mexico                             33806
    Italy                              31073
    Spain                              25313
    Canada                             21544
    Brazil                             19204
    Australia                          14481
    United Arab Emirates               11500
    Switzerland                        11229
    Qatar                              10966
    United States of America           10294
    United Kingdom (excl.Scotland)     9714 
    Colombia                           9073 
    Finland                            8829 
    Belgium                            8597 
    Denmark                            7481 
    Jordan                             7038 
    Chile                              6856 
    Thailand                           6606 
    Japan                              6351 
    Chinese Taipei                     6046 
    Peru                               6035 
    Slovenia                           5911 
    Argentina                          5908 
    Kazakhstan                         5808 
    Portugal                           5722 
    Indonesia                          5622 
    Singapore                          5546 
    Macao-China                        5335 
    Czech Republic                     5327 
    Uruguay                            5315 
    Bulgaria                           5282 
    Luxembourg                         5258 
    Russian Federation                 5231 
    Malaysia                           5197 
    China (Shanghai)                   5177 
    Greece                             5125 
    Romania                            5074 
    Israel                             5055 
    Republic of Korea                  5033 
    Ireland                            5016 
    Croatia                            5008 
    Germany                            5001 
    Viet Nam                           4959 
    Turkey                             4848 
    Hungary                            4810 
    Estonia                            4779 
    Austria                            4755 
    Montenegro                         4744 
    Albania                            4743 
    Sweden                             4736 
    Norway                             4686 
    Serbia                             4684 
    Slovak Republic                    4678 
    Hong Kong-China                    4670 
    Lithuania                          4618 
    France                             4613 
    Poland                             4607 
    Costa Rica                         4602 
    Netherlands                        4460 
    Tunisia                            4407 
    Latvia                             4306 
    New Zealand                        4291 
    Iceland                            3508 
    United Kingdom (Scotland)          2945 
    Perm (Russian Federation)          1761 
    Liechtenstein                      293  
    Name: CNT, dtype: int64



Mexico has the highest amount of participating students with a total of 33806 students while the lowest participation is from Liechtenstein with 293 students.
But comparing the population of both countries these numbers can not be put in relation.
Liechtenstein has a population of around 38000 and Mexico 124 million. Both were estimated in 2017 according to wikipedia.


```python
# Displays proportion of male/female students
pisa.groupby('ST04Q01').count()['CNT'].sort_values(ascending=False)
```




    ST04Q01
    Female    245064
    Male      240426
    Name: CNT, dtype: int64



The dataset is healthy balanced with a ration of 1.019/1 on each male student. The female students are slighty more represented in the dataset.

## Questions
- Q1: Are there differences between students in grades that skip school or not?
- Q2: In what countries do students skip the most often?
- Q3: By comparing the country with the highest frequency and the lowest frequency of skipping school are there some visible differences in a plot by comparing them?

### What is/are the main feature(s) of interest in your dataset?
I'm most interested in figuring out what features are best for finding strong patterns for grade performance of the students in the dataset.  

### What features in the dataset do you think will help support your investigation into your feature(s) of interest?  
By overflying the dataset columns with the pisa_dict dataset I have choosen a couple of features that are interesting for my analysis.  
I expect that for example these features will have a strong effect on the output:
- Age
- Gender
- Country
- Possessions
- Wealth
- Education of parents


## Data Cleaning

### Copy datasets

##### Define
First, a copy of the two datasets will be made, before the actual data cleaning happens.  
##### Code


```python
# Copies of original datasets are asigned to new dataframes
pisa_clean = pisa.copy()
pisa_dict_clean = pisa_dict.copy()
```

##### Test


```python
pisa_clean.info()
print('=====================================================')
pisa_dict_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 485490 entries, 0 to 485489
    Columns: 636 entries, Unnamed: 0 to VER_STU
    dtypes: float64(250), int64(18), object(368)
    memory usage: 2.3+ GB
    =====================================================
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 636 entries, 0 to 635
    Data columns (total 2 columns):
    ColName       635 non-null object
    Definition    636 non-null object
    dtypes: object(2)
    memory usage: 10.0+ KB
    

### Filter for desired columns

##### Define
With these features I am going to investigate the dataset.  
##### Code


```python
# Columns with relevance in this project
col_names = ['CNT','SCHOOLID','STIDSTD','ST01Q01','ST03Q01'
             ,'ST03Q02','ST04Q01','ST08Q01','ST11Q01'
             ,'ST11Q02','ST20Q01','ST20Q02','ST20Q03'
             ,'ST25Q01','ST26Q02','ST26Q04','ST26Q06'
             ,'PV1MATH','PV2MATH','PV3MATH','PV4MATH','PV5MATH'
             ,'PV1READ','PV2READ','PV3READ','PV4READ','PV5READ'
             ,'PV1SCIE','PV2SCIE','PV3SCIE','PV4SCIE','PV5SCIE']
pisa_clean = pisa_clean[col_names]
```

#### Test


```python
# Check new dataset
pisa_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 485490 entries, 0 to 485489
    Data columns (total 32 columns):
    CNT         485490 non-null object
    SCHOOLID    485490 non-null int64
    STIDSTD     485490 non-null int64
    ST01Q01     485490 non-null int64
    ST03Q01     485490 non-null int64
    ST03Q02     485490 non-null int64
    ST04Q01     485490 non-null object
    ST08Q01     479143 non-null object
    ST11Q01     460559 non-null object
    ST11Q02     441036 non-null object
    ST20Q01     476363 non-null object
    ST20Q02     472518 non-null object
    ST20Q03     469141 non-null object
    ST25Q01     465496 non-null object
    ST26Q02     469693 non-null object
    ST26Q04     473877 non-null object
    ST26Q06     473182 non-null object
    PV1MATH     485490 non-null float64
    PV2MATH     485490 non-null float64
    PV3MATH     485490 non-null float64
    PV4MATH     485490 non-null float64
    PV5MATH     485490 non-null float64
    PV1READ     485490 non-null float64
    PV2READ     485490 non-null float64
    PV3READ     485490 non-null float64
    PV4READ     485490 non-null float64
    PV5READ     485490 non-null float64
    PV1SCIE     485490 non-null float64
    PV2SCIE     485490 non-null float64
    PV3SCIE     485490 non-null float64
    PV4SCIE     485490 non-null float64
    PV5SCIE     485490 non-null float64
    dtypes: float64(15), int64(5), object(12)
    memory usage: 118.5+ MB
    

### Tidiness of dataset

##### Define
To keep the columns tidy, the 5 grades of each study area will be merged together.
Therefore, the mean of each area will be calucated.  
This will cut down the size of the columns from 32 to 20.
##### Code


```python
# Mean of math calculated
pisa_clean['MATH'] = pisa_clean[['PV1MATH','PV2MATH','PV3MATH','PV4MATH','PV5MATH']].mean(axis=1)
# Mean of reading calculated
pisa_clean['READ'] = pisa_clean[['PV1READ','PV2READ','PV3READ','PV4READ','PV5READ']].mean(axis=1)
# Mean of science calculated
pisa_clean['SCIENCE'] = pisa_clean[['PV1SCIE','PV2SCIE','PV3SCIE','PV4SCIE','PV5SCIE']].mean(axis=1)
```

##### Test


```python
# check new columns
pisa_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 485490 entries, 0 to 485489
    Data columns (total 35 columns):
    CNT         485490 non-null object
    SCHOOLID    485490 non-null int64
    STIDSTD     485490 non-null int64
    ST01Q01     485490 non-null int64
    ST03Q01     485490 non-null int64
    ST03Q02     485490 non-null int64
    ST04Q01     485490 non-null object
    ST08Q01     479143 non-null object
    ST11Q01     460559 non-null object
    ST11Q02     441036 non-null object
    ST20Q01     476363 non-null object
    ST20Q02     472518 non-null object
    ST20Q03     469141 non-null object
    ST25Q01     465496 non-null object
    ST26Q02     469693 non-null object
    ST26Q04     473877 non-null object
    ST26Q06     473182 non-null object
    PV1MATH     485490 non-null float64
    PV2MATH     485490 non-null float64
    PV3MATH     485490 non-null float64
    PV4MATH     485490 non-null float64
    PV5MATH     485490 non-null float64
    PV1READ     485490 non-null float64
    PV2READ     485490 non-null float64
    PV3READ     485490 non-null float64
    PV4READ     485490 non-null float64
    PV5READ     485490 non-null float64
    PV1SCIE     485490 non-null float64
    PV2SCIE     485490 non-null float64
    PV3SCIE     485490 non-null float64
    PV4SCIE     485490 non-null float64
    PV5SCIE     485490 non-null float64
    MATH        485490 non-null float64
    READ        485490 non-null float64
    SCIENCE     485490 non-null float64
    dtypes: float64(18), int64(5), object(12)
    memory usage: 129.6+ MB
    


```python
pisa_clean.head()
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
      <th>CNT</th>
      <th>SCHOOLID</th>
      <th>STIDSTD</th>
      <th>ST01Q01</th>
      <th>ST03Q01</th>
      <th>ST03Q02</th>
      <th>ST04Q01</th>
      <th>ST08Q01</th>
      <th>ST11Q01</th>
      <th>ST11Q02</th>
      <th>ST20Q01</th>
      <th>ST20Q02</th>
      <th>ST20Q03</th>
      <th>ST25Q01</th>
      <th>ST26Q02</th>
      <th>ST26Q04</th>
      <th>ST26Q06</th>
      <th>PV1MATH</th>
      <th>PV2MATH</th>
      <th>PV3MATH</th>
      <th>PV4MATH</th>
      <th>PV5MATH</th>
      <th>PV1READ</th>
      <th>PV2READ</th>
      <th>PV3READ</th>
      <th>PV4READ</th>
      <th>PV5READ</th>
      <th>PV1SCIE</th>
      <th>PV2SCIE</th>
      <th>PV3SCIE</th>
      <th>PV4SCIE</th>
      <th>PV5SCIE</th>
      <th>MATH</th>
      <th>READ</th>
      <th>SCIENCE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Albania</td>
      <td>1</td>
      <td>1</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>406.8469</td>
      <td>376.4683</td>
      <td>344.5319</td>
      <td>321.1637</td>
      <td>381.9209</td>
      <td>249.5762</td>
      <td>254.3420</td>
      <td>406.8496</td>
      <td>175.7053</td>
      <td>218.5981</td>
      <td>341.7009</td>
      <td>408.8400</td>
      <td>348.2283</td>
      <td>367.8105</td>
      <td>392.9877</td>
      <td>366.18634</td>
      <td>261.01424</td>
      <td>371.91348</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>1</td>
      <td>2</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>486.1427</td>
      <td>464.3325</td>
      <td>453.4273</td>
      <td>472.9008</td>
      <td>476.0165</td>
      <td>406.2936</td>
      <td>349.8975</td>
      <td>400.7334</td>
      <td>369.7553</td>
      <td>396.7618</td>
      <td>548.9929</td>
      <td>471.5964</td>
      <td>471.5964</td>
      <td>443.6218</td>
      <td>454.8116</td>
      <td>470.56396</td>
      <td>384.68832</td>
      <td>478.12382</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>1</td>
      <td>3</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>533.2684</td>
      <td>481.0796</td>
      <td>489.6479</td>
      <td>490.4269</td>
      <td>533.2684</td>
      <td>401.2100</td>
      <td>404.3872</td>
      <td>387.7067</td>
      <td>431.3938</td>
      <td>401.2100</td>
      <td>499.6643</td>
      <td>428.7952</td>
      <td>492.2044</td>
      <td>512.7191</td>
      <td>499.6643</td>
      <td>505.53824</td>
      <td>405.18154</td>
      <td>486.60946</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>1</td>
      <td>4</td>
      <td>9</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>412.2215</td>
      <td>498.6836</td>
      <td>415.3373</td>
      <td>466.7472</td>
      <td>454.2842</td>
      <td>547.3630</td>
      <td>481.4353</td>
      <td>461.5776</td>
      <td>425.0393</td>
      <td>471.9036</td>
      <td>438.6796</td>
      <td>481.5740</td>
      <td>448.9370</td>
      <td>474.1141</td>
      <td>426.5573</td>
      <td>449.45476</td>
      <td>477.46376</td>
      <td>453.97240</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Albania</td>
      <td>1</td>
      <td>5</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>381.9209</td>
      <td>328.1742</td>
      <td>403.7311</td>
      <td>418.5309</td>
      <td>395.1628</td>
      <td>311.7707</td>
      <td>141.7883</td>
      <td>293.5015</td>
      <td>272.8495</td>
      <td>260.1405</td>
      <td>361.5628</td>
      <td>275.7740</td>
      <td>372.7527</td>
      <td>403.5248</td>
      <td>422.1746</td>
      <td>385.50398</td>
      <td>256.01010</td>
      <td>367.15778</td>
    </tr>
  </tbody>
</table>
</div>



##### Define
Next the redundant grading columns can be dropped.
##### Code


```python
# drop columns
pisa_clean.drop(['PV1MATH','PV2MATH','PV3MATH','PV4MATH','PV5MATH',
                 'PV1READ','PV2READ','PV3READ','PV4READ','PV5READ',
                 'PV1SCIE','PV2SCIE','PV3SCIE','PV4SCIE','PV5SCIE'], 1, inplace=True)
```

##### Test


```python
# check for altered dataset shape
pisa_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 485490 entries, 0 to 485489
    Data columns (total 20 columns):
    CNT         485490 non-null object
    SCHOOLID    485490 non-null int64
    STIDSTD     485490 non-null int64
    ST01Q01     485490 non-null int64
    ST03Q01     485490 non-null int64
    ST03Q02     485490 non-null int64
    ST04Q01     485490 non-null object
    ST08Q01     479143 non-null object
    ST11Q01     460559 non-null object
    ST11Q02     441036 non-null object
    ST20Q01     476363 non-null object
    ST20Q02     472518 non-null object
    ST20Q03     469141 non-null object
    ST25Q01     465496 non-null object
    ST26Q02     469693 non-null object
    ST26Q04     473877 non-null object
    ST26Q06     473182 non-null object
    MATH        485490 non-null float64
    READ        485490 non-null float64
    SCIENCE     485490 non-null float64
    dtypes: float64(3), int64(5), object(12)
    memory usage: 74.1+ MB
    

### Change column names

##### Define
At the moment, the column names do not have a human readable description. Therefore, the names will be changed into a more appropriate naming.
##### Code


```python
pisa_clean.sample(5)
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
      <th>CNT</th>
      <th>SCHOOLID</th>
      <th>STIDSTD</th>
      <th>ST01Q01</th>
      <th>ST03Q01</th>
      <th>ST03Q02</th>
      <th>ST04Q01</th>
      <th>ST08Q01</th>
      <th>ST11Q01</th>
      <th>ST11Q02</th>
      <th>ST20Q01</th>
      <th>ST20Q02</th>
      <th>ST20Q03</th>
      <th>ST25Q01</th>
      <th>ST26Q02</th>
      <th>ST26Q04</th>
      <th>ST26Q06</th>
      <th>MATH</th>
      <th>READ</th>
      <th>SCIENCE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>323194</th>
      <td>Mexico</td>
      <td>333</td>
      <td>7492</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>402.48482</td>
      <td>397.74650</td>
      <td>390.93624</td>
    </tr>
    <tr>
      <th>42989</th>
      <td>Belgium</td>
      <td>59</td>
      <td>1603</td>
      <td>9</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>Three or four times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Other country</td>
      <td>Other country</td>
      <td>Other country</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>409.65102</td>
      <td>464.27820</td>
      <td>434.11040</td>
    </tr>
    <tr>
      <th>285359</th>
      <td>Kazakhstan</td>
      <td>12</td>
      <td>308</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>537.16312</td>
      <td>468.01146</td>
      <td>473.92764</td>
    </tr>
    <tr>
      <th>406253</th>
      <td>Perm(Russian Federation)</td>
      <td>30</td>
      <td>860</td>
      <td>9</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>570.65742</td>
      <td>556.49762</td>
      <td>558.50428</td>
    </tr>
    <tr>
      <th>446089</th>
      <td>Sweden</td>
      <td>112</td>
      <td>2495</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>522.83064</td>
      <td>531.55628</td>
      <td>486.32974</td>
    </tr>
  </tbody>
</table>
</div>




```python
# renaming the columns
pisa_clean.columns = ['COUNTRY','SCHOOL_ID','STUDENT_ID','INT_GRADE'
                     ,'BIRTH_MONTH','BIRTH_YEAR','GENDER','SKIPPED_SCHOOL'
                     ,'At_HOME_MOTHER','AT_HOME_FATHER','CNT_OF_BIRTH_SELF'
                     ,'CNT_OF_BIRTH_MOTHER','CNT_OF_BIRTH_FATHER'
                     ,'INT_LANG_AT_HOME','POS_OWN_ROOM','POS_OWN_COMP','POS_INTERNET'
                     ,'MATH','READ','SCIENCE']
```

##### Test


```python
# check for changes
pisa_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 485490 entries, 0 to 485489
    Data columns (total 20 columns):
    COUNTRY                485490 non-null object
    SCHOOL_ID              485490 non-null int64
    STUDENT_ID             485490 non-null int64
    INT_GRADE              485490 non-null int64
    BIRTH_MONTH            485490 non-null int64
    BIRTH_YEAR             485490 non-null int64
    GENDER                 485490 non-null object
    SKIPPED_SCHOOL         479143 non-null object
    At_HOME_MOTHER         460559 non-null object
    AT_HOME_FATHER         441036 non-null object
    CNT_OF_BIRTH_SELF      476363 non-null object
    CNT_OF_BIRTH_MOTHER    472518 non-null object
    CNT_OF_BIRTH_FATHER    469141 non-null object
    INT_LANG_AT_HOME       465496 non-null object
    POS_OWN_ROOM           469693 non-null object
    POS_OWN_COMP           473877 non-null object
    POS_INTERNET           473182 non-null object
    MATH                   485490 non-null float64
    READ                   485490 non-null float64
    SCIENCE                485490 non-null float64
    dtypes: float64(3), int64(5), object(12)
    memory usage: 74.1+ MB
    

### Add additional column with average overall grade

##### Define
The columns MATH, READ and SCIENCE will be joined as an overall average grade together in a new column.
##### Code


```python
# Calc average of all scores
pisa_clean['AVG_SCORE'] = pisa_clean[['MATH','READ','SCIENCE']].mean(axis=1)
```

##### Test


```python
pisa_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 485490 entries, 0 to 485489
    Data columns (total 21 columns):
    COUNTRY                485490 non-null object
    SCHOOL_ID              485490 non-null int64
    STUDENT_ID             485490 non-null int64
    INT_GRADE              485490 non-null int64
    BIRTH_MONTH            485490 non-null int64
    BIRTH_YEAR             485490 non-null int64
    GENDER                 485490 non-null object
    SKIPPED_SCHOOL         479143 non-null object
    At_HOME_MOTHER         460559 non-null object
    AT_HOME_FATHER         441036 non-null object
    CNT_OF_BIRTH_SELF      476363 non-null object
    CNT_OF_BIRTH_MOTHER    472518 non-null object
    CNT_OF_BIRTH_FATHER    469141 non-null object
    INT_LANG_AT_HOME       465496 non-null object
    POS_OWN_ROOM           469693 non-null object
    POS_OWN_COMP           473877 non-null object
    POS_INTERNET           473182 non-null object
    MATH                   485490 non-null float64
    READ                   485490 non-null float64
    SCIENCE                485490 non-null float64
    AVG_SCORE              485490 non-null float64
    dtypes: float64(4), int64(5), object(12)
    memory usage: 77.8+ MB
    

### Check for NaN in dataset

##### Define
The dataset contains NaN values, check records which have NaN values
##### Code


```python
# Display all records which have NaN
pisa_clean[pisa_clean.isna().any(axis=1)]
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
      <th>COUNTRY</th>
      <th>SCHOOL_ID</th>
      <th>STUDENT_ID</th>
      <th>INT_GRADE</th>
      <th>BIRTH_MONTH</th>
      <th>BIRTH_YEAR</th>
      <th>GENDER</th>
      <th>SKIPPED_SCHOOL</th>
      <th>At_HOME_MOTHER</th>
      <th>AT_HOME_FATHER</th>
      <th>CNT_OF_BIRTH_SELF</th>
      <th>CNT_OF_BIRTH_MOTHER</th>
      <th>CNT_OF_BIRTH_FATHER</th>
      <th>INT_LANG_AT_HOME</th>
      <th>POS_OWN_ROOM</th>
      <th>POS_OWN_COMP</th>
      <th>POS_INTERNET</th>
      <th>MATH</th>
      <th>READ</th>
      <th>SCIENCE</th>
      <th>AVG_SCORE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>Albania</td>
      <td>1</td>
      <td>9</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>408.71634</td>
      <td>326.78312</td>
      <td>371.72698</td>
      <td>369.075480</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Albania</td>
      <td>2</td>
      <td>13</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>231.89750</td>
      <td>178.88258</td>
      <td>194.36778</td>
      <td>201.715953</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Albania</td>
      <td>2</td>
      <td>17</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>245.99622</td>
      <td>188.89090</td>
      <td>225.97912</td>
      <td>220.288747</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Albania</td>
      <td>2</td>
      <td>18</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>527.27062</td>
      <td>558.77706</td>
      <td>500.78328</td>
      <td>528.943653</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Albania</td>
      <td>2</td>
      <td>29</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>364.23900</td>
      <td>323.28816</td>
      <td>289.38830</td>
      <td>325.638487</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Albania</td>
      <td>2</td>
      <td>31</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>490.89422</td>
      <td>569.92146</td>
      <td>538.82878</td>
      <td>533.214820</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Albania</td>
      <td>2</td>
      <td>33</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>424.37294</td>
      <td>489.45784</td>
      <td>511.69340</td>
      <td>475.174727</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Albania</td>
      <td>2</td>
      <td>35</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>395.24070</td>
      <td>350.27134</td>
      <td>405.85604</td>
      <td>383.789360</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Albania</td>
      <td>2</td>
      <td>37</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>494.24366</td>
      <td>484.53312</td>
      <td>505.81872</td>
      <td>494.865167</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Albania</td>
      <td>3</td>
      <td>55</td>
      <td>9</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>381.06404</td>
      <td>396.20584</td>
      <td>427.02350</td>
      <td>401.431127</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Albania</td>
      <td>4</td>
      <td>68</td>
      <td>9</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>415.33728</td>
      <td>325.09026</td>
      <td>398.48936</td>
      <td>379.638967</td>
    </tr>
    <tr>
      <th>91</th>
      <td>Albania</td>
      <td>5</td>
      <td>92</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>424.84032</td>
      <td>405.18154</td>
      <td>388.60500</td>
      <td>406.208953</td>
    </tr>
    <tr>
      <th>93</th>
      <td>Albania</td>
      <td>5</td>
      <td>94</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>257.83610</td>
      <td>233.50814</td>
      <td>335.45318</td>
      <td>275.599140</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Albania</td>
      <td>5</td>
      <td>101</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>443.84640</td>
      <td>398.35046</td>
      <td>425.06528</td>
      <td>422.420713</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Albania</td>
      <td>5</td>
      <td>106</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>504.99300</td>
      <td>441.08436</td>
      <td>489.31370</td>
      <td>478.463687</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Albania</td>
      <td>6</td>
      <td>111</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>329.65416</td>
      <td>332.46816</td>
      <td>324.72960</td>
      <td>328.950640</td>
    </tr>
    <tr>
      <th>117</th>
      <td>Albania</td>
      <td>6</td>
      <td>118</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>525.32326</td>
      <td>597.00742</td>
      <td>611.28312</td>
      <td>577.871267</td>
    </tr>
    <tr>
      <th>129</th>
      <td>Albania</td>
      <td>6</td>
      <td>130</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>263.98974</td>
      <td>335.67940</td>
      <td>250.69006</td>
      <td>283.453067</td>
    </tr>
    <tr>
      <th>134</th>
      <td>Albania</td>
      <td>6</td>
      <td>135</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>396.25330</td>
      <td>477.45984</td>
      <td>390.93622</td>
      <td>421.549787</td>
    </tr>
    <tr>
      <th>136</th>
      <td>Albania</td>
      <td>6</td>
      <td>137</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>480.92380</td>
      <td>630.84504</td>
      <td>483.43900</td>
      <td>531.735947</td>
    </tr>
    <tr>
      <th>138</th>
      <td>Albania</td>
      <td>6</td>
      <td>139</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>360.03272</td>
      <td>327.25554</td>
      <td>392.05520</td>
      <td>359.781153</td>
    </tr>
    <tr>
      <th>143</th>
      <td>Albania</td>
      <td>7</td>
      <td>144</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>277.62112</td>
      <td>169.43274</td>
      <td>267.19508</td>
      <td>238.082980</td>
    </tr>
    <tr>
      <th>148</th>
      <td>Albania</td>
      <td>7</td>
      <td>149</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>419.85514</td>
      <td>375.61282</td>
      <td>453.87914</td>
      <td>416.449033</td>
    </tr>
    <tr>
      <th>149</th>
      <td>Albania</td>
      <td>7</td>
      <td>150</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>356.44962</td>
      <td>368.39530</td>
      <td>380.11936</td>
      <td>368.321427</td>
    </tr>
    <tr>
      <th>160</th>
      <td>Albania</td>
      <td>7</td>
      <td>161</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>130.94718</td>
      <td>56.41088</td>
      <td>137.57926</td>
      <td>108.312440</td>
    </tr>
    <tr>
      <th>163</th>
      <td>Albania</td>
      <td>7</td>
      <td>164</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>506.55088</td>
      <td>343.29442</td>
      <td>514.49086</td>
      <td>454.778720</td>
    </tr>
    <tr>
      <th>168</th>
      <td>Albania</td>
      <td>7</td>
      <td>169</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>401.31640</td>
      <td>280.58230</td>
      <td>387.01976</td>
      <td>356.306153</td>
    </tr>
    <tr>
      <th>177</th>
      <td>Albania</td>
      <td>8</td>
      <td>178</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>285.87786</td>
      <td>266.65384</td>
      <td>257.03098</td>
      <td>269.854227</td>
    </tr>
    <tr>
      <th>179</th>
      <td>Albania</td>
      <td>8</td>
      <td>180</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>415.02572</td>
      <td>385.63712</td>
      <td>448.75046</td>
      <td>416.471100</td>
    </tr>
    <tr>
      <th>180</th>
      <td>Albania</td>
      <td>9</td>
      <td>181</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>452.49262</td>
      <td>482.27150</td>
      <td>454.53190</td>
      <td>463.098673</td>
    </tr>
    <tr>
      <th>191</th>
      <td>Albania</td>
      <td>10</td>
      <td>192</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>439.71804</td>
      <td>427.65906</td>
      <td>445.67324</td>
      <td>437.683447</td>
    </tr>
    <tr>
      <th>193</th>
      <td>Albania</td>
      <td>10</td>
      <td>194</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>498.13834</td>
      <td>438.86028</td>
      <td>493.97614</td>
      <td>476.991587</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Albania</td>
      <td>10</td>
      <td>200</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>Five or more times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>300.13242</td>
      <td>261.57026</td>
      <td>370.32824</td>
      <td>310.676973</td>
    </tr>
    <tr>
      <th>201</th>
      <td>Albania</td>
      <td>10</td>
      <td>202</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>527.50426</td>
      <td>580.40636</td>
      <td>565.77768</td>
      <td>557.896100</td>
    </tr>
    <tr>
      <th>203</th>
      <td>Albania</td>
      <td>10</td>
      <td>204</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>461.29458</td>
      <td>416.75262</td>
      <td>477.09808</td>
      <td>451.715093</td>
    </tr>
    <tr>
      <th>220</th>
      <td>Albania</td>
      <td>11</td>
      <td>221</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>541.52516</td>
      <td>630.95212</td>
      <td>588.15740</td>
      <td>586.878227</td>
    </tr>
    <tr>
      <th>227</th>
      <td>Albania</td>
      <td>11</td>
      <td>228</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>409.65104</td>
      <td>471.76604</td>
      <td>413.22270</td>
      <td>431.546593</td>
    </tr>
    <tr>
      <th>231</th>
      <td>Albania</td>
      <td>11</td>
      <td>232</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>459.03568</td>
      <td>472.53902</td>
      <td>450.70870</td>
      <td>460.761133</td>
    </tr>
    <tr>
      <th>238</th>
      <td>Albania</td>
      <td>12</td>
      <td>239</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>279.41266</td>
      <td>267.51062</td>
      <td>295.44944</td>
      <td>280.790907</td>
    </tr>
    <tr>
      <th>244</th>
      <td>Albania</td>
      <td>12</td>
      <td>245</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>393.37124</td>
      <td>448.15372</td>
      <td>382.63708</td>
      <td>408.054013</td>
    </tr>
    <tr>
      <th>245</th>
      <td>Albania</td>
      <td>12</td>
      <td>246</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>454.05048</td>
      <td>527.42586</td>
      <td>508.42968</td>
      <td>496.635340</td>
    </tr>
    <tr>
      <th>247</th>
      <td>Albania</td>
      <td>12</td>
      <td>248</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>415.25938</td>
      <td>364.78656</td>
      <td>429.26148</td>
      <td>403.102473</td>
    </tr>
    <tr>
      <th>248</th>
      <td>Albania</td>
      <td>12</td>
      <td>249</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>420.16670</td>
      <td>434.07462</td>
      <td>417.04588</td>
      <td>423.762400</td>
    </tr>
    <tr>
      <th>252</th>
      <td>Albania</td>
      <td>12</td>
      <td>253</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>399.21326</td>
      <td>320.51920</td>
      <td>373.87170</td>
      <td>364.534720</td>
    </tr>
    <tr>
      <th>263</th>
      <td>Albania</td>
      <td>12</td>
      <td>264</td>
      <td>9</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>301.76818</td>
      <td>278.73786</td>
      <td>306.54606</td>
      <td>295.684033</td>
    </tr>
    <tr>
      <th>265</th>
      <td>Albania</td>
      <td>13</td>
      <td>266</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>440.88644</td>
      <td>389.13648</td>
      <td>401.00710</td>
      <td>410.343340</td>
    </tr>
    <tr>
      <th>267</th>
      <td>Albania</td>
      <td>13</td>
      <td>268</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>530.62002</td>
      <td>603.04420</td>
      <td>563.72622</td>
      <td>565.796813</td>
    </tr>
    <tr>
      <th>271</th>
      <td>Albania</td>
      <td>13</td>
      <td>272</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>491.12790</td>
      <td>544.02696</td>
      <td>482.59978</td>
      <td>505.918213</td>
    </tr>
    <tr>
      <th>272</th>
      <td>Albania</td>
      <td>13</td>
      <td>273</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>429.98132</td>
      <td>503.59656</td>
      <td>526.05374</td>
      <td>486.543873</td>
    </tr>
    <tr>
      <th>276</th>
      <td>Albania</td>
      <td>13</td>
      <td>277</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>419.62142</td>
      <td>286.35272</td>
      <td>402.40582</td>
      <td>369.459987</td>
    </tr>
    <tr>
      <th>278</th>
      <td>Albania</td>
      <td>13</td>
      <td>279</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>460.20408</td>
      <td>503.59654</td>
      <td>517.84780</td>
      <td>493.882807</td>
    </tr>
    <tr>
      <th>282</th>
      <td>Albania</td>
      <td>13</td>
      <td>283</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>361.12324</td>
      <td>343.54306</td>
      <td>421.61508</td>
      <td>375.427127</td>
    </tr>
    <tr>
      <th>284</th>
      <td>Albania</td>
      <td>13</td>
      <td>285</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>444.85900</td>
      <td>491.44362</td>
      <td>500.31706</td>
      <td>478.873227</td>
    </tr>
    <tr>
      <th>287</th>
      <td>Albania</td>
      <td>14</td>
      <td>288</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>463.00826</td>
      <td>407.48502</td>
      <td>397.09064</td>
      <td>422.527973</td>
    </tr>
    <tr>
      <th>295</th>
      <td>Albania</td>
      <td>14</td>
      <td>296</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>348.73814</td>
      <td>332.06720</td>
      <td>292.55876</td>
      <td>324.454700</td>
    </tr>
    <tr>
      <th>320</th>
      <td>Albania</td>
      <td>16</td>
      <td>321</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>410.58576</td>
      <td>478.57578</td>
      <td>446.60574</td>
      <td>445.255760</td>
    </tr>
    <tr>
      <th>322</th>
      <td>Albania</td>
      <td>16</td>
      <td>323</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>355.04752</td>
      <td>335.75882</td>
      <td>344.87132</td>
      <td>345.225887</td>
    </tr>
    <tr>
      <th>329</th>
      <td>Albania</td>
      <td>16</td>
      <td>330</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>362.21374</td>
      <td>411.21918</td>
      <td>376.10968</td>
      <td>383.180867</td>
    </tr>
    <tr>
      <th>331</th>
      <td>Albania</td>
      <td>16</td>
      <td>332</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>446.26110</td>
      <td>553.56442</td>
      <td>444.92728</td>
      <td>481.584267</td>
    </tr>
    <tr>
      <th>334</th>
      <td>Albania</td>
      <td>16</td>
      <td>335</td>
      <td>9</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>Other country</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>445.56006</td>
      <td>486.12086</td>
      <td>489.68668</td>
      <td>473.789200</td>
    </tr>
    <tr>
      <th>335</th>
      <td>Albania</td>
      <td>16</td>
      <td>336</td>
      <td>9</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>476.63968</td>
      <td>530.14762</td>
      <td>458.91460</td>
      <td>488.567300</td>
    </tr>
    <tr>
      <th>338</th>
      <td>Albania</td>
      <td>16</td>
      <td>339</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>318.28168</td>
      <td>360.93722</td>
      <td>332.00300</td>
      <td>337.073967</td>
    </tr>
    <tr>
      <th>339</th>
      <td>Albania</td>
      <td>16</td>
      <td>340</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>350.52968</td>
      <td>372.72580</td>
      <td>350.27972</td>
      <td>357.845067</td>
    </tr>
    <tr>
      <th>347</th>
      <td>Albania</td>
      <td>17</td>
      <td>348</td>
      <td>8</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>299.97664</td>
      <td>201.10954</td>
      <td>291.71952</td>
      <td>264.268567</td>
    </tr>
    <tr>
      <th>349</th>
      <td>Albania</td>
      <td>17</td>
      <td>350</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>383.86818</td>
      <td>295.96388</td>
      <td>440.45134</td>
      <td>373.427800</td>
    </tr>
    <tr>
      <th>353</th>
      <td>Albania</td>
      <td>17</td>
      <td>354</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>503.98038</td>
      <td>441.71980</td>
      <td>586.19918</td>
      <td>510.633120</td>
    </tr>
    <tr>
      <th>356</th>
      <td>Albania</td>
      <td>17</td>
      <td>357</td>
      <td>9</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>431.30550</td>
      <td>341.55728</td>
      <td>454.53188</td>
      <td>409.131553</td>
    </tr>
    <tr>
      <th>357</th>
      <td>Albania</td>
      <td>17</td>
      <td>358</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>333.86042</td>
      <td>362.92424</td>
      <td>511.78666</td>
      <td>402.857107</td>
    </tr>
    <tr>
      <th>361</th>
      <td>Albania</td>
      <td>17</td>
      <td>362</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>393.60492</td>
      <td>350.99310</td>
      <td>400.72734</td>
      <td>381.775120</td>
    </tr>
    <tr>
      <th>389</th>
      <td>Albania</td>
      <td>18</td>
      <td>390</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>413.54570</td>
      <td>425.83360</td>
      <td>398.30286</td>
      <td>412.560720</td>
    </tr>
    <tr>
      <th>394</th>
      <td>Albania</td>
      <td>18</td>
      <td>395</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>516.83284</td>
      <td>517.17926</td>
      <td>487.07572</td>
      <td>507.029273</td>
    </tr>
    <tr>
      <th>396</th>
      <td>Albania</td>
      <td>18</td>
      <td>397</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>305.11760</td>
      <td>370.56056</td>
      <td>289.20178</td>
      <td>321.626647</td>
    </tr>
    <tr>
      <th>397</th>
      <td>Albania</td>
      <td>18</td>
      <td>398</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>497.35940</td>
      <td>508.68014</td>
      <td>467.40024</td>
      <td>491.146593</td>
    </tr>
    <tr>
      <th>404</th>
      <td>Albania</td>
      <td>18</td>
      <td>405</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>375.14410</td>
      <td>392.13288</td>
      <td>392.98768</td>
      <td>386.754887</td>
    </tr>
    <tr>
      <th>415</th>
      <td>Albania</td>
      <td>20</td>
      <td>416</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>Three or four times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>519.63702</td>
      <td>563.96412</td>
      <td>529.13092</td>
      <td>537.577353</td>
    </tr>
    <tr>
      <th>419</th>
      <td>Albania</td>
      <td>20</td>
      <td>420</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>247.24254</td>
      <td>327.17534</td>
      <td>344.21858</td>
      <td>306.212153</td>
    </tr>
    <tr>
      <th>421</th>
      <td>Albania</td>
      <td>20</td>
      <td>422</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>405.60056</td>
      <td>452.76072</td>
      <td>417.41886</td>
      <td>425.260047</td>
    </tr>
    <tr>
      <th>423</th>
      <td>Albania</td>
      <td>20</td>
      <td>424</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>215.92928</td>
      <td>338.72334</td>
      <td>376.66916</td>
      <td>310.440593</td>
    </tr>
    <tr>
      <th>424</th>
      <td>Albania</td>
      <td>20</td>
      <td>425</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>332.61412</td>
      <td>407.20948</td>
      <td>434.76314</td>
      <td>391.528913</td>
    </tr>
    <tr>
      <th>427</th>
      <td>Albania</td>
      <td>20</td>
      <td>428</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>380.36298</td>
      <td>393.02858</td>
      <td>445.95300</td>
      <td>406.448187</td>
    </tr>
    <tr>
      <th>433</th>
      <td>Albania</td>
      <td>20</td>
      <td>434</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>256.27822</td>
      <td>318.03314</td>
      <td>370.32822</td>
      <td>314.879860</td>
    </tr>
    <tr>
      <th>449</th>
      <td>Albania</td>
      <td>21</td>
      <td>450</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>285.48840</td>
      <td>230.22014</td>
      <td>288.45580</td>
      <td>268.054780</td>
    </tr>
    <tr>
      <th>450</th>
      <td>Albania</td>
      <td>21</td>
      <td>451</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>368.75680</td>
      <td>252.59444</td>
      <td>317.92242</td>
      <td>313.091220</td>
    </tr>
    <tr>
      <th>452</th>
      <td>Albania</td>
      <td>21</td>
      <td>453</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>429.59184</td>
      <td>443.37720</td>
      <td>370.88772</td>
      <td>414.618920</td>
    </tr>
    <tr>
      <th>457</th>
      <td>Albania</td>
      <td>21</td>
      <td>458</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>609.83800</td>
      <td>626.06028</td>
      <td>588.53038</td>
      <td>608.142887</td>
    </tr>
    <tr>
      <th>462</th>
      <td>Albania</td>
      <td>21</td>
      <td>463</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>Three or four times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>245.52888</td>
      <td>251.24422</td>
      <td>319.50764</td>
      <td>272.093580</td>
    </tr>
    <tr>
      <th>464</th>
      <td>Albania</td>
      <td>21</td>
      <td>465</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>425.93082</td>
      <td>394.85552</td>
      <td>389.44424</td>
      <td>403.410193</td>
    </tr>
    <tr>
      <th>465</th>
      <td>Albania</td>
      <td>21</td>
      <td>466</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>336.82038</td>
      <td>194.53050</td>
      <td>282.30136</td>
      <td>271.217413</td>
    </tr>
    <tr>
      <th>472</th>
      <td>Albania</td>
      <td>21</td>
      <td>473</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>356.60538</td>
      <td>398.58876</td>
      <td>396.62440</td>
      <td>383.939513</td>
    </tr>
    <tr>
      <th>475</th>
      <td>Albania</td>
      <td>21</td>
      <td>476</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>294.44618</td>
      <td>324.55908</td>
      <td>297.87392</td>
      <td>305.626393</td>
    </tr>
    <tr>
      <th>484</th>
      <td>Albania</td>
      <td>22</td>
      <td>485</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>506.23930</td>
      <td>461.82190</td>
      <td>485.39724</td>
      <td>484.486147</td>
    </tr>
    <tr>
      <th>485</th>
      <td>Albania</td>
      <td>22</td>
      <td>486</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>452.72628</td>
      <td>432.23014</td>
      <td>433.17794</td>
      <td>439.378120</td>
    </tr>
    <tr>
      <th>493</th>
      <td>Albania</td>
      <td>22</td>
      <td>494</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>328.25204</td>
      <td>411.93316</td>
      <td>371.44722</td>
      <td>370.544140</td>
    </tr>
    <tr>
      <th>494</th>
      <td>Albania</td>
      <td>22</td>
      <td>495</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>486.61006</td>
      <td>497.71868</td>
      <td>447.63148</td>
      <td>477.320073</td>
    </tr>
    <tr>
      <th>497</th>
      <td>Albania</td>
      <td>22</td>
      <td>498</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>564.50380</td>
      <td>632.47582</td>
      <td>562.98022</td>
      <td>586.653280</td>
    </tr>
    <tr>
      <th>499</th>
      <td>Albania</td>
      <td>22</td>
      <td>500</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>527.50428</td>
      <td>663.35072</td>
      <td>623.87168</td>
      <td>604.908893</td>
    </tr>
    <tr>
      <th>503</th>
      <td>Albania</td>
      <td>22</td>
      <td>504</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>339.85824</td>
      <td>439.17802</td>
      <td>388.41850</td>
      <td>389.151587</td>
    </tr>
    <tr>
      <th>504</th>
      <td>Albania</td>
      <td>22</td>
      <td>505</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>491.20580</td>
      <td>442.35524</td>
      <td>471.68966</td>
      <td>468.416900</td>
    </tr>
    <tr>
      <th>512</th>
      <td>Albania</td>
      <td>24</td>
      <td>513</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>473.21234</td>
      <td>529.82686</td>
      <td>479.24282</td>
      <td>494.094007</td>
    </tr>
    <tr>
      <th>516</th>
      <td>Albania</td>
      <td>24</td>
      <td>517</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>320.77424</td>
      <td>320.42864</td>
      <td>379.46662</td>
      <td>340.223167</td>
    </tr>
    <tr>
      <th>518</th>
      <td>Albania</td>
      <td>24</td>
      <td>519</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>494.86678</td>
      <td>464.86932</td>
      <td>505.91200</td>
      <td>488.549367</td>
    </tr>
    <tr>
      <th>521</th>
      <td>Albania</td>
      <td>24</td>
      <td>522</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Other language</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>438.39382</td>
      <td>460.46554</td>
      <td>548.52668</td>
      <td>482.462013</td>
    </tr>
    <tr>
      <th>523</th>
      <td>Albania</td>
      <td>24</td>
      <td>524</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>463.08616</td>
      <td>499.51334</td>
      <td>506.28498</td>
      <td>489.628160</td>
    </tr>
    <tr>
      <th>542</th>
      <td>Albania</td>
      <td>24</td>
      <td>543</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>423.28246</td>
      <td>469.76116</td>
      <td>502.64828</td>
      <td>465.230633</td>
    </tr>
    <tr>
      <th>550</th>
      <td>Albania</td>
      <td>25</td>
      <td>551</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>360.96746</td>
      <td>285.55844</td>
      <td>251.62252</td>
      <td>299.382807</td>
    </tr>
    <tr>
      <th>552</th>
      <td>Albania</td>
      <td>25</td>
      <td>553</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>430.99394</td>
      <td>495.25630</td>
      <td>405.76278</td>
      <td>444.004340</td>
    </tr>
    <tr>
      <th>558</th>
      <td>Albania</td>
      <td>25</td>
      <td>559</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>524.07696</td>
      <td>558.77708</td>
      <td>567.36292</td>
      <td>550.072320</td>
    </tr>
    <tr>
      <th>560</th>
      <td>Albania</td>
      <td>25</td>
      <td>561</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>447.35160</td>
      <td>489.45784</td>
      <td>464.97578</td>
      <td>467.261740</td>
    </tr>
    <tr>
      <th>562</th>
      <td>Albania</td>
      <td>26</td>
      <td>563</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Other country</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>342.27294</td>
      <td>455.24596</td>
      <td>381.98434</td>
      <td>393.167747</td>
    </tr>
    <tr>
      <th>564</th>
      <td>Albania</td>
      <td>26</td>
      <td>565</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>365.64106</td>
      <td>332.78894</td>
      <td>346.17682</td>
      <td>348.202273</td>
    </tr>
    <tr>
      <th>566</th>
      <td>Albania</td>
      <td>26</td>
      <td>567</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>420.16668</td>
      <td>428.53426</td>
      <td>418.81762</td>
      <td>422.506187</td>
    </tr>
    <tr>
      <th>573</th>
      <td>Albania</td>
      <td>26</td>
      <td>574</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>331.36778</td>
      <td>369.04042</td>
      <td>331.07048</td>
      <td>343.826227</td>
    </tr>
    <tr>
      <th>577</th>
      <td>Albania</td>
      <td>26</td>
      <td>578</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>369.30206</td>
      <td>403.92148</td>
      <td>359.13838</td>
      <td>377.453973</td>
    </tr>
    <tr>
      <th>579</th>
      <td>Albania</td>
      <td>26</td>
      <td>580</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>380.75248</td>
      <td>384.84720</td>
      <td>439.79858</td>
      <td>401.799420</td>
    </tr>
    <tr>
      <th>580</th>
      <td>Albania</td>
      <td>26</td>
      <td>581</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>447.89686</td>
      <td>450.99564</td>
      <td>361.93586</td>
      <td>420.276120</td>
    </tr>
    <tr>
      <th>583</th>
      <td>Albania</td>
      <td>26</td>
      <td>584</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>181.50024</td>
      <td>161.88434</td>
      <td>190.91758</td>
      <td>178.100720</td>
    </tr>
    <tr>
      <th>585</th>
      <td>Albania</td>
      <td>26</td>
      <td>586</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>430.68236</td>
      <td>481.91190</td>
      <td>431.68592</td>
      <td>448.093393</td>
    </tr>
    <tr>
      <th>587</th>
      <td>Albania</td>
      <td>26</td>
      <td>588</td>
      <td>9</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>366.18634</td>
      <td>310.42034</td>
      <td>351.95822</td>
      <td>342.854967</td>
    </tr>
    <tr>
      <th>588</th>
      <td>Albania</td>
      <td>26</td>
      <td>589</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>360.11060</td>
      <td>402.55816</td>
      <td>402.68556</td>
      <td>388.451440</td>
    </tr>
    <tr>
      <th>592</th>
      <td>Albania</td>
      <td>26</td>
      <td>593</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>410.50786</td>
      <td>455.06422</td>
      <td>455.09138</td>
      <td>440.221153</td>
    </tr>
    <tr>
      <th>597</th>
      <td>Albania</td>
      <td>27</td>
      <td>598</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>406.92476</td>
      <td>393.02858</td>
      <td>475.13988</td>
      <td>425.031073</td>
    </tr>
    <tr>
      <th>598</th>
      <td>Albania</td>
      <td>27</td>
      <td>599</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>288.21468</td>
      <td>283.22874</td>
      <td>338.06418</td>
      <td>303.169200</td>
    </tr>
    <tr>
      <th>599</th>
      <td>Albania</td>
      <td>27</td>
      <td>600</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>474.14706</td>
      <td>520.43594</td>
      <td>514.77062</td>
      <td>503.117873</td>
    </tr>
    <tr>
      <th>602</th>
      <td>Albania</td>
      <td>27</td>
      <td>603</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>501.09832</td>
      <td>568.65058</td>
      <td>511.50690</td>
      <td>527.085267</td>
    </tr>
    <tr>
      <th>604</th>
      <td>Albania</td>
      <td>27</td>
      <td>605</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>449.06528</td>
      <td>446.90572</td>
      <td>429.63448</td>
      <td>441.868493</td>
    </tr>
    <tr>
      <th>605</th>
      <td>Albania</td>
      <td>27</td>
      <td>606</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>359.64324</td>
      <td>262.85932</td>
      <td>358.85864</td>
      <td>327.120400</td>
    </tr>
    <tr>
      <th>607</th>
      <td>Albania</td>
      <td>27</td>
      <td>608</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>393.99442</td>
      <td>452.28412</td>
      <td>447.81800</td>
      <td>431.365513</td>
    </tr>
    <tr>
      <th>610</th>
      <td>Albania</td>
      <td>27</td>
      <td>611</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>483.10484</td>
      <td>454.04304</td>
      <td>367.53078</td>
      <td>434.892887</td>
    </tr>
    <tr>
      <th>613</th>
      <td>Albania</td>
      <td>27</td>
      <td>614</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>419.93302</td>
      <td>551.33460</td>
      <td>483.34578</td>
      <td>484.871133</td>
    </tr>
    <tr>
      <th>614</th>
      <td>Albania</td>
      <td>27</td>
      <td>615</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>494.39946</td>
      <td>487.94864</td>
      <td>490.80568</td>
      <td>491.051260</td>
    </tr>
    <tr>
      <th>621</th>
      <td>Albania</td>
      <td>27</td>
      <td>622</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>445.17060</td>
      <td>415.18984</td>
      <td>404.64378</td>
      <td>421.668073</td>
    </tr>
    <tr>
      <th>622</th>
      <td>Albania</td>
      <td>27</td>
      <td>623</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>235.40272</td>
      <td>80.73762</td>
      <td>187.28084</td>
      <td>167.807060</td>
    </tr>
    <tr>
      <th>625</th>
      <td>Albania</td>
      <td>27</td>
      <td>626</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>343.83082</td>
      <td>260.14052</td>
      <td>361.00336</td>
      <td>321.658233</td>
    </tr>
    <tr>
      <th>633</th>
      <td>Albania</td>
      <td>28</td>
      <td>634</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>442.21064</td>
      <td>469.52068</td>
      <td>462.08504</td>
      <td>457.938787</td>
    </tr>
    <tr>
      <th>635</th>
      <td>Albania</td>
      <td>28</td>
      <td>636</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>338.22248</td>
      <td>238.07926</td>
      <td>308.22456</td>
      <td>294.842100</td>
    </tr>
    <tr>
      <th>637</th>
      <td>Albania</td>
      <td>28</td>
      <td>638</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>358.63064</td>
      <td>421.22658</td>
      <td>388.79152</td>
      <td>389.549580</td>
    </tr>
    <tr>
      <th>645</th>
      <td>Albania</td>
      <td>28</td>
      <td>646</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>403.10796</td>
      <td>347.03804</td>
      <td>371.07422</td>
      <td>373.740073</td>
    </tr>
    <tr>
      <th>647</th>
      <td>Albania</td>
      <td>28</td>
      <td>648</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>394.07230</td>
      <td>331.50584</td>
      <td>376.76240</td>
      <td>367.446847</td>
    </tr>
    <tr>
      <th>649</th>
      <td>Albania</td>
      <td>28</td>
      <td>650</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>442.28850</td>
      <td>436.71564</td>
      <td>303.18912</td>
      <td>394.064420</td>
    </tr>
    <tr>
      <th>656</th>
      <td>Albania</td>
      <td>28</td>
      <td>657</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>360.42220</td>
      <td>290.20564</td>
      <td>332.84222</td>
      <td>327.823353</td>
    </tr>
    <tr>
      <th>659</th>
      <td>Albania</td>
      <td>28</td>
      <td>660</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>422.73718</td>
      <td>442.83186</td>
      <td>424.22602</td>
      <td>429.931687</td>
    </tr>
    <tr>
      <th>671</th>
      <td>Albania</td>
      <td>29</td>
      <td>672</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>462.85248</td>
      <td>565.15560</td>
      <td>479.33608</td>
      <td>502.448053</td>
    </tr>
    <tr>
      <th>674</th>
      <td>Albania</td>
      <td>30</td>
      <td>675</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>293.12198</td>
      <td>308.75228</td>
      <td>330.41774</td>
      <td>310.764000</td>
    </tr>
    <tr>
      <th>677</th>
      <td>Albania</td>
      <td>30</td>
      <td>678</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>345.54450</td>
      <td>289.00274</td>
      <td>406.50878</td>
      <td>347.018673</td>
    </tr>
    <tr>
      <th>678</th>
      <td>Albania</td>
      <td>30</td>
      <td>679</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>380.75246</td>
      <td>379.04874</td>
      <td>409.02650</td>
      <td>389.609233</td>
    </tr>
    <tr>
      <th>686</th>
      <td>Albania</td>
      <td>30</td>
      <td>687</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>449.92208</td>
      <td>458.85472</td>
      <td>445.67326</td>
      <td>451.483353</td>
    </tr>
    <tr>
      <th>687</th>
      <td>Albania</td>
      <td>30</td>
      <td>688</td>
      <td>9</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>415.96042</td>
      <td>388.04296</td>
      <td>434.29690</td>
      <td>412.766760</td>
    </tr>
    <tr>
      <th>689</th>
      <td>Albania</td>
      <td>31</td>
      <td>690</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>481.78064</td>
      <td>401.59584</td>
      <td>428.23574</td>
      <td>437.204073</td>
    </tr>
    <tr>
      <th>693</th>
      <td>Albania</td>
      <td>31</td>
      <td>694</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>452.88206</td>
      <td>411.77430</td>
      <td>457.23610</td>
      <td>440.630820</td>
    </tr>
    <tr>
      <th>695</th>
      <td>Albania</td>
      <td>31</td>
      <td>696</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>323.03318</td>
      <td>354.98114</td>
      <td>350.37300</td>
      <td>342.795773</td>
    </tr>
    <tr>
      <th>697</th>
      <td>Albania</td>
      <td>31</td>
      <td>698</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>340.79296</td>
      <td>305.81334</td>
      <td>318.76166</td>
      <td>321.789320</td>
    </tr>
    <tr>
      <th>699</th>
      <td>Albania</td>
      <td>31</td>
      <td>700</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>393.60492</td>
      <td>323.68532</td>
      <td>397.37040</td>
      <td>371.553547</td>
    </tr>
    <tr>
      <th>703</th>
      <td>Albania</td>
      <td>31</td>
      <td>704</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>304.26078</td>
      <td>304.56048</td>
      <td>282.39460</td>
      <td>297.071953</td>
    </tr>
    <tr>
      <th>706</th>
      <td>Albania</td>
      <td>31</td>
      <td>707</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>397.42170</td>
      <td>415.54966</td>
      <td>377.97464</td>
      <td>396.982000</td>
    </tr>
    <tr>
      <th>714</th>
      <td>Albania</td>
      <td>31</td>
      <td>715</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>441.82114</td>
      <td>446.48568</td>
      <td>526.33346</td>
      <td>471.546760</td>
    </tr>
    <tr>
      <th>725</th>
      <td>Albania</td>
      <td>32</td>
      <td>726</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>402.25112</td>
      <td>412.82306</td>
      <td>438.49310</td>
      <td>417.855760</td>
    </tr>
    <tr>
      <th>727</th>
      <td>Albania</td>
      <td>32</td>
      <td>728</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>216.24084</td>
      <td>68.76084</td>
      <td>122.19318</td>
      <td>135.731620</td>
    </tr>
    <tr>
      <th>728</th>
      <td>Albania</td>
      <td>32</td>
      <td>729</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>461.60616</td>
      <td>419.55942</td>
      <td>467.49346</td>
      <td>449.553013</td>
    </tr>
    <tr>
      <th>729</th>
      <td>Albania</td>
      <td>32</td>
      <td>730</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>361.43482</td>
      <td>322.84482</td>
      <td>318.85490</td>
      <td>334.378180</td>
    </tr>
    <tr>
      <th>733</th>
      <td>Albania</td>
      <td>32</td>
      <td>734</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>150.73220</td>
      <td>117.08526</td>
      <td>98.50800</td>
      <td>122.108487</td>
    </tr>
    <tr>
      <th>734</th>
      <td>Albania</td>
      <td>32</td>
      <td>735</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>203.23262</td>
      <td>158.36590</td>
      <td>180.28722</td>
      <td>180.628580</td>
    </tr>
    <tr>
      <th>735</th>
      <td>Albania</td>
      <td>32</td>
      <td>736</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>390.64496</td>
      <td>355.53714</td>
      <td>348.78776</td>
      <td>364.989953</td>
    </tr>
    <tr>
      <th>736</th>
      <td>Albania</td>
      <td>32</td>
      <td>737</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>375.22198</td>
      <td>390.20820</td>
      <td>356.99366</td>
      <td>374.141280</td>
    </tr>
    <tr>
      <th>737</th>
      <td>Albania</td>
      <td>32</td>
      <td>738</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>169.89408</td>
      <td>97.14806</td>
      <td>140.19024</td>
      <td>135.744127</td>
    </tr>
    <tr>
      <th>738</th>
      <td>Albania</td>
      <td>32</td>
      <td>739</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>284.86524</td>
      <td>248.02336</td>
      <td>284.91236</td>
      <td>272.600320</td>
    </tr>
    <tr>
      <th>739</th>
      <td>Albania</td>
      <td>32</td>
      <td>740</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>408.56052</td>
      <td>365.46602</td>
      <td>356.90042</td>
      <td>376.975653</td>
    </tr>
    <tr>
      <th>740</th>
      <td>Albania</td>
      <td>32</td>
      <td>741</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>301.92398</td>
      <td>373.17086</td>
      <td>346.92280</td>
      <td>340.672547</td>
    </tr>
    <tr>
      <th>743</th>
      <td>Albania</td>
      <td>32</td>
      <td>744</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>330.35518</td>
      <td>288.25908</td>
      <td>304.30810</td>
      <td>307.640787</td>
    </tr>
    <tr>
      <th>744</th>
      <td>Albania</td>
      <td>32</td>
      <td>745</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>281.98318</td>
      <td>265.46236</td>
      <td>286.59084</td>
      <td>278.012127</td>
    </tr>
    <tr>
      <th>745</th>
      <td>Albania</td>
      <td>32</td>
      <td>746</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>516.52128</td>
      <td>455.46136</td>
      <td>489.96644</td>
      <td>487.316360</td>
    </tr>
    <tr>
      <th>748</th>
      <td>Albania</td>
      <td>32</td>
      <td>749</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>538.72098</td>
      <td>508.01394</td>
      <td>548.61992</td>
      <td>531.784947</td>
    </tr>
    <tr>
      <th>750</th>
      <td>Albania</td>
      <td>32</td>
      <td>751</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>202.84312</td>
      <td>122.40712</td>
      <td>245.09512</td>
      <td>190.115120</td>
    </tr>
    <tr>
      <th>751</th>
      <td>Albania</td>
      <td>33</td>
      <td>752</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>355.59276</td>
      <td>242.18908</td>
      <td>377.78816</td>
      <td>325.190000</td>
    </tr>
    <tr>
      <th>758</th>
      <td>Albania</td>
      <td>33</td>
      <td>759</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>477.18490</td>
      <td>470.47380</td>
      <td>564.93846</td>
      <td>504.199053</td>
    </tr>
    <tr>
      <th>777</th>
      <td>Albania</td>
      <td>33</td>
      <td>778</td>
      <td>9</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>386.04924</td>
      <td>349.87038</td>
      <td>421.42858</td>
      <td>385.782733</td>
    </tr>
    <tr>
      <th>780</th>
      <td>Albania</td>
      <td>33</td>
      <td>781</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>493.46474</td>
      <td>507.93376</td>
      <td>547.22118</td>
      <td>516.206560</td>
    </tr>
    <tr>
      <th>796</th>
      <td>Albania</td>
      <td>34</td>
      <td>797</td>
      <td>8</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>345.07710</td>
      <td>352.51680</td>
      <td>356.52740</td>
      <td>351.373767</td>
    </tr>
    <tr>
      <th>797</th>
      <td>Albania</td>
      <td>34</td>
      <td>798</td>
      <td>8</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>452.18102</td>
      <td>404.08184</td>
      <td>445.11376</td>
      <td>433.792207</td>
    </tr>
    <tr>
      <th>806</th>
      <td>Albania</td>
      <td>35</td>
      <td>807</td>
      <td>11</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>321.08584</td>
      <td>371.50278</td>
      <td>326.03508</td>
      <td>339.541233</td>
    </tr>
    <tr>
      <th>807</th>
      <td>Albania</td>
      <td>35</td>
      <td>808</td>
      <td>11</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>319.37218</td>
      <td>364.38558</td>
      <td>299.55242</td>
      <td>327.770060</td>
    </tr>
    <tr>
      <th>811</th>
      <td>Albania</td>
      <td>35</td>
      <td>812</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>527.11480</td>
      <td>585.80260</td>
      <td>562.23424</td>
      <td>558.383880</td>
    </tr>
    <tr>
      <th>815</th>
      <td>Albania</td>
      <td>35</td>
      <td>816</td>
      <td>11</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>365.48528</td>
      <td>438.08434</td>
      <td>443.90152</td>
      <td>415.823713</td>
    </tr>
    <tr>
      <th>816</th>
      <td>Albania</td>
      <td>35</td>
      <td>817</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>286.65682</td>
      <td>260.13272</td>
      <td>256.37822</td>
      <td>267.722587</td>
    </tr>
    <tr>
      <th>832</th>
      <td>Albania</td>
      <td>35</td>
      <td>833</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>354.11280</td>
      <td>452.75994</td>
      <td>378.62736</td>
      <td>395.166700</td>
    </tr>
    <tr>
      <th>833</th>
      <td>Albania</td>
      <td>35</td>
      <td>834</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>421.49088</td>
      <td>417.55454</td>
      <td>439.70536</td>
      <td>426.250260</td>
    </tr>
    <tr>
      <th>834</th>
      <td>Albania</td>
      <td>36</td>
      <td>835</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>384.80296</td>
      <td>399.30364</td>
      <td>351.02572</td>
      <td>378.377440</td>
    </tr>
    <tr>
      <th>835</th>
      <td>Albania</td>
      <td>36</td>
      <td>836</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>395.70806</td>
      <td>399.91174</td>
      <td>432.71166</td>
      <td>409.443820</td>
    </tr>
    <tr>
      <th>837</th>
      <td>Albania</td>
      <td>36</td>
      <td>838</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>398.12278</td>
      <td>415.14872</td>
      <td>421.80158</td>
      <td>411.691027</td>
    </tr>
    <tr>
      <th>846</th>
      <td>Albania</td>
      <td>36</td>
      <td>847</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>494.71102</td>
      <td>550.61974</td>
      <td>500.22380</td>
      <td>515.184853</td>
    </tr>
    <tr>
      <th>861</th>
      <td>Albania</td>
      <td>36</td>
      <td>862</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>367.82210</td>
      <td>344.97282</td>
      <td>380.67884</td>
      <td>364.491253</td>
    </tr>
    <tr>
      <th>869</th>
      <td>Albania</td>
      <td>37</td>
      <td>870</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>534.98210</td>
      <td>407.12924</td>
      <td>450.61544</td>
      <td>464.242260</td>
    </tr>
    <tr>
      <th>876</th>
      <td>Albania</td>
      <td>37</td>
      <td>877</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>Three or four times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>349.36128</td>
      <td>393.10800</td>
      <td>363.05482</td>
      <td>368.508033</td>
    </tr>
    <tr>
      <th>877</th>
      <td>Albania</td>
      <td>37</td>
      <td>878</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>398.20064</td>
      <td>572.06606</td>
      <td>491.64494</td>
      <td>487.303880</td>
    </tr>
    <tr>
      <th>878</th>
      <td>Albania</td>
      <td>37</td>
      <td>879</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>442.75588</td>
      <td>464.67536</td>
      <td>396.81090</td>
      <td>434.747380</td>
    </tr>
    <tr>
      <th>884</th>
      <td>Albania</td>
      <td>37</td>
      <td>885</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>403.34164</td>
      <td>474.52480</td>
      <td>413.59568</td>
      <td>430.487373</td>
    </tr>
    <tr>
      <th>909</th>
      <td>Albania</td>
      <td>39</td>
      <td>910</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>329.18680</td>
      <td>230.43330</td>
      <td>273.90898</td>
      <td>277.843027</td>
    </tr>
    <tr>
      <th>912</th>
      <td>Albania</td>
      <td>40</td>
      <td>913</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>562.71226</td>
      <td>586.20482</td>
      <td>582.56248</td>
      <td>577.159853</td>
    </tr>
    <tr>
      <th>917</th>
      <td>Albania</td>
      <td>40</td>
      <td>918</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>414.09096</td>
      <td>480.66762</td>
      <td>481.48078</td>
      <td>458.746453</td>
    </tr>
    <tr>
      <th>928</th>
      <td>Albania</td>
      <td>40</td>
      <td>929</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>443.14534</td>
      <td>513.68428</td>
      <td>388.79150</td>
      <td>448.540373</td>
    </tr>
    <tr>
      <th>929</th>
      <td>Albania</td>
      <td>40</td>
      <td>930</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>422.19194</td>
      <td>447.22652</td>
      <td>493.23012</td>
      <td>454.216193</td>
    </tr>
    <tr>
      <th>933</th>
      <td>Albania</td>
      <td>40</td>
      <td>934</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>379.73984</td>
      <td>430.86684</td>
      <td>445.85976</td>
      <td>418.822147</td>
    </tr>
    <tr>
      <th>941</th>
      <td>Albania</td>
      <td>40</td>
      <td>942</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>332.38044</td>
      <td>303.75856</td>
      <td>312.04774</td>
      <td>316.062247</td>
    </tr>
    <tr>
      <th>949</th>
      <td>Albania</td>
      <td>41</td>
      <td>950</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>509.74448</td>
      <td>445.78302</td>
      <td>472.71542</td>
      <td>476.080973</td>
    </tr>
    <tr>
      <th>951</th>
      <td>Albania</td>
      <td>41</td>
      <td>952</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>406.76898</td>
      <td>468.80578</td>
      <td>432.80492</td>
      <td>436.126560</td>
    </tr>
    <tr>
      <th>955</th>
      <td>Albania</td>
      <td>41</td>
      <td>956</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>555.31234</td>
      <td>427.01750</td>
      <td>461.89852</td>
      <td>481.409453</td>
    </tr>
    <tr>
      <th>957</th>
      <td>Albania</td>
      <td>41</td>
      <td>958</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>445.17058</td>
      <td>388.76470</td>
      <td>362.96158</td>
      <td>398.965620</td>
    </tr>
    <tr>
      <th>959</th>
      <td>Albania</td>
      <td>41</td>
      <td>960</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>381.53142</td>
      <td>392.53384</td>
      <td>329.76502</td>
      <td>367.943427</td>
    </tr>
    <tr>
      <th>960</th>
      <td>Albania</td>
      <td>41</td>
      <td>961</td>
      <td>9</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>348.11496</td>
      <td>307.04650</td>
      <td>322.58488</td>
      <td>325.915447</td>
    </tr>
    <tr>
      <th>961</th>
      <td>Albania</td>
      <td>41</td>
      <td>962</td>
      <td>9</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>435.35596</td>
      <td>433.43306</td>
      <td>428.14248</td>
      <td>432.310500</td>
    </tr>
    <tr>
      <th>963</th>
      <td>Albania</td>
      <td>41</td>
      <td>964</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>412.53312</td>
      <td>368.24610</td>
      <td>395.50542</td>
      <td>392.094880</td>
    </tr>
    <tr>
      <th>966</th>
      <td>Albania</td>
      <td>41</td>
      <td>967</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>512.23710</td>
      <td>602.56762</td>
      <td>491.17866</td>
      <td>535.327793</td>
    </tr>
    <tr>
      <th>968</th>
      <td>Albania</td>
      <td>41</td>
      <td>969</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>588.65088</td>
      <td>565.07616</td>
      <td>540.50730</td>
      <td>564.744780</td>
    </tr>
    <tr>
      <th>972</th>
      <td>Albania</td>
      <td>42</td>
      <td>973</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>464.56614</td>
      <td>527.58474</td>
      <td>476.07238</td>
      <td>489.407753</td>
    </tr>
    <tr>
      <th>976</th>
      <td>Albania</td>
      <td>42</td>
      <td>977</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>432.94128</td>
      <td>378.33386</td>
      <td>436.81464</td>
      <td>416.029927</td>
    </tr>
    <tr>
      <th>981</th>
      <td>Albania</td>
      <td>42</td>
      <td>982</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>358.78642</td>
      <td>407.80276</td>
      <td>453.41292</td>
      <td>406.667367</td>
    </tr>
    <tr>
      <th>983</th>
      <td>Albania</td>
      <td>43</td>
      <td>984</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>400.69324</td>
      <td>436.31848</td>
      <td>394.57292</td>
      <td>410.528213</td>
    </tr>
    <tr>
      <th>984</th>
      <td>Albania</td>
      <td>43</td>
      <td>985</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>347.41390</td>
      <td>409.61530</td>
      <td>294.61022</td>
      <td>350.546473</td>
    </tr>
    <tr>
      <th>985</th>
      <td>Albania</td>
      <td>43</td>
      <td>986</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>518.39072</td>
      <td>532.07230</td>
      <td>466.74748</td>
      <td>505.736833</td>
    </tr>
    <tr>
      <th>987</th>
      <td>Albania</td>
      <td>43</td>
      <td>988</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>447.35160</td>
      <td>483.95562</td>
      <td>457.04960</td>
      <td>462.785607</td>
    </tr>
    <tr>
      <th>1008</th>
      <td>Albania</td>
      <td>43</td>
      <td>1009</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>424.84030</td>
      <td>521.46856</td>
      <td>503.58076</td>
      <td>483.296540</td>
    </tr>
    <tr>
      <th>1013</th>
      <td>Albania</td>
      <td>44</td>
      <td>1014</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>Five or more times</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>324.51318</td>
      <td>405.65812</td>
      <td>461.99180</td>
      <td>397.387700</td>
    </tr>
    <tr>
      <th>1015</th>
      <td>Albania</td>
      <td>44</td>
      <td>1016</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>456.85464</td>
      <td>485.23868</td>
      <td>435.41590</td>
      <td>459.169740</td>
    </tr>
    <tr>
      <th>1018</th>
      <td>Albania</td>
      <td>44</td>
      <td>1019</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>335.88568</td>
      <td>333.13760</td>
      <td>416.76614</td>
      <td>361.929807</td>
    </tr>
    <tr>
      <th>1027</th>
      <td>Albania</td>
      <td>45</td>
      <td>1028</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>365.01792</td>
      <td>268.15216</td>
      <td>344.21858</td>
      <td>325.796220</td>
    </tr>
    <tr>
      <th>1030</th>
      <td>Albania</td>
      <td>45</td>
      <td>1031</td>
      <td>9</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>469.55134</td>
      <td>503.27884</td>
      <td>538.08280</td>
      <td>503.637660</td>
    </tr>
    <tr>
      <th>1031</th>
      <td>Albania</td>
      <td>45</td>
      <td>1032</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>521.42856</td>
      <td>537.19588</td>
      <td>517.75458</td>
      <td>525.459673</td>
    </tr>
    <tr>
      <th>1036</th>
      <td>Albania</td>
      <td>46</td>
      <td>1037</td>
      <td>8</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>Other country</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>340.32558</td>
      <td>393.33582</td>
      <td>391.02948</td>
      <td>374.896960</td>
    </tr>
    <tr>
      <th>1044</th>
      <td>Albania</td>
      <td>46</td>
      <td>1045</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>445.32636</td>
      <td>554.90900</td>
      <td>511.97314</td>
      <td>504.069500</td>
    </tr>
    <tr>
      <th>1061</th>
      <td>Albania</td>
      <td>47</td>
      <td>1062</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>493.54262</td>
      <td>498.19524</td>
      <td>507.59046</td>
      <td>499.776107</td>
    </tr>
    <tr>
      <th>1063</th>
      <td>Albania</td>
      <td>47</td>
      <td>1064</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>416.58360</td>
      <td>367.19238</td>
      <td>389.63074</td>
      <td>391.135573</td>
    </tr>
    <tr>
      <th>1066</th>
      <td>Albania</td>
      <td>47</td>
      <td>1067</td>
      <td>8</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>239.68686</td>
      <td>229.33802</td>
      <td>218.42596</td>
      <td>229.150280</td>
    </tr>
    <tr>
      <th>1067</th>
      <td>Albania</td>
      <td>47</td>
      <td>1068</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>401.55010</td>
      <td>354.66342</td>
      <td>360.44386</td>
      <td>372.219127</td>
    </tr>
    <tr>
      <th>1073</th>
      <td>Albania</td>
      <td>48</td>
      <td>1074</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>266.24864</td>
      <td>325.81202</td>
      <td>323.79710</td>
      <td>305.285920</td>
    </tr>
    <tr>
      <th>1074</th>
      <td>Albania</td>
      <td>48</td>
      <td>1075</td>
      <td>9</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>349.90654</td>
      <td>396.14262</td>
      <td>364.17382</td>
      <td>370.074327</td>
    </tr>
    <tr>
      <th>1089</th>
      <td>Albania</td>
      <td>48</td>
      <td>1090</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>501.17620</td>
      <td>493.98540</td>
      <td>429.54120</td>
      <td>474.900933</td>
    </tr>
    <tr>
      <th>1094</th>
      <td>Albania</td>
      <td>48</td>
      <td>1095</td>
      <td>9</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>386.59448</td>
      <td>308.49002</td>
      <td>337.87764</td>
      <td>344.320713</td>
    </tr>
    <tr>
      <th>1097</th>
      <td>Albania</td>
      <td>48</td>
      <td>1098</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>Five or more times</td>
      <td>No</td>
      <td>Yes</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>422.50350</td>
      <td>390.24848</td>
      <td>440.54458</td>
      <td>417.765520</td>
    </tr>
    <tr>
      <th>1102</th>
      <td>Albania</td>
      <td>49</td>
      <td>1103</td>
      <td>9</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>516.59916</td>
      <td>547.99848</td>
      <td>555.42710</td>
      <td>540.008247</td>
    </tr>
    <tr>
      <th>1116</th>
      <td>Albania</td>
      <td>50</td>
      <td>1117</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>303.71550</td>
      <td>257.04270</td>
      <td>348.60128</td>
      <td>303.119827</td>
    </tr>
    <tr>
      <th>1120</th>
      <td>Albania</td>
      <td>50</td>
      <td>1121</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>Yes</td>
      <td>412.53312</td>
      <td>500.97536</td>
      <td>560.36926</td>
      <td>491.292580</td>
    </tr>
    <tr>
      <th>1127</th>
      <td>Albania</td>
      <td>50</td>
      <td>1128</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>476.63966</td>
      <td>511.77794</td>
      <td>504.04698</td>
      <td>497.488193</td>
    </tr>
    <tr>
      <th>1129</th>
      <td>Albania</td>
      <td>50</td>
      <td>1130</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>302.15764</td>
      <td>235.99418</td>
      <td>377.41516</td>
      <td>305.188993</td>
    </tr>
    <tr>
      <th>1135</th>
      <td>Albania</td>
      <td>50</td>
      <td>1136</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>378.88300</td>
      <td>333.99186</td>
      <td>425.34500</td>
      <td>379.406620</td>
    </tr>
    <tr>
      <th>1146</th>
      <td>Albania</td>
      <td>51</td>
      <td>1147</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>400.84906</td>
      <td>396.86436</td>
      <td>420.49610</td>
      <td>406.069840</td>
    </tr>
    <tr>
      <th>1158</th>
      <td>Albania</td>
      <td>51</td>
      <td>1159</td>
      <td>9</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>432.70758</td>
      <td>373.92876</td>
      <td>404.27080</td>
      <td>403.635713</td>
    </tr>
    <tr>
      <th>1175</th>
      <td>Albania</td>
      <td>52</td>
      <td>1176</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>362.21374</td>
      <td>380.95508</td>
      <td>435.60240</td>
      <td>392.923740</td>
    </tr>
    <tr>
      <th>1180</th>
      <td>Albania</td>
      <td>52</td>
      <td>1181</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>338.53406</td>
      <td>335.59998</td>
      <td>417.79186</td>
      <td>363.975300</td>
    </tr>
    <tr>
      <th>1185</th>
      <td>Albania</td>
      <td>53</td>
      <td>1186</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>426.55400</td>
      <td>392.55200</td>
      <td>434.85638</td>
      <td>417.987460</td>
    </tr>
    <tr>
      <th>1193</th>
      <td>Albania</td>
      <td>53</td>
      <td>1194</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>484.81850</td>
      <td>428.13708</td>
      <td>525.49424</td>
      <td>479.483273</td>
    </tr>
    <tr>
      <th>1195</th>
      <td>Albania</td>
      <td>53</td>
      <td>1196</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>308.70072</td>
      <td>369.11986</td>
      <td>349.81350</td>
      <td>342.544693</td>
    </tr>
    <tr>
      <th>1197</th>
      <td>Albania</td>
      <td>53</td>
      <td>1198</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>553.75450</td>
      <td>501.51820</td>
      <td>544.61024</td>
      <td>533.294313</td>
    </tr>
    <tr>
      <th>1198</th>
      <td>Albania</td>
      <td>53</td>
      <td>1199</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>455.68626</td>
      <td>440.00902</td>
      <td>458.72806</td>
      <td>451.474447</td>
    </tr>
    <tr>
      <th>1206</th>
      <td>Albania</td>
      <td>53</td>
      <td>1207</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>No</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>404.12058</td>
      <td>403.51348</td>
      <td>416.57964</td>
      <td>408.071233</td>
    </tr>
    <tr>
      <th>1209</th>
      <td>Albania</td>
      <td>53</td>
      <td>1210</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>449.37686</td>
      <td>357.44352</td>
      <td>431.59268</td>
      <td>412.804353</td>
    </tr>
    <tr>
      <th>1215</th>
      <td>Albania</td>
      <td>53</td>
      <td>1216</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>401.93956</td>
      <td>262.13758</td>
      <td>416.95264</td>
      <td>360.343260</td>
    </tr>
    <tr>
      <th>1228</th>
      <td>Albania</td>
      <td>54</td>
      <td>1229</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>332.53622</td>
      <td>361.73914</td>
      <td>343.84556</td>
      <td>346.040307</td>
    </tr>
    <tr>
      <th>1234</th>
      <td>Albania</td>
      <td>54</td>
      <td>1235</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>432.55180</td>
      <td>532.11228</td>
      <td>509.26892</td>
      <td>491.311000</td>
    </tr>
    <tr>
      <th>1238</th>
      <td>Albania</td>
      <td>54</td>
      <td>1239</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>158.67738</td>
      <td>147.78022</td>
      <td>198.00448</td>
      <td>168.154027</td>
    </tr>
    <tr>
      <th>1241</th>
      <td>Albania</td>
      <td>54</td>
      <td>1242</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>385.81554</td>
      <td>382.06710</td>
      <td>422.26782</td>
      <td>396.716820</td>
    </tr>
    <tr>
      <th>1253</th>
      <td>Albania</td>
      <td>55</td>
      <td>1254</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>440.57486</td>
      <td>380.10372</td>
      <td>398.11638</td>
      <td>406.264987</td>
    </tr>
    <tr>
      <th>1257</th>
      <td>Albania</td>
      <td>55</td>
      <td>1258</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>325.37000</td>
      <td>364.19516</td>
      <td>369.76872</td>
      <td>353.111293</td>
    </tr>
    <tr>
      <th>1259</th>
      <td>Albania</td>
      <td>55</td>
      <td>1260</td>
      <td>9</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>407.08054</td>
      <td>368.32556</td>
      <td>421.89482</td>
      <td>399.100307</td>
    </tr>
    <tr>
      <th>1260</th>
      <td>Albania</td>
      <td>55</td>
      <td>1261</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>386.43868</td>
      <td>334.47304</td>
      <td>396.43790</td>
      <td>372.449873</td>
    </tr>
    <tr>
      <th>1264</th>
      <td>Albania</td>
      <td>55</td>
      <td>1265</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>Three or four times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>234.93534</td>
      <td>214.54710</td>
      <td>296.75494</td>
      <td>248.745793</td>
    </tr>
    <tr>
      <th>1268</th>
      <td>Albania</td>
      <td>56</td>
      <td>1269</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>340.40348</td>
      <td>324.92986</td>
      <td>400.35434</td>
      <td>355.229227</td>
    </tr>
    <tr>
      <th>1270</th>
      <td>Albania</td>
      <td>56</td>
      <td>1271</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>371.01574</td>
      <td>385.16494</td>
      <td>340.48864</td>
      <td>365.556440</td>
    </tr>
    <tr>
      <th>1271</th>
      <td>Albania</td>
      <td>57</td>
      <td>1272</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>307.37654</td>
      <td>234.14968</td>
      <td>347.85530</td>
      <td>296.460507</td>
    </tr>
    <tr>
      <th>1273</th>
      <td>Albania</td>
      <td>57</td>
      <td>1274</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>459.26938</td>
      <td>430.99662</td>
      <td>503.30098</td>
      <td>464.522327</td>
    </tr>
    <tr>
      <th>1274</th>
      <td>Albania</td>
      <td>57</td>
      <td>1275</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>324.35738</td>
      <td>347.19688</td>
      <td>390.19024</td>
      <td>353.914833</td>
    </tr>
    <tr>
      <th>1275</th>
      <td>Albania</td>
      <td>57</td>
      <td>1276</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>397.42172</td>
      <td>340.80840</td>
      <td>421.80158</td>
      <td>386.677233</td>
    </tr>
    <tr>
      <th>1284</th>
      <td>Albania</td>
      <td>57</td>
      <td>1285</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>231.43014</td>
      <td>115.22122</td>
      <td>248.54532</td>
      <td>198.398893</td>
    </tr>
    <tr>
      <th>1315</th>
      <td>Albania</td>
      <td>59</td>
      <td>1316</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>237.42794</td>
      <td>150.90780</td>
      <td>250.22380</td>
      <td>212.853180</td>
    </tr>
    <tr>
      <th>1317</th>
      <td>Albania</td>
      <td>59</td>
      <td>1318</td>
      <td>9</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>591.22136</td>
      <td>582.91562</td>
      <td>546.94144</td>
      <td>573.692807</td>
    </tr>
    <tr>
      <th>1331</th>
      <td>Albania</td>
      <td>59</td>
      <td>1332</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>424.21718</td>
      <td>387.07126</td>
      <td>395.78516</td>
      <td>402.357867</td>
    </tr>
    <tr>
      <th>1332</th>
      <td>Albania</td>
      <td>59</td>
      <td>1333</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>409.88472</td>
      <td>319.71376</td>
      <td>362.12236</td>
      <td>363.906947</td>
    </tr>
    <tr>
      <th>1333</th>
      <td>Albania</td>
      <td>59</td>
      <td>1334</td>
      <td>9</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>372.10624</td>
      <td>314.63016</td>
      <td>344.59156</td>
      <td>343.775987</td>
    </tr>
    <tr>
      <th>1337</th>
      <td>Albania</td>
      <td>60</td>
      <td>1338</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>319.83954</td>
      <td>265.82652</td>
      <td>311.30174</td>
      <td>298.989267</td>
    </tr>
    <tr>
      <th>1342</th>
      <td>Albania</td>
      <td>60</td>
      <td>1343</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>382.38824</td>
      <td>366.65750</td>
      <td>420.02986</td>
      <td>389.691867</td>
    </tr>
    <tr>
      <th>1344</th>
      <td>Albania</td>
      <td>60</td>
      <td>1345</td>
      <td>9</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>436.52438</td>
      <td>494.46108</td>
      <td>535.75158</td>
      <td>488.912347</td>
    </tr>
    <tr>
      <th>1350</th>
      <td>Albania</td>
      <td>60</td>
      <td>1351</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>No</td>
      <td>374.52096</td>
      <td>471.90358</td>
      <td>368.92950</td>
      <td>405.118013</td>
    </tr>
    <tr>
      <th>1351</th>
      <td>Albania</td>
      <td>60</td>
      <td>1352</td>
      <td>9</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Other country</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>368.83472</td>
      <td>407.69062</td>
      <td>410.89146</td>
      <td>395.805600</td>
    </tr>
    <tr>
      <th>1352</th>
      <td>Albania</td>
      <td>60</td>
      <td>1353</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>305.27340</td>
      <td>325.73180</td>
      <td>279.41068</td>
      <td>303.471960</td>
    </tr>
    <tr>
      <th>1356</th>
      <td>Albania</td>
      <td>60</td>
      <td>1357</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>573.53950</td>
      <td>534.15736</td>
      <td>511.87990</td>
      <td>539.858920</td>
    </tr>
    <tr>
      <th>1358</th>
      <td>Albania</td>
      <td>60</td>
      <td>1359</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>310.64808</td>
      <td>152.43148</td>
      <td>238.56770</td>
      <td>233.882420</td>
    </tr>
    <tr>
      <th>1366</th>
      <td>Albania</td>
      <td>60</td>
      <td>1367</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>312.36174</td>
      <td>235.43744</td>
      <td>280.62290</td>
      <td>276.140693</td>
    </tr>
    <tr>
      <th>1374</th>
      <td>Albania</td>
      <td>61</td>
      <td>1375</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>483.88380</td>
      <td>470.56310</td>
      <td>489.50018</td>
      <td>481.315693</td>
    </tr>
    <tr>
      <th>1379</th>
      <td>Albania</td>
      <td>61</td>
      <td>1380</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>372.26204</td>
      <td>347.54474</td>
      <td>388.51174</td>
      <td>369.439507</td>
    </tr>
    <tr>
      <th>1396</th>
      <td>Albania</td>
      <td>61</td>
      <td>1397</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>273.25908</td>
      <td>295.32844</td>
      <td>293.58448</td>
      <td>287.390667</td>
    </tr>
    <tr>
      <th>1404</th>
      <td>Albania</td>
      <td>61</td>
      <td>1405</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>394.46174</td>
      <td>425.41360</td>
      <td>457.04962</td>
      <td>425.641653</td>
    </tr>
    <tr>
      <th>1409</th>
      <td>Albania</td>
      <td>62</td>
      <td>1410</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>556.01340</td>
      <td>524.96352</td>
      <td>605.68818</td>
      <td>562.221700</td>
    </tr>
    <tr>
      <th>1410</th>
      <td>Albania</td>
      <td>62</td>
      <td>1411</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>305.35130</td>
      <td>271.52034</td>
      <td>397.74338</td>
      <td>324.871673</td>
    </tr>
    <tr>
      <th>1411</th>
      <td>Albania</td>
      <td>62</td>
      <td>1412</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>565.75012</td>
      <td>570.64588</td>
      <td>591.98060</td>
      <td>576.125533</td>
    </tr>
    <tr>
      <th>1415</th>
      <td>Albania</td>
      <td>62</td>
      <td>1416</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>376.62408</td>
      <td>490.64930</td>
      <td>423.48004</td>
      <td>430.251140</td>
    </tr>
    <tr>
      <th>1417</th>
      <td>Albania</td>
      <td>62</td>
      <td>1418</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>589.19610</td>
      <td>573.53286</td>
      <td>543.58448</td>
      <td>568.771147</td>
    </tr>
    <tr>
      <th>1420</th>
      <td>Albania</td>
      <td>62</td>
      <td>1421</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>414.71412</td>
      <td>376.09398</td>
      <td>416.95264</td>
      <td>402.586913</td>
    </tr>
    <tr>
      <th>1421</th>
      <td>Albania</td>
      <td>62</td>
      <td>1422</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>476.17232</td>
      <td>474.44538</td>
      <td>521.95078</td>
      <td>490.856160</td>
    </tr>
    <tr>
      <th>1422</th>
      <td>Albania</td>
      <td>62</td>
      <td>1423</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>289.07150</td>
      <td>285.23362</td>
      <td>357.45990</td>
      <td>310.588340</td>
    </tr>
    <tr>
      <th>1423</th>
      <td>Albania</td>
      <td>62</td>
      <td>1424</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>422.50350</td>
      <td>411.53994</td>
      <td>481.76052</td>
      <td>438.601320</td>
    </tr>
    <tr>
      <th>1429</th>
      <td>Albania</td>
      <td>62</td>
      <td>1430</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>506.39508</td>
      <td>467.99690</td>
      <td>501.34278</td>
      <td>491.911587</td>
    </tr>
    <tr>
      <th>1430</th>
      <td>Albania</td>
      <td>62</td>
      <td>1431</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>498.83940</td>
      <td>570.63634</td>
      <td>558.69078</td>
      <td>542.722173</td>
    </tr>
    <tr>
      <th>1431</th>
      <td>Albania</td>
      <td>62</td>
      <td>1432</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>Five or more times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>339.54666</td>
      <td>231.70420</td>
      <td>373.68518</td>
      <td>314.978680</td>
    </tr>
    <tr>
      <th>1432</th>
      <td>Albania</td>
      <td>63</td>
      <td>1433</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>367.97788</td>
      <td>290.56258</td>
      <td>350.27974</td>
      <td>336.273400</td>
    </tr>
    <tr>
      <th>1434</th>
      <td>Albania</td>
      <td>63</td>
      <td>1435</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>431.53920</td>
      <td>518.76002</td>
      <td>471.68968</td>
      <td>473.996300</td>
    </tr>
    <tr>
      <th>1439</th>
      <td>Albania</td>
      <td>63</td>
      <td>1440</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>506.47298</td>
      <td>435.12704</td>
      <td>463.76354</td>
      <td>468.454520</td>
    </tr>
    <tr>
      <th>1446</th>
      <td>Albania</td>
      <td>64</td>
      <td>1447</td>
      <td>8</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>432.00656</td>
      <td>438.46312</td>
      <td>438.77286</td>
      <td>436.414180</td>
    </tr>
    <tr>
      <th>1447</th>
      <td>Albania</td>
      <td>64</td>
      <td>1448</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>498.76152</td>
      <td>507.01206</td>
      <td>478.12384</td>
      <td>494.632473</td>
    </tr>
    <tr>
      <th>1448</th>
      <td>Albania</td>
      <td>64</td>
      <td>1449</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>406.06790</td>
      <td>426.13536</td>
      <td>373.21894</td>
      <td>401.807400</td>
    </tr>
    <tr>
      <th>1456</th>
      <td>Albania</td>
      <td>64</td>
      <td>1457</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>No</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>403.73112</td>
      <td>428.86198</td>
      <td>380.67884</td>
      <td>404.423980</td>
    </tr>
    <tr>
      <th>1457</th>
      <td>Albania</td>
      <td>64</td>
      <td>1458</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>355.28120</td>
      <td>376.81574</td>
      <td>380.95858</td>
      <td>371.018507</td>
    </tr>
    <tr>
      <th>1460</th>
      <td>Albania</td>
      <td>64</td>
      <td>1461</td>
      <td>8</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>395.47434</td>
      <td>317.39162</td>
      <td>359.41816</td>
      <td>357.428040</td>
    </tr>
    <tr>
      <th>1462</th>
      <td>Albania</td>
      <td>64</td>
      <td>1463</td>
      <td>8</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>332.61412</td>
      <td>266.54830</td>
      <td>318.66840</td>
      <td>305.943607</td>
    </tr>
    <tr>
      <th>1474</th>
      <td>Albania</td>
      <td>66</td>
      <td>1475</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>420.24456</td>
      <td>414.79268</td>
      <td>416.11342</td>
      <td>417.050220</td>
    </tr>
    <tr>
      <th>1477</th>
      <td>Albania</td>
      <td>66</td>
      <td>1478</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>421.80246</td>
      <td>495.41516</td>
      <td>429.44798</td>
      <td>448.888533</td>
    </tr>
    <tr>
      <th>1478</th>
      <td>Albania</td>
      <td>66</td>
      <td>1479</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>459.58094</td>
      <td>500.18102</td>
      <td>503.39424</td>
      <td>487.718733</td>
    </tr>
    <tr>
      <th>1481</th>
      <td>Albania</td>
      <td>66</td>
      <td>1482</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>345.31078</td>
      <td>347.91178</td>
      <td>401.19356</td>
      <td>364.805373</td>
    </tr>
    <tr>
      <th>1484</th>
      <td>Albania</td>
      <td>66</td>
      <td>1485</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>399.68064</td>
      <td>454.03160</td>
      <td>420.02984</td>
      <td>424.580693</td>
    </tr>
    <tr>
      <th>1485</th>
      <td>Albania</td>
      <td>66</td>
      <td>1486</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>404.97744</td>
      <td>375.53264</td>
      <td>463.95002</td>
      <td>414.820033</td>
    </tr>
    <tr>
      <th>1491</th>
      <td>Albania</td>
      <td>66</td>
      <td>1492</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>438.54960</td>
      <td>492.39678</td>
      <td>425.53152</td>
      <td>452.159300</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>481573</th>
      <td>Vietnam</td>
      <td>33</td>
      <td>1043</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>502.26670</td>
      <td>511.46230</td>
      <td>570.81314</td>
      <td>528.180713</td>
    </tr>
    <tr>
      <th>481579</th>
      <td>Vietnam</td>
      <td>33</td>
      <td>1049</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>510.75714</td>
      <td>521.70682</td>
      <td>528.47818</td>
      <td>520.314047</td>
    </tr>
    <tr>
      <th>481581</th>
      <td>Vietnam</td>
      <td>33</td>
      <td>1051</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>442.28854</td>
      <td>457.68542</td>
      <td>499.94404</td>
      <td>466.639333</td>
    </tr>
    <tr>
      <th>481601</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1071</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>512.23710</td>
      <td>591.28840</td>
      <td>566.71020</td>
      <td>556.745233</td>
    </tr>
    <tr>
      <th>481608</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1078</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>447.74108</td>
      <td>470.40272</td>
      <td>519.33980</td>
      <td>479.161200</td>
    </tr>
    <tr>
      <th>481613</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1083</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>499.22884</td>
      <td>521.30966</td>
      <td>504.04702</td>
      <td>508.195173</td>
    </tr>
    <tr>
      <th>481615</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1085</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>441.50958</td>
      <td>458.47976</td>
      <td>475.13988</td>
      <td>458.376407</td>
    </tr>
    <tr>
      <th>481618</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1088</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>468.77240</td>
      <td>469.28236</td>
      <td>485.77024</td>
      <td>474.608333</td>
    </tr>
    <tr>
      <th>481621</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1091</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>430.05920</td>
      <td>460.13784</td>
      <td>487.91496</td>
      <td>459.370667</td>
    </tr>
    <tr>
      <th>481622</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1092</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>501.56566</td>
      <td>528.94472</td>
      <td>534.81910</td>
      <td>521.776493</td>
    </tr>
    <tr>
      <th>481623</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1093</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>458.02304</td>
      <td>501.53134</td>
      <td>507.21746</td>
      <td>488.923947</td>
    </tr>
    <tr>
      <th>481624</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1094</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>438.08228</td>
      <td>452.92032</td>
      <td>448.09772</td>
      <td>446.366773</td>
    </tr>
    <tr>
      <th>481625</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1095</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>467.44824</td>
      <td>493.34998</td>
      <td>494.53560</td>
      <td>485.111273</td>
    </tr>
    <tr>
      <th>481630</th>
      <td>Vietnam</td>
      <td>34</td>
      <td>1100</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>591.68874</td>
      <td>523.33110</td>
      <td>568.48192</td>
      <td>561.167253</td>
    </tr>
    <tr>
      <th>481645</th>
      <td>Vietnam</td>
      <td>35</td>
      <td>1115</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>543.47250</td>
      <td>546.48930</td>
      <td>569.04138</td>
      <td>553.001060</td>
    </tr>
    <tr>
      <th>481664</th>
      <td>Vietnam</td>
      <td>35</td>
      <td>1134</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>512.15922</td>
      <td>569.36544</td>
      <td>579.11226</td>
      <td>553.545640</td>
    </tr>
    <tr>
      <th>481668</th>
      <td>Vietnam</td>
      <td>36</td>
      <td>1138</td>
      <td>96</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>422.03616</td>
      <td>389.72706</td>
      <td>443.80828</td>
      <td>418.523833</td>
    </tr>
    <tr>
      <th>481690</th>
      <td>Vietnam</td>
      <td>36</td>
      <td>1160</td>
      <td>96</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>397.73330</td>
      <td>476.74888</td>
      <td>435.22940</td>
      <td>436.570527</td>
    </tr>
    <tr>
      <th>481701</th>
      <td>Vietnam</td>
      <td>37</td>
      <td>1171</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>365.09580</td>
      <td>369.99918</td>
      <td>410.14546</td>
      <td>381.746813</td>
    </tr>
    <tr>
      <th>481702</th>
      <td>Vietnam</td>
      <td>37</td>
      <td>1172</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>396.25332</td>
      <td>420.68212</td>
      <td>396.53114</td>
      <td>404.488860</td>
    </tr>
    <tr>
      <th>481706</th>
      <td>Vietnam</td>
      <td>37</td>
      <td>1176</td>
      <td>9</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>400.07012</td>
      <td>378.01866</td>
      <td>437.56062</td>
      <td>405.216467</td>
    </tr>
    <tr>
      <th>481720</th>
      <td>Vietnam</td>
      <td>38</td>
      <td>1190</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>410.27416</td>
      <td>419.23862</td>
      <td>443.24878</td>
      <td>424.253853</td>
    </tr>
    <tr>
      <th>481723</th>
      <td>Vietnam</td>
      <td>38</td>
      <td>1193</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>Five or more times</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>333.62672</td>
      <td>387.78616</td>
      <td>359.32488</td>
      <td>360.245920</td>
    </tr>
    <tr>
      <th>481746</th>
      <td>Vietnam</td>
      <td>39</td>
      <td>1216</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>610.38322</td>
      <td>559.73940</td>
      <td>601.95822</td>
      <td>590.693613</td>
    </tr>
    <tr>
      <th>481761</th>
      <td>Vietnam</td>
      <td>39</td>
      <td>1231</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>505.61614</td>
      <td>504.31146</td>
      <td>515.98282</td>
      <td>508.636807</td>
    </tr>
    <tr>
      <th>481762</th>
      <td>Vietnam</td>
      <td>39</td>
      <td>1232</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>568.32060</td>
      <td>588.11118</td>
      <td>591.51434</td>
      <td>582.648707</td>
    </tr>
    <tr>
      <th>481809</th>
      <td>Vietnam</td>
      <td>40</td>
      <td>1279</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>535.13788</td>
      <td>470.40272</td>
      <td>506.84444</td>
      <td>504.128347</td>
    </tr>
    <tr>
      <th>481847</th>
      <td>Vietnam</td>
      <td>42</td>
      <td>1317</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>505.14878</td>
      <td>536.24268</td>
      <td>535.19208</td>
      <td>525.527847</td>
    </tr>
    <tr>
      <th>481893</th>
      <td>Vietnam</td>
      <td>43</td>
      <td>1363</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>442.44430</td>
      <td>513.06622</td>
      <td>488.56770</td>
      <td>481.359407</td>
    </tr>
    <tr>
      <th>481897</th>
      <td>Vietnam</td>
      <td>43</td>
      <td>1367</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>408.79422</td>
      <td>473.88936</td>
      <td>425.34502</td>
      <td>436.009533</td>
    </tr>
    <tr>
      <th>481902</th>
      <td>Vietnam</td>
      <td>43</td>
      <td>1372</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>620.97680</td>
      <td>573.85362</td>
      <td>596.73632</td>
      <td>597.188913</td>
    </tr>
    <tr>
      <th>481938</th>
      <td>Vietnam</td>
      <td>44</td>
      <td>1408</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>618.95154</td>
      <td>553.64464</td>
      <td>632.54382</td>
      <td>601.713333</td>
    </tr>
    <tr>
      <th>481945</th>
      <td>Vietnam</td>
      <td>45</td>
      <td>1415</td>
      <td>96</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>365.79686</td>
      <td>341.44994</td>
      <td>365.47932</td>
      <td>357.575373</td>
    </tr>
    <tr>
      <th>481948</th>
      <td>Vietnam</td>
      <td>45</td>
      <td>1418</td>
      <td>96</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>400.53746</td>
      <td>433.06182</td>
      <td>415.08764</td>
      <td>416.228973</td>
    </tr>
    <tr>
      <th>481957</th>
      <td>Vietnam</td>
      <td>45</td>
      <td>1427</td>
      <td>96</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>381.92086</td>
      <td>409.13412</td>
      <td>412.56992</td>
      <td>401.208300</td>
    </tr>
    <tr>
      <th>481966</th>
      <td>Vietnam</td>
      <td>45</td>
      <td>1436</td>
      <td>96</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>390.09970</td>
      <td>421.30604</td>
      <td>375.17716</td>
      <td>395.527633</td>
    </tr>
    <tr>
      <th>481967</th>
      <td>Vietnam</td>
      <td>45</td>
      <td>1437</td>
      <td>96</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>396.87646</td>
      <td>404.80362</td>
      <td>404.64380</td>
      <td>402.107960</td>
    </tr>
    <tr>
      <th>482033</th>
      <td>Vietnam</td>
      <td>48</td>
      <td>1503</td>
      <td>8</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>394.77332</td>
      <td>389.40628</td>
      <td>433.17792</td>
      <td>405.785840</td>
    </tr>
    <tr>
      <th>482051</th>
      <td>Vietnam</td>
      <td>49</td>
      <td>1521</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>575.48682</td>
      <td>531.35056</td>
      <td>579.20552</td>
      <td>562.014300</td>
    </tr>
    <tr>
      <th>482061</th>
      <td>Vietnam</td>
      <td>49</td>
      <td>1531</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>546.19878</td>
      <td>504.86744</td>
      <td>584.42746</td>
      <td>545.164560</td>
    </tr>
    <tr>
      <th>482063</th>
      <td>Vietnam</td>
      <td>49</td>
      <td>1533</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>560.37544</td>
      <td>535.68108</td>
      <td>602.70422</td>
      <td>566.253580</td>
    </tr>
    <tr>
      <th>482072</th>
      <td>Vietnam</td>
      <td>49</td>
      <td>1542</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>547.13350</td>
      <td>545.53612</td>
      <td>546.56844</td>
      <td>546.412687</td>
    </tr>
    <tr>
      <th>482107</th>
      <td>Vietnam</td>
      <td>50</td>
      <td>1577</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>595.50552</td>
      <td>564.87188</td>
      <td>557.85152</td>
      <td>572.742973</td>
    </tr>
    <tr>
      <th>482115</th>
      <td>Vietnam</td>
      <td>51</td>
      <td>1585</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>424.21718</td>
      <td>497.71866</td>
      <td>533.51360</td>
      <td>485.149813</td>
    </tr>
    <tr>
      <th>482117</th>
      <td>Vietnam</td>
      <td>51</td>
      <td>1587</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>586.08038</td>
      <td>530.44426</td>
      <td>601.21224</td>
      <td>572.578960</td>
    </tr>
    <tr>
      <th>482136</th>
      <td>Vietnam</td>
      <td>51</td>
      <td>1606</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>484.97428</td>
      <td>473.28974</td>
      <td>538.54904</td>
      <td>498.937687</td>
    </tr>
    <tr>
      <th>482159</th>
      <td>Vietnam</td>
      <td>53</td>
      <td>1629</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>433.87600</td>
      <td>428.93142</td>
      <td>485.58374</td>
      <td>449.463720</td>
    </tr>
    <tr>
      <th>482174</th>
      <td>Vietnam</td>
      <td>53</td>
      <td>1644</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>436.44648</td>
      <td>466.74056</td>
      <td>453.31966</td>
      <td>452.168900</td>
    </tr>
    <tr>
      <th>482204</th>
      <td>Vietnam</td>
      <td>54</td>
      <td>1674</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>463.08614</td>
      <td>445.94342</td>
      <td>456.21038</td>
      <td>455.079980</td>
    </tr>
    <tr>
      <th>482218</th>
      <td>Vietnam</td>
      <td>54</td>
      <td>1688</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>539.88938</td>
      <td>506.81104</td>
      <td>562.42072</td>
      <td>536.373713</td>
    </tr>
    <tr>
      <th>482239</th>
      <td>Vietnam</td>
      <td>55</td>
      <td>1709</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>398.04486</td>
      <td>451.01322</td>
      <td>442.87580</td>
      <td>430.644627</td>
    </tr>
    <tr>
      <th>482241</th>
      <td>Vietnam</td>
      <td>55</td>
      <td>1711</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>492.29632</td>
      <td>459.81706</td>
      <td>533.51360</td>
      <td>495.208993</td>
    </tr>
    <tr>
      <th>482250</th>
      <td>Vietnam</td>
      <td>55</td>
      <td>1720</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>524.70010</td>
      <td>534.71872</td>
      <td>563.72622</td>
      <td>541.048347</td>
    </tr>
    <tr>
      <th>482254</th>
      <td>Vietnam</td>
      <td>55</td>
      <td>1724</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>502.18882</td>
      <td>522.26284</td>
      <td>540.78702</td>
      <td>521.746227</td>
    </tr>
    <tr>
      <th>482255</th>
      <td>Vietnam</td>
      <td>55</td>
      <td>1725</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>502.81194</td>
      <td>483.47444</td>
      <td>488.84744</td>
      <td>491.711273</td>
    </tr>
    <tr>
      <th>482263</th>
      <td>Vietnam</td>
      <td>56</td>
      <td>1733</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>458.10094</td>
      <td>480.87928</td>
      <td>466.65422</td>
      <td>468.544813</td>
    </tr>
    <tr>
      <th>482265</th>
      <td>Vietnam</td>
      <td>56</td>
      <td>1735</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>475.54914</td>
      <td>413.54478</td>
      <td>426.18428</td>
      <td>438.426067</td>
    </tr>
    <tr>
      <th>482297</th>
      <td>Vietnam</td>
      <td>57</td>
      <td>1767</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>499.61830</td>
      <td>612.09930</td>
      <td>547.31442</td>
      <td>553.010673</td>
    </tr>
    <tr>
      <th>482312</th>
      <td>Vietnam</td>
      <td>57</td>
      <td>1782</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>565.51642</td>
      <td>629.66902</td>
      <td>605.12870</td>
      <td>600.104713</td>
    </tr>
    <tr>
      <th>482322</th>
      <td>Vietnam</td>
      <td>57</td>
      <td>1792</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>510.75712</td>
      <td>548.91314</td>
      <td>518.87356</td>
      <td>526.181273</td>
    </tr>
    <tr>
      <th>482336</th>
      <td>Vietnam</td>
      <td>58</td>
      <td>1806</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>524.38852</td>
      <td>566.79654</td>
      <td>560.18276</td>
      <td>550.455940</td>
    </tr>
    <tr>
      <th>482340</th>
      <td>Vietnam</td>
      <td>58</td>
      <td>1810</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>469.70712</td>
      <td>459.90950</td>
      <td>496.58708</td>
      <td>475.401233</td>
    </tr>
    <tr>
      <th>482341</th>
      <td>Vietnam</td>
      <td>58</td>
      <td>1811</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>549.93768</td>
      <td>521.08566</td>
      <td>570.44012</td>
      <td>547.154487</td>
    </tr>
    <tr>
      <th>482390</th>
      <td>Vietnam</td>
      <td>59</td>
      <td>1860</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>485.44168</td>
      <td>440.89116</td>
      <td>510.20142</td>
      <td>478.844753</td>
    </tr>
    <tr>
      <th>482405</th>
      <td>Vietnam</td>
      <td>60</td>
      <td>1875</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>No</td>
      <td>415.88254</td>
      <td>410.34456</td>
      <td>434.48342</td>
      <td>420.236840</td>
    </tr>
    <tr>
      <th>482422</th>
      <td>Vietnam</td>
      <td>60</td>
      <td>1892</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>450.31158</td>
      <td>489.21954</td>
      <td>424.69228</td>
      <td>454.741133</td>
    </tr>
    <tr>
      <th>482437</th>
      <td>Vietnam</td>
      <td>61</td>
      <td>1907</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>532.56736</td>
      <td>578.57946</td>
      <td>557.85156</td>
      <td>556.332793</td>
    </tr>
    <tr>
      <th>482450</th>
      <td>Vietnam</td>
      <td>61</td>
      <td>1920</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>568.63216</td>
      <td>616.70632</td>
      <td>543.58446</td>
      <td>576.307647</td>
    </tr>
    <tr>
      <th>482454</th>
      <td>Vietnam</td>
      <td>61</td>
      <td>1924</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>587.63826</td>
      <td>588.27000</td>
      <td>593.19284</td>
      <td>589.700367</td>
    </tr>
    <tr>
      <th>482463</th>
      <td>Vietnam</td>
      <td>62</td>
      <td>1933</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>424.13928</td>
      <td>434.31520</td>
      <td>483.62552</td>
      <td>447.360000</td>
    </tr>
    <tr>
      <th>482466</th>
      <td>Vietnam</td>
      <td>62</td>
      <td>1936</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>531.47688</td>
      <td>507.37240</td>
      <td>521.11154</td>
      <td>519.986940</td>
    </tr>
    <tr>
      <th>482470</th>
      <td>Vietnam</td>
      <td>62</td>
      <td>1940</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>412.14364</td>
      <td>393.49618</td>
      <td>432.80492</td>
      <td>412.814913</td>
    </tr>
    <tr>
      <th>482499</th>
      <td>Vietnam</td>
      <td>63</td>
      <td>1969</td>
      <td>96</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>379.19458</td>
      <td>397.42572</td>
      <td>445.11376</td>
      <td>407.244687</td>
    </tr>
    <tr>
      <th>482502</th>
      <td>Vietnam</td>
      <td>63</td>
      <td>1972</td>
      <td>96</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>344.37608</td>
      <td>351.79502</td>
      <td>423.66652</td>
      <td>373.279207</td>
    </tr>
    <tr>
      <th>482506</th>
      <td>Vietnam</td>
      <td>63</td>
      <td>1976</td>
      <td>96</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>No</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>334.01622</td>
      <td>349.46940</td>
      <td>340.86160</td>
      <td>341.449073</td>
    </tr>
    <tr>
      <th>482509</th>
      <td>Vietnam</td>
      <td>63</td>
      <td>1979</td>
      <td>96</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>410.11840</td>
      <td>437.20218</td>
      <td>477.65762</td>
      <td>441.659400</td>
    </tr>
    <tr>
      <th>482511</th>
      <td>Vietnam</td>
      <td>63</td>
      <td>1981</td>
      <td>96</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>320.46268</td>
      <td>369.99920</td>
      <td>382.07756</td>
      <td>357.513147</td>
    </tr>
    <tr>
      <th>482540</th>
      <td>Vietnam</td>
      <td>64</td>
      <td>2010</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>366.73158</td>
      <td>466.42288</td>
      <td>402.59232</td>
      <td>411.915593</td>
    </tr>
    <tr>
      <th>482551</th>
      <td>Vietnam</td>
      <td>65</td>
      <td>2021</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>550.24926</td>
      <td>546.26672</td>
      <td>570.06714</td>
      <td>555.527707</td>
    </tr>
    <tr>
      <th>482558</th>
      <td>Vietnam</td>
      <td>65</td>
      <td>2028</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>531.08740</td>
      <td>547.60134</td>
      <td>513.18538</td>
      <td>530.624707</td>
    </tr>
    <tr>
      <th>482559</th>
      <td>Vietnam</td>
      <td>65</td>
      <td>2029</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>567.30800</td>
      <td>527.98238</td>
      <td>591.60762</td>
      <td>562.299333</td>
    </tr>
    <tr>
      <th>482566</th>
      <td>Vietnam</td>
      <td>65</td>
      <td>2036</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>601.89282</td>
      <td>553.39978</td>
      <td>552.07012</td>
      <td>569.120907</td>
    </tr>
    <tr>
      <th>482572</th>
      <td>Vietnam</td>
      <td>65</td>
      <td>2042</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>580.93938</td>
      <td>509.69804</td>
      <td>547.12792</td>
      <td>545.921780</td>
    </tr>
    <tr>
      <th>482582</th>
      <td>Vietnam</td>
      <td>65</td>
      <td>2052</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>493.15314</td>
      <td>507.09150</td>
      <td>488.94070</td>
      <td>496.395113</td>
    </tr>
    <tr>
      <th>482594</th>
      <td>Vietnam</td>
      <td>66</td>
      <td>2064</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>567.69746</td>
      <td>524.40746</td>
      <td>571.55912</td>
      <td>554.554680</td>
    </tr>
    <tr>
      <th>482600</th>
      <td>Vietnam</td>
      <td>66</td>
      <td>2070</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>536.61786</td>
      <td>536.48102</td>
      <td>555.14732</td>
      <td>542.748733</td>
    </tr>
    <tr>
      <th>482606</th>
      <td>Vietnam</td>
      <td>66</td>
      <td>2076</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>461.76198</td>
      <td>517.73526</td>
      <td>556.07982</td>
      <td>511.859020</td>
    </tr>
    <tr>
      <th>482626</th>
      <td>Vietnam</td>
      <td>67</td>
      <td>2096</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>543.31674</td>
      <td>569.36546</td>
      <td>547.03470</td>
      <td>553.238967</td>
    </tr>
    <tr>
      <th>482629</th>
      <td>Vietnam</td>
      <td>67</td>
      <td>2099</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>371.87258</td>
      <td>407.16732</td>
      <td>441.38384</td>
      <td>406.807913</td>
    </tr>
    <tr>
      <th>482633</th>
      <td>Vietnam</td>
      <td>67</td>
      <td>2103</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>488.63530</td>
      <td>469.11960</td>
      <td>503.58078</td>
      <td>487.111893</td>
    </tr>
    <tr>
      <th>482650</th>
      <td>Vietnam</td>
      <td>67</td>
      <td>2120</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>499.07308</td>
      <td>588.27002</td>
      <td>556.54606</td>
      <td>547.963053</td>
    </tr>
    <tr>
      <th>482692</th>
      <td>Vietnam</td>
      <td>69</td>
      <td>2162</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>454.43994</td>
      <td>427.25810</td>
      <td>471.22344</td>
      <td>450.973827</td>
    </tr>
    <tr>
      <th>482702</th>
      <td>Vietnam</td>
      <td>69</td>
      <td>2172</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>562.24490</td>
      <td>576.03764</td>
      <td>609.60462</td>
      <td>582.629053</td>
    </tr>
    <tr>
      <th>482709</th>
      <td>Vietnam</td>
      <td>69</td>
      <td>2179</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>451.32418</td>
      <td>481.67362</td>
      <td>500.50352</td>
      <td>477.833773</td>
    </tr>
    <tr>
      <th>482731</th>
      <td>Vietnam</td>
      <td>70</td>
      <td>2201</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>490.58264</td>
      <td>494.54142</td>
      <td>466.00148</td>
      <td>483.708513</td>
    </tr>
    <tr>
      <th>482734</th>
      <td>Vietnam</td>
      <td>70</td>
      <td>2204</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>560.29756</td>
      <td>595.02166</td>
      <td>615.38604</td>
      <td>590.235087</td>
    </tr>
    <tr>
      <th>482736</th>
      <td>Vietnam</td>
      <td>70</td>
      <td>2206</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>500.94250</td>
      <td>561.10460</td>
      <td>538.36252</td>
      <td>533.469873</td>
    </tr>
    <tr>
      <th>482746</th>
      <td>Vietnam</td>
      <td>70</td>
      <td>2216</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>479.83330</td>
      <td>606.22142</td>
      <td>533.51360</td>
      <td>539.856107</td>
    </tr>
    <tr>
      <th>482747</th>
      <td>Vietnam</td>
      <td>70</td>
      <td>2217</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>459.58092</td>
      <td>469.44122</td>
      <td>490.80568</td>
      <td>473.275940</td>
    </tr>
    <tr>
      <th>482750</th>
      <td>Vietnam</td>
      <td>70</td>
      <td>2220</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>507.71928</td>
      <td>541.13428</td>
      <td>546.75494</td>
      <td>531.869500</td>
    </tr>
    <tr>
      <th>482753</th>
      <td>Vietnam</td>
      <td>70</td>
      <td>2223</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>395.94174</td>
      <td>413.54480</td>
      <td>451.45466</td>
      <td>420.313733</td>
    </tr>
    <tr>
      <th>482760</th>
      <td>Vietnam</td>
      <td>71</td>
      <td>2230</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>485.36376</td>
      <td>506.05892</td>
      <td>469.07870</td>
      <td>486.833793</td>
    </tr>
    <tr>
      <th>482763</th>
      <td>Vietnam</td>
      <td>71</td>
      <td>2233</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>595.27184</td>
      <td>550.43686</td>
      <td>570.99962</td>
      <td>572.236107</td>
    </tr>
    <tr>
      <th>482798</th>
      <td>Vietnam</td>
      <td>72</td>
      <td>2268</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>492.53000</td>
      <td>544.66238</td>
      <td>502.55500</td>
      <td>513.249127</td>
    </tr>
    <tr>
      <th>482803</th>
      <td>Vietnam</td>
      <td>72</td>
      <td>2273</td>
      <td>9</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>447.74108</td>
      <td>472.61844</td>
      <td>487.63522</td>
      <td>469.331580</td>
    </tr>
    <tr>
      <th>482811</th>
      <td>Vietnam</td>
      <td>72</td>
      <td>2281</td>
      <td>9</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>425.61926</td>
      <td>497.24208</td>
      <td>444.74074</td>
      <td>455.867360</td>
    </tr>
    <tr>
      <th>482820</th>
      <td>Vietnam</td>
      <td>72</td>
      <td>2290</td>
      <td>9</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>367.43262</td>
      <td>407.96160</td>
      <td>400.35436</td>
      <td>391.916193</td>
    </tr>
    <tr>
      <th>482834</th>
      <td>Vietnam</td>
      <td>73</td>
      <td>2304</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>473.13444</td>
      <td>462.54366</td>
      <td>469.63820</td>
      <td>468.438767</td>
    </tr>
    <tr>
      <th>482845</th>
      <td>Vietnam</td>
      <td>73</td>
      <td>2315</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>498.91726</td>
      <td>465.43068</td>
      <td>492.39090</td>
      <td>485.579613</td>
    </tr>
    <tr>
      <th>482862</th>
      <td>Vietnam</td>
      <td>74</td>
      <td>2332</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>392.90386</td>
      <td>357.97002</td>
      <td>411.54422</td>
      <td>387.472700</td>
    </tr>
    <tr>
      <th>482873</th>
      <td>Vietnam</td>
      <td>74</td>
      <td>2343</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>435.43386</td>
      <td>416.35162</td>
      <td>374.61768</td>
      <td>408.801053</td>
    </tr>
    <tr>
      <th>482878</th>
      <td>Vietnam</td>
      <td>74</td>
      <td>2348</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>466.51346</td>
      <td>442.73564</td>
      <td>424.69230</td>
      <td>444.647133</td>
    </tr>
    <tr>
      <th>482892</th>
      <td>Vietnam</td>
      <td>75</td>
      <td>2362</td>
      <td>8</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>362.29164</td>
      <td>307.52770</td>
      <td>419.93658</td>
      <td>363.251973</td>
    </tr>
    <tr>
      <th>482893</th>
      <td>Vietnam</td>
      <td>75</td>
      <td>2363</td>
      <td>9</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>370.15892</td>
      <td>351.39406</td>
      <td>428.14248</td>
      <td>383.231820</td>
    </tr>
    <tr>
      <th>482896</th>
      <td>Vietnam</td>
      <td>75</td>
      <td>2366</td>
      <td>9</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>458.64620</td>
      <td>516.46438</td>
      <td>527.54570</td>
      <td>500.885427</td>
    </tr>
    <tr>
      <th>482899</th>
      <td>Vietnam</td>
      <td>75</td>
      <td>2369</td>
      <td>8</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>324.04580</td>
      <td>285.63456</td>
      <td>384.59532</td>
      <td>331.425227</td>
    </tr>
    <tr>
      <th>482911</th>
      <td>Vietnam</td>
      <td>76</td>
      <td>2381</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>488.24584</td>
      <td>539.18166</td>
      <td>539.29504</td>
      <td>522.240847</td>
    </tr>
    <tr>
      <th>482915</th>
      <td>Vietnam</td>
      <td>76</td>
      <td>2385</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>484.58484</td>
      <td>496.92436</td>
      <td>507.77696</td>
      <td>496.428720</td>
    </tr>
    <tr>
      <th>482981</th>
      <td>Vietnam</td>
      <td>79</td>
      <td>2451</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>455.68624</td>
      <td>489.14012</td>
      <td>496.58708</td>
      <td>480.471147</td>
    </tr>
    <tr>
      <th>482992</th>
      <td>Vietnam</td>
      <td>79</td>
      <td>2462</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>429.74762</td>
      <td>461.33926</td>
      <td>459.94032</td>
      <td>450.342400</td>
    </tr>
    <tr>
      <th>483037</th>
      <td>Vietnam</td>
      <td>80</td>
      <td>2507</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>662.88362</td>
      <td>662.61744</td>
      <td>667.60538</td>
      <td>664.368813</td>
    </tr>
    <tr>
      <th>483043</th>
      <td>Vietnam</td>
      <td>80</td>
      <td>2513</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>578.99202</td>
      <td>527.74180</td>
      <td>510.29468</td>
      <td>539.009500</td>
    </tr>
    <tr>
      <th>483048</th>
      <td>Vietnam</td>
      <td>81</td>
      <td>2518</td>
      <td>96</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>429.04660</td>
      <td>412.34188</td>
      <td>520.45878</td>
      <td>453.949087</td>
    </tr>
    <tr>
      <th>483049</th>
      <td>Vietnam</td>
      <td>81</td>
      <td>2519</td>
      <td>96</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>420.94566</td>
      <td>389.21590</td>
      <td>477.93734</td>
      <td>429.366300</td>
    </tr>
    <tr>
      <th>483059</th>
      <td>Vietnam</td>
      <td>81</td>
      <td>2529</td>
      <td>96</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>430.21498</td>
      <td>485.08914</td>
      <td>493.88288</td>
      <td>469.729000</td>
    </tr>
    <tr>
      <th>483067</th>
      <td>Vietnam</td>
      <td>81</td>
      <td>2537</td>
      <td>96</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>512.54868</td>
      <td>542.04116</td>
      <td>563.53974</td>
      <td>539.376527</td>
    </tr>
    <tr>
      <th>483090</th>
      <td>Vietnam</td>
      <td>82</td>
      <td>2560</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>664.36360</td>
      <td>625.92030</td>
      <td>686.72136</td>
      <td>659.001753</td>
    </tr>
    <tr>
      <th>483115</th>
      <td>Vietnam</td>
      <td>83</td>
      <td>2585</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>555.70182</td>
      <td>560.94576</td>
      <td>626.20292</td>
      <td>580.950167</td>
    </tr>
    <tr>
      <th>483128</th>
      <td>Vietnam</td>
      <td>83</td>
      <td>2598</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>541.99250</td>
      <td>525.36066</td>
      <td>573.79710</td>
      <td>547.050087</td>
    </tr>
    <tr>
      <th>483131</th>
      <td>Vietnam</td>
      <td>83</td>
      <td>2601</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>549.23664</td>
      <td>528.54374</td>
      <td>571.37260</td>
      <td>549.717660</td>
    </tr>
    <tr>
      <th>483142</th>
      <td>Vietnam</td>
      <td>83</td>
      <td>2612</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>536.15050</td>
      <td>570.31862</td>
      <td>576.12828</td>
      <td>560.865800</td>
    </tr>
    <tr>
      <th>483152</th>
      <td>Vietnam</td>
      <td>84</td>
      <td>2622</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>432.94128</td>
      <td>480.87930</td>
      <td>444.55428</td>
      <td>452.791620</td>
    </tr>
    <tr>
      <th>483157</th>
      <td>Vietnam</td>
      <td>84</td>
      <td>2627</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>562.71226</td>
      <td>488.34580</td>
      <td>569.88064</td>
      <td>540.312900</td>
    </tr>
    <tr>
      <th>483174</th>
      <td>Vietnam</td>
      <td>84</td>
      <td>2644</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>496.65836</td>
      <td>498.67182</td>
      <td>521.01828</td>
      <td>505.449487</td>
    </tr>
    <tr>
      <th>483179</th>
      <td>Vietnam</td>
      <td>84</td>
      <td>2649</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>NaN</td>
      <td>Other language</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>448.98736</td>
      <td>435.43792</td>
      <td>418.44460</td>
      <td>434.289960</td>
    </tr>
    <tr>
      <th>483187</th>
      <td>Vietnam</td>
      <td>85</td>
      <td>2657</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>477.41862</td>
      <td>502.07956</td>
      <td>516.91530</td>
      <td>498.804493</td>
    </tr>
    <tr>
      <th>483210</th>
      <td>Vietnam</td>
      <td>85</td>
      <td>2680</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>525.47904</td>
      <td>576.74066</td>
      <td>550.85786</td>
      <td>551.025853</td>
    </tr>
    <tr>
      <th>483222</th>
      <td>Vietnam</td>
      <td>86</td>
      <td>2692</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>538.56522</td>
      <td>420.68214</td>
      <td>511.87988</td>
      <td>490.375747</td>
    </tr>
    <tr>
      <th>483229</th>
      <td>Vietnam</td>
      <td>86</td>
      <td>2699</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>513.63918</td>
      <td>541.08800</td>
      <td>533.51362</td>
      <td>529.413600</td>
    </tr>
    <tr>
      <th>483230</th>
      <td>Vietnam</td>
      <td>86</td>
      <td>2700</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>521.50648</td>
      <td>538.54622</td>
      <td>538.08280</td>
      <td>532.711833</td>
    </tr>
    <tr>
      <th>483268</th>
      <td>Vietnam</td>
      <td>88</td>
      <td>2738</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>433.56442</td>
      <td>448.75022</td>
      <td>459.10108</td>
      <td>447.138573</td>
    </tr>
    <tr>
      <th>483303</th>
      <td>Vietnam</td>
      <td>89</td>
      <td>2773</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>497.35942</td>
      <td>495.98476</td>
      <td>560.36926</td>
      <td>517.904480</td>
    </tr>
    <tr>
      <th>483305</th>
      <td>Vietnam</td>
      <td>89</td>
      <td>2775</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>575.87630</td>
      <td>593.51244</td>
      <td>628.53414</td>
      <td>599.307627</td>
    </tr>
    <tr>
      <th>483314</th>
      <td>Vietnam</td>
      <td>89</td>
      <td>2784</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>475.70494</td>
      <td>514.63748</td>
      <td>519.43306</td>
      <td>503.258493</td>
    </tr>
    <tr>
      <th>483336</th>
      <td>Vietnam</td>
      <td>90</td>
      <td>2806</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>608.59168</td>
      <td>578.82570</td>
      <td>584.33418</td>
      <td>590.583853</td>
    </tr>
    <tr>
      <th>483357</th>
      <td>Vietnam</td>
      <td>90</td>
      <td>2827</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>609.99378</td>
      <td>541.85602</td>
      <td>573.98360</td>
      <td>575.277800</td>
    </tr>
    <tr>
      <th>483375</th>
      <td>Vietnam</td>
      <td>91</td>
      <td>2845</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>459.03568</td>
      <td>470.55324</td>
      <td>528.66468</td>
      <td>486.084533</td>
    </tr>
    <tr>
      <th>483390</th>
      <td>Vietnam</td>
      <td>91</td>
      <td>2860</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>446.57268</td>
      <td>473.73048</td>
      <td>497.61284</td>
      <td>472.638667</td>
    </tr>
    <tr>
      <th>483407</th>
      <td>Vietnam</td>
      <td>92</td>
      <td>2877</td>
      <td>7</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>276.21906</td>
      <td>322.68444</td>
      <td>351.11900</td>
      <td>316.674167</td>
    </tr>
    <tr>
      <th>483416</th>
      <td>Vietnam</td>
      <td>92</td>
      <td>2886</td>
      <td>9</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>394.77334</td>
      <td>409.45490</td>
      <td>444.18128</td>
      <td>416.136507</td>
    </tr>
    <tr>
      <th>483418</th>
      <td>Vietnam</td>
      <td>92</td>
      <td>2888</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>378.33772</td>
      <td>383.95302</td>
      <td>414.80794</td>
      <td>392.366227</td>
    </tr>
    <tr>
      <th>483435</th>
      <td>Vietnam</td>
      <td>92</td>
      <td>2905</td>
      <td>9</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>397.42174</td>
      <td>409.29452</td>
      <td>423.85306</td>
      <td>410.189773</td>
    </tr>
    <tr>
      <th>483439</th>
      <td>Vietnam</td>
      <td>92</td>
      <td>2909</td>
      <td>7</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>333.00358</td>
      <td>326.77434</td>
      <td>356.62066</td>
      <td>338.799527</td>
    </tr>
    <tr>
      <th>483478</th>
      <td>Vietnam</td>
      <td>94</td>
      <td>2948</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>470.64184</td>
      <td>370.64076</td>
      <td>411.91720</td>
      <td>417.733267</td>
    </tr>
    <tr>
      <th>483484</th>
      <td>Vietnam</td>
      <td>95</td>
      <td>2954</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>485.59746</td>
      <td>445.22164</td>
      <td>492.29766</td>
      <td>474.372253</td>
    </tr>
    <tr>
      <th>483485</th>
      <td>Vietnam</td>
      <td>95</td>
      <td>2955</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>481.54696</td>
      <td>462.38326</td>
      <td>517.66132</td>
      <td>487.197180</td>
    </tr>
    <tr>
      <th>483488</th>
      <td>Vietnam</td>
      <td>95</td>
      <td>2958</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>500.55304</td>
      <td>548.23680</td>
      <td>551.69712</td>
      <td>533.495653</td>
    </tr>
    <tr>
      <th>483504</th>
      <td>Vietnam</td>
      <td>95</td>
      <td>2974</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>590.13084</td>
      <td>551.23880</td>
      <td>553.65536</td>
      <td>565.008333</td>
    </tr>
    <tr>
      <th>483506</th>
      <td>Vietnam</td>
      <td>95</td>
      <td>2976</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>420.40038</td>
      <td>503.60328</td>
      <td>457.14286</td>
      <td>460.382173</td>
    </tr>
    <tr>
      <th>483517</th>
      <td>Vietnam</td>
      <td>96</td>
      <td>2987</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>473.75760</td>
      <td>515.03464</td>
      <td>507.40396</td>
      <td>498.732067</td>
    </tr>
    <tr>
      <th>483562</th>
      <td>Vietnam</td>
      <td>97</td>
      <td>3032</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>414.63620</td>
      <td>462.70406</td>
      <td>451.92092</td>
      <td>443.087060</td>
    </tr>
    <tr>
      <th>483589</th>
      <td>Vietnam</td>
      <td>98</td>
      <td>3059</td>
      <td>7</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>382.07664</td>
      <td>410.02682</td>
      <td>355.50166</td>
      <td>382.535040</td>
    </tr>
    <tr>
      <th>483590</th>
      <td>Vietnam</td>
      <td>98</td>
      <td>3060</td>
      <td>8</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>428.34554</td>
      <td>424.64214</td>
      <td>424.97202</td>
      <td>425.986567</td>
    </tr>
    <tr>
      <th>483597</th>
      <td>Vietnam</td>
      <td>98</td>
      <td>3067</td>
      <td>9</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>404.12058</td>
      <td>392.71086</td>
      <td>454.99814</td>
      <td>417.276527</td>
    </tr>
    <tr>
      <th>483607</th>
      <td>Vietnam</td>
      <td>98</td>
      <td>3077</td>
      <td>8</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>412.06574</td>
      <td>380.42450</td>
      <td>425.25178</td>
      <td>405.914007</td>
    </tr>
    <tr>
      <th>483609</th>
      <td>Vietnam</td>
      <td>98</td>
      <td>3079</td>
      <td>9</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>369.37996</td>
      <td>382.54370</td>
      <td>416.39314</td>
      <td>389.438933</td>
    </tr>
    <tr>
      <th>483616</th>
      <td>Vietnam</td>
      <td>98</td>
      <td>3086</td>
      <td>8</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>521.11700</td>
      <td>416.99320</td>
      <td>486.32974</td>
      <td>474.813313</td>
    </tr>
    <tr>
      <th>483638</th>
      <td>Vietnam</td>
      <td>100</td>
      <td>3108</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>670.12774</td>
      <td>599.27528</td>
      <td>648.67590</td>
      <td>639.359640</td>
    </tr>
    <tr>
      <th>483640</th>
      <td>Vietnam</td>
      <td>100</td>
      <td>3110</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>630.71348</td>
      <td>656.26294</td>
      <td>612.77508</td>
      <td>633.250500</td>
    </tr>
    <tr>
      <th>483659</th>
      <td>Vietnam</td>
      <td>100</td>
      <td>3129</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>585.84672</td>
      <td>573.89300</td>
      <td>597.29576</td>
      <td>585.678493</td>
    </tr>
    <tr>
      <th>483686</th>
      <td>Vietnam</td>
      <td>101</td>
      <td>3156</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>551.18398</td>
      <td>602.08210</td>
      <td>593.00632</td>
      <td>582.090800</td>
    </tr>
    <tr>
      <th>483689</th>
      <td>Vietnam</td>
      <td>101</td>
      <td>3159</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>571.43636</td>
      <td>591.92382</td>
      <td>588.34392</td>
      <td>583.901367</td>
    </tr>
    <tr>
      <th>483712</th>
      <td>Vietnam</td>
      <td>103</td>
      <td>3182</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>658.13210</td>
      <td>586.28426</td>
      <td>645.03916</td>
      <td>629.818507</td>
    </tr>
    <tr>
      <th>483715</th>
      <td>Vietnam</td>
      <td>103</td>
      <td>3185</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>530.85372</td>
      <td>535.05124</td>
      <td>567.17642</td>
      <td>544.360460</td>
    </tr>
    <tr>
      <th>483716</th>
      <td>Vietnam</td>
      <td>103</td>
      <td>3186</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>523.22012</td>
      <td>476.49752</td>
      <td>546.28868</td>
      <td>515.335440</td>
    </tr>
    <tr>
      <th>483721</th>
      <td>Vietnam</td>
      <td>103</td>
      <td>3191</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>583.12040</td>
      <td>538.08690</td>
      <td>566.71018</td>
      <td>562.639160</td>
    </tr>
    <tr>
      <th>483741</th>
      <td>Vietnam</td>
      <td>103</td>
      <td>3211</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>536.53996</td>
      <td>555.70332</td>
      <td>543.95748</td>
      <td>545.400253</td>
    </tr>
    <tr>
      <th>483770</th>
      <td>Vietnam</td>
      <td>104</td>
      <td>3240</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>480.76804</td>
      <td>557.60964</td>
      <td>567.08318</td>
      <td>535.153620</td>
    </tr>
    <tr>
      <th>483789</th>
      <td>Vietnam</td>
      <td>105</td>
      <td>3259</td>
      <td>8</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>324.82472</td>
      <td>379.84304</td>
      <td>387.11300</td>
      <td>363.926920</td>
    </tr>
    <tr>
      <th>483809</th>
      <td>Vietnam</td>
      <td>106</td>
      <td>3279</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>423.74980</td>
      <td>421.94148</td>
      <td>453.50616</td>
      <td>433.065813</td>
    </tr>
    <tr>
      <th>483818</th>
      <td>Vietnam</td>
      <td>106</td>
      <td>3288</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>474.53650</td>
      <td>487.86920</td>
      <td>495.28160</td>
      <td>485.895767</td>
    </tr>
    <tr>
      <th>483819</th>
      <td>Vietnam</td>
      <td>106</td>
      <td>3289</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>459.73672</td>
      <td>486.12172</td>
      <td>507.40396</td>
      <td>484.420800</td>
    </tr>
    <tr>
      <th>483831</th>
      <td>Vietnam</td>
      <td>107</td>
      <td>3301</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>595.66130</td>
      <td>565.99458</td>
      <td>595.24430</td>
      <td>585.633393</td>
    </tr>
    <tr>
      <th>483843</th>
      <td>Vietnam</td>
      <td>107</td>
      <td>3313</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>542.14832</td>
      <td>570.95408</td>
      <td>548.43342</td>
      <td>553.845273</td>
    </tr>
    <tr>
      <th>483846</th>
      <td>Vietnam</td>
      <td>107</td>
      <td>3316</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>511.38026</td>
      <td>512.33394</td>
      <td>512.25288</td>
      <td>511.989027</td>
    </tr>
    <tr>
      <th>483853</th>
      <td>Vietnam</td>
      <td>107</td>
      <td>3323</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>522.51908</td>
      <td>545.21840</td>
      <td>521.67102</td>
      <td>529.802833</td>
    </tr>
    <tr>
      <th>483862</th>
      <td>Vietnam</td>
      <td>108</td>
      <td>3332</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>611.31798</td>
      <td>595.18538</td>
      <td>641.49572</td>
      <td>615.999693</td>
    </tr>
    <tr>
      <th>483903</th>
      <td>Vietnam</td>
      <td>109</td>
      <td>3373</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>478.43122</td>
      <td>448.42942</td>
      <td>507.40396</td>
      <td>478.088200</td>
    </tr>
    <tr>
      <th>483909</th>
      <td>Vietnam</td>
      <td>109</td>
      <td>3379</td>
      <td>9</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>460.59356</td>
      <td>393.01502</td>
      <td>439.98508</td>
      <td>431.197887</td>
    </tr>
    <tr>
      <th>483934</th>
      <td>Vietnam</td>
      <td>110</td>
      <td>3404</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>728.00282</td>
      <td>637.84888</td>
      <td>676.55726</td>
      <td>680.802987</td>
    </tr>
    <tr>
      <th>483968</th>
      <td>Vietnam</td>
      <td>111</td>
      <td>3438</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>521.27278</td>
      <td>559.35712</td>
      <td>546.47520</td>
      <td>542.368367</td>
    </tr>
    <tr>
      <th>483972</th>
      <td>Vietnam</td>
      <td>111</td>
      <td>3442</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>441.58746</td>
      <td>478.98354</td>
      <td>476.81836</td>
      <td>465.796453</td>
    </tr>
    <tr>
      <th>483994</th>
      <td>Vietnam</td>
      <td>112</td>
      <td>3464</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>497.90466</td>
      <td>494.30070</td>
      <td>562.98024</td>
      <td>518.395200</td>
    </tr>
    <tr>
      <th>484011</th>
      <td>Vietnam</td>
      <td>112</td>
      <td>3481</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>404.04268</td>
      <td>441.00492</td>
      <td>451.36144</td>
      <td>432.136347</td>
    </tr>
    <tr>
      <th>484062</th>
      <td>Vietnam</td>
      <td>114</td>
      <td>3532</td>
      <td>9</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>357.69590</td>
      <td>355.24340</td>
      <td>366.41178</td>
      <td>359.783693</td>
    </tr>
    <tr>
      <th>484099</th>
      <td>Vietnam</td>
      <td>116</td>
      <td>3569</td>
      <td>8</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>284.08628</td>
      <td>399.38308</td>
      <td>348.22826</td>
      <td>343.899207</td>
    </tr>
    <tr>
      <th>484100</th>
      <td>Vietnam</td>
      <td>116</td>
      <td>3570</td>
      <td>8</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>407.39210</td>
      <td>425.27758</td>
      <td>438.77284</td>
      <td>423.814173</td>
    </tr>
    <tr>
      <th>484102</th>
      <td>Vietnam</td>
      <td>116</td>
      <td>3572</td>
      <td>9</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>409.41736</td>
      <td>402.71856</td>
      <td>439.89182</td>
      <td>417.342580</td>
    </tr>
    <tr>
      <th>484103</th>
      <td>Vietnam</td>
      <td>116</td>
      <td>3573</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>427.48872</td>
      <td>418.27628</td>
      <td>456.86310</td>
      <td>434.209367</td>
    </tr>
    <tr>
      <th>484109</th>
      <td>Vietnam</td>
      <td>116</td>
      <td>3579</td>
      <td>8</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>310.10282</td>
      <td>379.36646</td>
      <td>345.80380</td>
      <td>345.091027</td>
    </tr>
    <tr>
      <th>484123</th>
      <td>Vietnam</td>
      <td>117</td>
      <td>3593</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>426.86554</td>
      <td>469.75894</td>
      <td>491.92464</td>
      <td>462.849707</td>
    </tr>
    <tr>
      <th>484129</th>
      <td>Vietnam</td>
      <td>117</td>
      <td>3599</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>440.96434</td>
      <td>428.78176</td>
      <td>482.04030</td>
      <td>450.595467</td>
    </tr>
    <tr>
      <th>484130</th>
      <td>Vietnam</td>
      <td>117</td>
      <td>3600</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>480.30066</td>
      <td>529.90704</td>
      <td>542.27900</td>
      <td>517.495567</td>
    </tr>
    <tr>
      <th>484131</th>
      <td>Vietnam</td>
      <td>117</td>
      <td>3601</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>No</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>444.08006</td>
      <td>442.33464</td>
      <td>456.30364</td>
      <td>447.572780</td>
    </tr>
    <tr>
      <th>484132</th>
      <td>Vietnam</td>
      <td>117</td>
      <td>3602</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>396.40910</td>
      <td>480.87928</td>
      <td>429.26146</td>
      <td>435.516613</td>
    </tr>
    <tr>
      <th>484140</th>
      <td>Vietnam</td>
      <td>117</td>
      <td>3610</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>516.44338</td>
      <td>511.30190</td>
      <td>524.00222</td>
      <td>517.249167</td>
    </tr>
    <tr>
      <th>484189</th>
      <td>Vietnam</td>
      <td>119</td>
      <td>3659</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>555.23444</td>
      <td>548.23678</td>
      <td>587.97090</td>
      <td>563.814040</td>
    </tr>
    <tr>
      <th>484201</th>
      <td>Vietnam</td>
      <td>119</td>
      <td>3671</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>373.50834</td>
      <td>481.03814</td>
      <td>453.31966</td>
      <td>435.955380</td>
    </tr>
    <tr>
      <th>484202</th>
      <td>Vietnam</td>
      <td>119</td>
      <td>3672</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>578.05734</td>
      <td>557.25340</td>
      <td>577.43380</td>
      <td>570.914847</td>
    </tr>
    <tr>
      <th>484209</th>
      <td>Vietnam</td>
      <td>119</td>
      <td>3679</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>394.53964</td>
      <td>474.52482</td>
      <td>442.40954</td>
      <td>437.158000</td>
    </tr>
    <tr>
      <th>484216</th>
      <td>Vietnam</td>
      <td>119</td>
      <td>3686</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>476.09442</td>
      <td>539.02280</td>
      <td>536.49758</td>
      <td>517.204933</td>
    </tr>
    <tr>
      <th>484227</th>
      <td>Vietnam</td>
      <td>120</td>
      <td>3697</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>515.66442</td>
      <td>470.40274</td>
      <td>555.33384</td>
      <td>513.800333</td>
    </tr>
    <tr>
      <th>484243</th>
      <td>Vietnam</td>
      <td>120</td>
      <td>3713</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other country</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>526.41378</td>
      <td>517.41756</td>
      <td>578.08652</td>
      <td>540.639287</td>
    </tr>
    <tr>
      <th>484256</th>
      <td>Vietnam</td>
      <td>121</td>
      <td>3726</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>522.36332</td>
      <td>549.66656</td>
      <td>568.38866</td>
      <td>546.806180</td>
    </tr>
    <tr>
      <th>484261</th>
      <td>Vietnam</td>
      <td>121</td>
      <td>3731</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>437.22542</td>
      <td>444.58010</td>
      <td>508.24318</td>
      <td>463.349567</td>
    </tr>
    <tr>
      <th>484276</th>
      <td>Vietnam</td>
      <td>121</td>
      <td>3746</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>468.14924</td>
      <td>412.18150</td>
      <td>526.05372</td>
      <td>468.794820</td>
    </tr>
    <tr>
      <th>484290</th>
      <td>Vietnam</td>
      <td>122</td>
      <td>3760</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>423.28244</td>
      <td>458.00316</td>
      <td>434.48340</td>
      <td>438.589667</td>
    </tr>
    <tr>
      <th>484298</th>
      <td>Vietnam</td>
      <td>122</td>
      <td>3768</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>481.54698</td>
      <td>492.47622</td>
      <td>514.49086</td>
      <td>496.171353</td>
    </tr>
    <tr>
      <th>484301</th>
      <td>Vietnam</td>
      <td>122</td>
      <td>3771</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>566.45116</td>
      <td>531.19016</td>
      <td>600.27974</td>
      <td>565.973687</td>
    </tr>
    <tr>
      <th>484312</th>
      <td>Vietnam</td>
      <td>122</td>
      <td>3782</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>432.62968</td>
      <td>464.03992</td>
      <td>493.04364</td>
      <td>463.237747</td>
    </tr>
    <tr>
      <th>484317</th>
      <td>Vietnam</td>
      <td>122</td>
      <td>3787</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>526.56956</td>
      <td>522.02454</td>
      <td>528.47820</td>
      <td>525.690767</td>
    </tr>
    <tr>
      <th>484319</th>
      <td>Vietnam</td>
      <td>122</td>
      <td>3789</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>415.18150</td>
      <td>420.35284</td>
      <td>445.67324</td>
      <td>427.069193</td>
    </tr>
    <tr>
      <th>484327</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3797</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>481.54694</td>
      <td>484.35656</td>
      <td>543.02498</td>
      <td>502.976160</td>
    </tr>
    <tr>
      <th>484329</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3799</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>407.31424</td>
      <td>524.16918</td>
      <td>447.25846</td>
      <td>459.580627</td>
    </tr>
    <tr>
      <th>484333</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3803</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>439.48434</td>
      <td>568.25338</td>
      <td>538.73556</td>
      <td>515.491093</td>
    </tr>
    <tr>
      <th>484334</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3804</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>560.21964</td>
      <td>598.43720</td>
      <td>587.13166</td>
      <td>581.929500</td>
    </tr>
    <tr>
      <th>484341</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3811</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>580.31624</td>
      <td>556.53162</td>
      <td>604.75568</td>
      <td>580.534513</td>
    </tr>
    <tr>
      <th>484342</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3812</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>543.23882</td>
      <td>574.76676</td>
      <td>563.35324</td>
      <td>560.452940</td>
    </tr>
    <tr>
      <th>484346</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3816</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>504.44774</td>
      <td>544.74182</td>
      <td>559.06376</td>
      <td>536.084440</td>
    </tr>
    <tr>
      <th>484348</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3818</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>469.70710</td>
      <td>518.84730</td>
      <td>475.13986</td>
      <td>487.898087</td>
    </tr>
    <tr>
      <th>484351</th>
      <td>Vietnam</td>
      <td>123</td>
      <td>3821</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>426.00872</td>
      <td>534.49520</td>
      <td>488.38118</td>
      <td>482.961700</td>
    </tr>
    <tr>
      <th>484361</th>
      <td>Vietnam</td>
      <td>124</td>
      <td>3831</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>525.08956</td>
      <td>518.51946</td>
      <td>552.25664</td>
      <td>531.955220</td>
    </tr>
    <tr>
      <th>484382</th>
      <td>Vietnam</td>
      <td>124</td>
      <td>3852</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>368.05576</td>
      <td>484.13596</td>
      <td>434.48342</td>
      <td>428.891713</td>
    </tr>
    <tr>
      <th>484383</th>
      <td>Vietnam</td>
      <td>124</td>
      <td>3853</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>402.87428</td>
      <td>412.02112</td>
      <td>429.44796</td>
      <td>414.781120</td>
    </tr>
    <tr>
      <th>484385</th>
      <td>Vietnam</td>
      <td>124</td>
      <td>3855</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>461.68406</td>
      <td>472.93620</td>
      <td>466.74746</td>
      <td>467.122573</td>
    </tr>
    <tr>
      <th>484390</th>
      <td>Vietnam</td>
      <td>125</td>
      <td>3860</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>516.59918</td>
      <td>544.90068</td>
      <td>527.17270</td>
      <td>529.557520</td>
    </tr>
    <tr>
      <th>484419</th>
      <td>Vietnam</td>
      <td>125</td>
      <td>3889</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>583.50988</td>
      <td>558.93746</td>
      <td>587.03842</td>
      <td>576.495253</td>
    </tr>
    <tr>
      <th>484448</th>
      <td>Vietnam</td>
      <td>127</td>
      <td>3918</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Other country</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>585.69092</td>
      <td>541.24686</td>
      <td>586.29242</td>
      <td>571.076733</td>
    </tr>
    <tr>
      <th>484453</th>
      <td>Vietnam</td>
      <td>127</td>
      <td>3923</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>561.23228</td>
      <td>530.76198</td>
      <td>572.02536</td>
      <td>554.673207</td>
    </tr>
    <tr>
      <th>484461</th>
      <td>Vietnam</td>
      <td>127</td>
      <td>3931</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>535.05998</td>
      <td>499.43314</td>
      <td>510.76092</td>
      <td>515.084680</td>
    </tr>
    <tr>
      <th>484462</th>
      <td>Vietnam</td>
      <td>128</td>
      <td>3932</td>
      <td>9</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>322.02056</td>
      <td>415.26926</td>
      <td>377.78814</td>
      <td>371.692653</td>
    </tr>
    <tr>
      <th>484501</th>
      <td>Vietnam</td>
      <td>129</td>
      <td>3971</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>552.19660</td>
      <td>503.83484</td>
      <td>533.70012</td>
      <td>529.910520</td>
    </tr>
    <tr>
      <th>484524</th>
      <td>Vietnam</td>
      <td>130</td>
      <td>3994</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>451.01264</td>
      <td>462.13360</td>
      <td>478.12384</td>
      <td>463.756693</td>
    </tr>
    <tr>
      <th>484527</th>
      <td>Vietnam</td>
      <td>130</td>
      <td>3997</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>529.99690</td>
      <td>528.78432</td>
      <td>510.48118</td>
      <td>523.087467</td>
    </tr>
    <tr>
      <th>484545</th>
      <td>Vietnam</td>
      <td>131</td>
      <td>4015</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>443.69058</td>
      <td>472.14186</td>
      <td>496.40060</td>
      <td>470.744347</td>
    </tr>
    <tr>
      <th>484550</th>
      <td>Vietnam</td>
      <td>131</td>
      <td>4020</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>481.62488</td>
      <td>506.13836</td>
      <td>540.69378</td>
      <td>509.485673</td>
    </tr>
    <tr>
      <th>484570</th>
      <td>Vietnam</td>
      <td>131</td>
      <td>4040</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>593.71398</td>
      <td>610.10156</td>
      <td>601.21224</td>
      <td>601.675927</td>
    </tr>
    <tr>
      <th>484629</th>
      <td>Vietnam</td>
      <td>134</td>
      <td>4099</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>494.32154</td>
      <td>478.49636</td>
      <td>561.48826</td>
      <td>511.435387</td>
    </tr>
    <tr>
      <th>484693</th>
      <td>Vietnam</td>
      <td>137</td>
      <td>4163</td>
      <td>10</td>
      <td>99</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>529.76320</td>
      <td>520.35648</td>
      <td>535.09884</td>
      <td>528.406173</td>
    </tr>
    <tr>
      <th>484695</th>
      <td>Vietnam</td>
      <td>137</td>
      <td>4165</td>
      <td>10</td>
      <td>99</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>429.12448</td>
      <td>481.35586</td>
      <td>493.69638</td>
      <td>468.058907</td>
    </tr>
    <tr>
      <th>484699</th>
      <td>Vietnam</td>
      <td>137</td>
      <td>4169</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>451.16840</td>
      <td>508.04470</td>
      <td>497.70608</td>
      <td>485.639727</td>
    </tr>
    <tr>
      <th>484706</th>
      <td>Vietnam</td>
      <td>137</td>
      <td>4176</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>472.66708</td>
      <td>486.75718</td>
      <td>544.51700</td>
      <td>501.313753</td>
    </tr>
    <tr>
      <th>484714</th>
      <td>Vietnam</td>
      <td>137</td>
      <td>4184</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>467.68190</td>
      <td>518.52960</td>
      <td>511.50690</td>
      <td>499.239467</td>
    </tr>
    <tr>
      <th>484738</th>
      <td>Vietnam</td>
      <td>138</td>
      <td>4208</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>487.93426</td>
      <td>499.59352</td>
      <td>511.50694</td>
      <td>499.678240</td>
    </tr>
    <tr>
      <th>484758</th>
      <td>Vietnam</td>
      <td>139</td>
      <td>4228</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>392.59230</td>
      <td>406.05526</td>
      <td>458.91458</td>
      <td>419.187380</td>
    </tr>
    <tr>
      <th>484764</th>
      <td>Vietnam</td>
      <td>139</td>
      <td>4234</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>394.07226</td>
      <td>479.44952</td>
      <td>499.47780</td>
      <td>457.666527</td>
    </tr>
    <tr>
      <th>484787</th>
      <td>Vietnam</td>
      <td>140</td>
      <td>4257</td>
      <td>9</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>402.56270</td>
      <td>302.79622</td>
      <td>439.89182</td>
      <td>381.750247</td>
    </tr>
    <tr>
      <th>484788</th>
      <td>Vietnam</td>
      <td>140</td>
      <td>4258</td>
      <td>8</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>364.23898</td>
      <td>264.94438</td>
      <td>369.58224</td>
      <td>332.921867</td>
    </tr>
    <tr>
      <th>484790</th>
      <td>Vietnam</td>
      <td>140</td>
      <td>4260</td>
      <td>8</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>364.70632</td>
      <td>303.75852</td>
      <td>411.73072</td>
      <td>360.065187</td>
    </tr>
    <tr>
      <th>484793</th>
      <td>Vietnam</td>
      <td>140</td>
      <td>4263</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>Yes</td>
      <td>297.87350</td>
      <td>313.12098</td>
      <td>382.45056</td>
      <td>331.148347</td>
    </tr>
    <tr>
      <th>484794</th>
      <td>Vietnam</td>
      <td>140</td>
      <td>4264</td>
      <td>8</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>382.38822</td>
      <td>346.08486</td>
      <td>400.91384</td>
      <td>376.462307</td>
    </tr>
    <tr>
      <th>484796</th>
      <td>Vietnam</td>
      <td>140</td>
      <td>4266</td>
      <td>8</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>345.07714</td>
      <td>240.40488</td>
      <td>349.90676</td>
      <td>311.796260</td>
    </tr>
    <tr>
      <th>484824</th>
      <td>Vietnam</td>
      <td>141</td>
      <td>4294</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>501.87724</td>
      <td>550.77858</td>
      <td>566.05746</td>
      <td>539.571093</td>
    </tr>
    <tr>
      <th>484866</th>
      <td>Vietnam</td>
      <td>143</td>
      <td>4336</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>484.27328</td>
      <td>505.04674</td>
      <td>512.90562</td>
      <td>500.741880</td>
    </tr>
    <tr>
      <th>484871</th>
      <td>Vietnam</td>
      <td>143</td>
      <td>4341</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>506.62876</td>
      <td>516.75514</td>
      <td>515.79634</td>
      <td>513.060080</td>
    </tr>
    <tr>
      <th>484873</th>
      <td>Vietnam</td>
      <td>144</td>
      <td>4343</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>581.48464</td>
      <td>594.86280</td>
      <td>571.55914</td>
      <td>582.635527</td>
    </tr>
    <tr>
      <th>484916</th>
      <td>Vietnam</td>
      <td>145</td>
      <td>4386</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>552.04082</td>
      <td>522.97774</td>
      <td>567.54942</td>
      <td>547.522660</td>
    </tr>
    <tr>
      <th>484932</th>
      <td>Vietnam</td>
      <td>145</td>
      <td>4402</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>491.59528</td>
      <td>467.59594</td>
      <td>526.79972</td>
      <td>495.330313</td>
    </tr>
    <tr>
      <th>484935</th>
      <td>Vietnam</td>
      <td>145</td>
      <td>4405</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>511.76974</td>
      <td>583.82188</td>
      <td>569.32112</td>
      <td>554.970913</td>
    </tr>
    <tr>
      <th>484950</th>
      <td>Vietnam</td>
      <td>146</td>
      <td>4420</td>
      <td>8</td>
      <td>8</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>352.24336</td>
      <td>372.05880</td>
      <td>407.06826</td>
      <td>377.123473</td>
    </tr>
    <tr>
      <th>484952</th>
      <td>Vietnam</td>
      <td>146</td>
      <td>4422</td>
      <td>9</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>408.87212</td>
      <td>473.20954</td>
      <td>479.05634</td>
      <td>453.712667</td>
    </tr>
    <tr>
      <th>484955</th>
      <td>Vietnam</td>
      <td>146</td>
      <td>4425</td>
      <td>9</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>429.82552</td>
      <td>465.59106</td>
      <td>473.83442</td>
      <td>456.417000</td>
    </tr>
    <tr>
      <th>484966</th>
      <td>Vietnam</td>
      <td>146</td>
      <td>4436</td>
      <td>9</td>
      <td>3</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>387.99656</td>
      <td>365.98946</td>
      <td>409.39950</td>
      <td>387.795173</td>
    </tr>
    <tr>
      <th>484968</th>
      <td>Vietnam</td>
      <td>146</td>
      <td>4438</td>
      <td>9</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>323.73426</td>
      <td>421.14718</td>
      <td>403.89780</td>
      <td>382.926413</td>
    </tr>
    <tr>
      <th>484969</th>
      <td>Vietnam</td>
      <td>146</td>
      <td>4439</td>
      <td>9</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>Three or four times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>341.80558</td>
      <td>420.35286</td>
      <td>391.21596</td>
      <td>384.458133</td>
    </tr>
    <tr>
      <th>484971</th>
      <td>Vietnam</td>
      <td>147</td>
      <td>4441</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>680.56552</td>
      <td>590.13312</td>
      <td>642.98768</td>
      <td>637.895440</td>
    </tr>
    <tr>
      <th>484980</th>
      <td>Vietnam</td>
      <td>147</td>
      <td>4450</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>638.89236</td>
      <td>561.89892</td>
      <td>628.81388</td>
      <td>609.868387</td>
    </tr>
    <tr>
      <th>485006</th>
      <td>Vietnam</td>
      <td>148</td>
      <td>4476</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>473.36812</td>
      <td>551.01688</td>
      <td>549.36588</td>
      <td>524.583627</td>
    </tr>
    <tr>
      <th>485013</th>
      <td>Vietnam</td>
      <td>148</td>
      <td>4483</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>448.59790</td>
      <td>522.10398</td>
      <td>451.54792</td>
      <td>474.083267</td>
    </tr>
    <tr>
      <th>485019</th>
      <td>Vietnam</td>
      <td>148</td>
      <td>4489</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>Three or four times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>475.15968</td>
      <td>512.74542</td>
      <td>540.22752</td>
      <td>509.377540</td>
    </tr>
    <tr>
      <th>485031</th>
      <td>Vietnam</td>
      <td>148</td>
      <td>4501</td>
      <td>10</td>
      <td>8</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>475.08180</td>
      <td>445.54242</td>
      <td>528.66466</td>
      <td>483.096293</td>
    </tr>
    <tr>
      <th>485057</th>
      <td>Vietnam</td>
      <td>149</td>
      <td>4527</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>570.11214</td>
      <td>571.27176</td>
      <td>577.43378</td>
      <td>572.939227</td>
    </tr>
    <tr>
      <th>485073</th>
      <td>Vietnam</td>
      <td>149</td>
      <td>4543</td>
      <td>10</td>
      <td>1</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>497.67098</td>
      <td>496.84492</td>
      <td>504.97948</td>
      <td>499.831793</td>
    </tr>
    <tr>
      <th>485077</th>
      <td>Vietnam</td>
      <td>150</td>
      <td>4547</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>472.66708</td>
      <td>509.31560</td>
      <td>493.04364</td>
      <td>491.675440</td>
    </tr>
    <tr>
      <th>485083</th>
      <td>Vietnam</td>
      <td>150</td>
      <td>4553</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>453.58312</td>
      <td>489.80982</td>
      <td>483.15926</td>
      <td>475.517400</td>
    </tr>
    <tr>
      <th>485093</th>
      <td>Vietnam</td>
      <td>150</td>
      <td>4563</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>Five or more times</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>490.66054</td>
      <td>480.66764</td>
      <td>544.98322</td>
      <td>505.437133</td>
    </tr>
    <tr>
      <th>485100</th>
      <td>Vietnam</td>
      <td>150</td>
      <td>4570</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>469.23974</td>
      <td>441.16378</td>
      <td>471.78292</td>
      <td>460.728813</td>
    </tr>
    <tr>
      <th>485107</th>
      <td>Vietnam</td>
      <td>150</td>
      <td>4577</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>453.27154</td>
      <td>426.85712</td>
      <td>445.20702</td>
      <td>441.778560</td>
    </tr>
    <tr>
      <th>485109</th>
      <td>Vietnam</td>
      <td>151</td>
      <td>4579</td>
      <td>7</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>281.98320</td>
      <td>264.94438</td>
      <td>330.97724</td>
      <td>292.634940</td>
    </tr>
    <tr>
      <th>485110</th>
      <td>Vietnam</td>
      <td>151</td>
      <td>4580</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>432.08442</td>
      <td>401.51564</td>
      <td>432.89818</td>
      <td>422.166080</td>
    </tr>
    <tr>
      <th>485120</th>
      <td>Vietnam</td>
      <td>151</td>
      <td>4590</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>346.32342</td>
      <td>454.66704</td>
      <td>402.03282</td>
      <td>401.007760</td>
    </tr>
    <tr>
      <th>485121</th>
      <td>Vietnam</td>
      <td>151</td>
      <td>4591</td>
      <td>8</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>371.56098</td>
      <td>315.94810</td>
      <td>446.41924</td>
      <td>377.976107</td>
    </tr>
    <tr>
      <th>485136</th>
      <td>Vietnam</td>
      <td>151</td>
      <td>4606</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Male</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Other language</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>428.96868</td>
      <td>404.96400</td>
      <td>476.72510</td>
      <td>436.885927</td>
    </tr>
    <tr>
      <th>485145</th>
      <td>Vietnam</td>
      <td>152</td>
      <td>4615</td>
      <td>9</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>390.56708</td>
      <td>437.03334</td>
      <td>428.98174</td>
      <td>418.860720</td>
    </tr>
    <tr>
      <th>485146</th>
      <td>Vietnam</td>
      <td>152</td>
      <td>4616</td>
      <td>9</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>386.59448</td>
      <td>422.02090</td>
      <td>418.63110</td>
      <td>409.082160</td>
    </tr>
    <tr>
      <th>485151</th>
      <td>Vietnam</td>
      <td>152</td>
      <td>4621</td>
      <td>7</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>242.17948</td>
      <td>321.46124</td>
      <td>282.95412</td>
      <td>282.198280</td>
    </tr>
    <tr>
      <th>485178</th>
      <td>Vietnam</td>
      <td>153</td>
      <td>4648</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>637.33448</td>
      <td>623.89504</td>
      <td>726.53864</td>
      <td>662.589387</td>
    </tr>
    <tr>
      <th>485186</th>
      <td>Vietnam</td>
      <td>153</td>
      <td>4656</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>772.01274</td>
      <td>664.15266</td>
      <td>758.52294</td>
      <td>731.562780</td>
    </tr>
    <tr>
      <th>485208</th>
      <td>Vietnam</td>
      <td>153</td>
      <td>4678</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>718.57768</td>
      <td>654.85010</td>
      <td>743.32340</td>
      <td>705.583727</td>
    </tr>
    <tr>
      <th>485211</th>
      <td>Vietnam</td>
      <td>153</td>
      <td>4681</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>586.70354</td>
      <td>599.70808</td>
      <td>638.51176</td>
      <td>608.307793</td>
    </tr>
    <tr>
      <th>485258</th>
      <td>Vietnam</td>
      <td>155</td>
      <td>4728</td>
      <td>10</td>
      <td>9</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>457.16622</td>
      <td>503.67598</td>
      <td>403.24506</td>
      <td>454.695753</td>
    </tr>
    <tr>
      <th>485263</th>
      <td>Vietnam</td>
      <td>155</td>
      <td>4733</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>473.83548</td>
      <td>522.97772</td>
      <td>503.39426</td>
      <td>500.069153</td>
    </tr>
    <tr>
      <th>485272</th>
      <td>Vietnam</td>
      <td>155</td>
      <td>4742</td>
      <td>10</td>
      <td>10</td>
      <td>1996</td>
      <td>Male</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>429.74762</td>
      <td>438.40512</td>
      <td>460.22004</td>
      <td>442.790927</td>
    </tr>
    <tr>
      <th>485278</th>
      <td>Vietnam</td>
      <td>155</td>
      <td>4748</td>
      <td>10</td>
      <td>3</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>514.41812</td>
      <td>538.38736</td>
      <td>526.24022</td>
      <td>526.348567</td>
    </tr>
    <tr>
      <th>485285</th>
      <td>Vietnam</td>
      <td>156</td>
      <td>4755</td>
      <td>96</td>
      <td>6</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>No</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>440.96432</td>
      <td>430.75832</td>
      <td>429.72770</td>
      <td>433.816780</td>
    </tr>
    <tr>
      <th>485290</th>
      <td>Vietnam</td>
      <td>156</td>
      <td>4760</td>
      <td>96</td>
      <td>4</td>
      <td>1996</td>
      <td>Female</td>
      <td>One or two times</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>473.91338</td>
      <td>458.63858</td>
      <td>456.21038</td>
      <td>462.920780</td>
    </tr>
    <tr>
      <th>485305</th>
      <td>Vietnam</td>
      <td>156</td>
      <td>4775</td>
      <td>96</td>
      <td>9</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>468.07134</td>
      <td>476.89850</td>
      <td>514.11784</td>
      <td>486.362560</td>
    </tr>
    <tr>
      <th>485308</th>
      <td>Vietnam</td>
      <td>156</td>
      <td>4778</td>
      <td>96</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>420.08880</td>
      <td>430.04346</td>
      <td>448.19098</td>
      <td>432.774413</td>
    </tr>
    <tr>
      <th>485309</th>
      <td>Vietnam</td>
      <td>156</td>
      <td>4779</td>
      <td>96</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>434.18756</td>
      <td>375.45242</td>
      <td>455.37114</td>
      <td>421.670373</td>
    </tr>
    <tr>
      <th>485361</th>
      <td>Vietnam</td>
      <td>159</td>
      <td>4831</td>
      <td>10</td>
      <td>5</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>490.19318</td>
      <td>497.71868</td>
      <td>526.14696</td>
      <td>504.686273</td>
    </tr>
    <tr>
      <th>485391</th>
      <td>Vietnam</td>
      <td>160</td>
      <td>4861</td>
      <td>10</td>
      <td>6</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>550.63874</td>
      <td>502.32014</td>
      <td>569.69414</td>
      <td>540.884340</td>
    </tr>
    <tr>
      <th>485396</th>
      <td>Vietnam</td>
      <td>160</td>
      <td>4866</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Language of the test</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>512.39288</td>
      <td>453.08070</td>
      <td>562.23424</td>
      <td>509.235940</td>
    </tr>
    <tr>
      <th>485407</th>
      <td>Vietnam</td>
      <td>160</td>
      <td>4877</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>592.62348</td>
      <td>544.82322</td>
      <td>609.13838</td>
      <td>582.195027</td>
    </tr>
    <tr>
      <th>485420</th>
      <td>Vietnam</td>
      <td>160</td>
      <td>4890</td>
      <td>10</td>
      <td>2</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>372.96310</td>
      <td>380.63736</td>
      <td>452.76016</td>
      <td>402.120207</td>
    </tr>
    <tr>
      <th>485427</th>
      <td>Vietnam</td>
      <td>161</td>
      <td>4897</td>
      <td>10</td>
      <td>7</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>588.72878</td>
      <td>568.73002</td>
      <td>600.27974</td>
      <td>585.912847</td>
    </tr>
    <tr>
      <th>485428</th>
      <td>Vietnam</td>
      <td>161</td>
      <td>4898</td>
      <td>10</td>
      <td>4</td>
      <td>1996</td>
      <td>Male</td>
      <td>None</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>531.32108</td>
      <td>496.38574</td>
      <td>527.73220</td>
      <td>518.479673</td>
    </tr>
    <tr>
      <th>485478</th>
      <td>Vietnam</td>
      <td>162</td>
      <td>4948</td>
      <td>10</td>
      <td>11</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>441.04222</td>
      <td>469.12348</td>
      <td>494.90860</td>
      <td>468.358100</td>
    </tr>
    <tr>
      <th>485489</th>
      <td>Vietnam</td>
      <td>162</td>
      <td>4959</td>
      <td>10</td>
      <td>12</td>
      <td>1996</td>
      <td>Female</td>
      <td>None</td>
      <td>Yes</td>
      <td>No</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Country of test</td>
      <td>Language of the test</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>454.43994</td>
      <td>488.66354</td>
      <td>492.95038</td>
      <td>478.684620</td>
    </tr>
  </tbody>
</table>
<p>78767 rows × 21 columns</p>
</div>



##### Verdict
As the core dataset (country/school_id/student_id/gender/grades) is complete, the records contaminated with NaN will only be removed from the visualization where the affected columns will be in use.

### Remove spaces from column SKIPPED_SCHOOL

##### Define
The column SKIPPED_SCHOOL has at the end of the actual string additional multiple blanks. These should be removed


```python
print("'None   ' = %1.f characters" % (len(pisa_clean.iloc[0]['SKIPPED_SCHOOL'])))
print("'None'    = %1.f characters" % (len('None')))
```

    'None   ' = 6 characters
    'None'    = 4 characters
    

It is visible that in the first cell of the column SKIPPED_SCHOOL are for the string 'None' instead of 4 characters 6 characters.  
This is proof enough that there are some blank spaces hidden behind the actual string.  
Investigating other cells, proofs that every string has these additional 2 blank spaces at the end.

##### Code


```python
# remove blank spaces
pisa_clean.SKIPPED_SCHOOL = pisa_clean.SKIPPED_SCHOOL.str[:-2]
```

##### Test


```python
print("Now the string '%s' is correct with a length of %1.f" % (pisa_clean.iloc[0]['SKIPPED_SCHOOL'], len(pisa_clean.iloc[0]['SKIPPED_SCHOOL'])))
```

    Now the string 'None' is correct with a length of 4
    

## Data Visualization
In this chapter the questions will be answered with some fancy beautiful plots.
### Univariate Exploration

##### Define
Let's first have a look at the grades overall.
##### Code


```python
plt.figure(figsize = [25, 10])

bins = np.linspace(0, 900, 20)

plt.hist([pisa_clean['MATH'], pisa_clean['READ'], pisa_clean['SCIENCE'], pisa_clean['AVG_SCORE']], bins, 
         alpha=0.3, label=['Math','Reading','Science', 'Overall'], color=['red','green','blue','white'])
plt.legend(loc='upper right', fontsize= 20)
plt.yticks(fontsize= 15)
plt.xticks(fontsize= 15)
plt.xlabel('Score', fontsize= 20);
plt.ylabel('Count', fontsize= 20)
plt.title('Scores in each study area', fontsize=30);
plt.show()
```


![png](output_59_0.png)


##### Findings
This plot is a showpiece of a bell-shaped curve. It is visible that students receive in average worse math scores than reading scores. On the other side, science is pretty balanced out and has an estimated same amount of good and bad scores.

### Does skipping school affects bad grades?

##### Define
The pisa dataset will be tested if there can be a correlation between bad scores and skipping school.
##### Code


```python
# Drop all NA records of column SKIPPED_SCHOOL
pisa_skip_school = pisa_clean.dropna(subset=['SKIPPED_SCHOOL'])
```


```python
# Check what selections are possible and the count of each selection
pisa_skip_school['SKIPPED_SCHOOL'].value_counts()
```




    None                   306065
    One or two times       124380
    Three or four times    29817 
    Five or more times     18881 
    Name: SKIPPED_SCHOOL, dtype: int64




```python
# Aggregate cleaned dataset for desired visualization
pisa_skip_school_agg = pisa_skip_school.groupby('SKIPPED_SCHOOL')['MATH','READ','SCIENCE','AVG_SCORE'].mean().reset_index()

# Create new dataframe for barplot output
pisa_skipped_vis = pd.DataFrame(columns=['SKIPPED_SCHOOL','SUBJECT','AVG_SCORE'])
# iterate row by row and column by column and insert into new dataframe with modified shape
for index, row in pisa_skip_school_agg.iterrows(): 
    for columnname in ['MATH','READ','SCIENCE','AVG_SCORE']:
        pisa_skipped_vis = pisa_skipped_vis.append({ 'SKIPPED_SCHOOL': row['SKIPPED_SCHOOL'],
                                                     'SUBJECT': columnname,
                                                     'AVG_SCORE': row[columnname]}, ignore_index=True)
# Sort dataframe by score
pisa_skipped_vis = pisa_skipped_vis.sort_values(by = ['SUBJECT','AVG_SCORE'], axis=0, ascending=False)

# create figure
plt.figure(figsize = [25, 10])
# create barplot
sb.barplot(x='SUBJECT', y='AVG_SCORE', hue='SKIPPED_SCHOOL', data= pisa_skipped_vis, 
           palette=sb.color_palette('Set1'), alpha=0.7)
# set title and labels
plt.title('Average Score per Subject and frequency of skipping school', fontsize=30)
plt.legend(loc='upper right', fontsize= 20)
plt.yticks(fontsize= 15)
plt.xticks(fontsize= 15)
plt.xlabel('Subject', fontsize= 20)
plt.ylabel('Score',fontsize= 20)
plt.ylim(410, 525)

# save plot as png
plt.savefig('univariate_bp_ScoreSkippingSchool.png')
plt.show()
```


![png](output_64_0.png)


##### Findings


```python
print('There is an obvious pattern that students that do not skip school are overall in each subject better than \nstudents skipping school.')
print('The difference from students never skipping school and skipping five or more times in Score is %.1f %% worse.' %(pisa_skip_school_agg.iloc[1]['AVG_SCORE']/pisa_skip_school_agg.iloc[0]['AVG_SCORE']*100-100))
print('Students that skip school only one or two times are in average %.1f %% worse than students that never skip school.' %(pisa_skip_school_agg.iloc[1]['AVG_SCORE']/pisa_skip_school_agg.iloc[2]['AVG_SCORE']*100-100))
```

    There is an obvious pattern that students that do not skip school are overall in each subject better than 
    students skipping school.
    The difference from students never skipping school and skipping five or more times in Score is 13.5 % worse.
    Students that skip school only one or two times are in average 5.8 % worse than students that never skip school.
    

### In which country do students skip the most frequently?
##### Define
Now let's check in which country the most students skip school.
##### Code


```python
# Aggregate data for analysis
pisa_agg_skip = pisa_skip_school.groupby(['COUNTRY','SKIPPED_SCHOOL'])['STUDENT_ID'].count().reset_index(name='COUNT')
pisa_agg_skip
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
      <th>COUNTRY</th>
      <th>SKIPPED_SCHOOL</th>
      <th>COUNT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Albania</td>
      <td>Five or more times</td>
      <td>114</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>None</td>
      <td>2847</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>One or two times</td>
      <td>1251</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>Three or four times</td>
      <td>219</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Argentina</td>
      <td>Five or more times</td>
      <td>482</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Argentina</td>
      <td>None</td>
      <td>3045</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Argentina</td>
      <td>One or two times</td>
      <td>1702</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Argentina</td>
      <td>Three or four times</td>
      <td>588</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Australia</td>
      <td>Five or more times</td>
      <td>629</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Australia</td>
      <td>None</td>
      <td>8896</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Australia</td>
      <td>One or two times</td>
      <td>3619</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Australia</td>
      <td>Three or four times</td>
      <td>1042</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Austria</td>
      <td>Five or more times</td>
      <td>94</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Austria</td>
      <td>None</td>
      <td>3725</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Austria</td>
      <td>One or two times</td>
      <td>752</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Austria</td>
      <td>Three or four times</td>
      <td>150</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Belgium</td>
      <td>Five or more times</td>
      <td>233</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Belgium</td>
      <td>None</td>
      <td>6265</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Belgium</td>
      <td>One or two times</td>
      <td>1705</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Belgium</td>
      <td>Three or four times</td>
      <td>302</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Brazil</td>
      <td>Five or more times</td>
      <td>662</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Brazil</td>
      <td>None</td>
      <td>12473</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Brazil</td>
      <td>One or two times</td>
      <td>4762</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Brazil</td>
      <td>Three or four times</td>
      <td>1063</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Bulgaria</td>
      <td>Five or more times</td>
      <td>467</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Bulgaria</td>
      <td>None</td>
      <td>2170</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Bulgaria</td>
      <td>One or two times</td>
      <td>1931</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Bulgaria</td>
      <td>Three or four times</td>
      <td>662</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Canada</td>
      <td>Five or more times</td>
      <td>1023</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Canada</td>
      <td>None</td>
      <td>12622</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Canada</td>
      <td>One or two times</td>
      <td>5772</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Canada</td>
      <td>Three or four times</td>
      <td>1621</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Chile</td>
      <td>Five or more times</td>
      <td>436</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Chile</td>
      <td>None</td>
      <td>3372</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Chile</td>
      <td>One or two times</td>
      <td>2292</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Chile</td>
      <td>Three or four times</td>
      <td>668</td>
    </tr>
    <tr>
      <th>36</th>
      <td>China-Shanghai</td>
      <td>Five or more times</td>
      <td>71</td>
    </tr>
    <tr>
      <th>37</th>
      <td>China-Shanghai</td>
      <td>None</td>
      <td>4304</td>
    </tr>
    <tr>
      <th>38</th>
      <td>China-Shanghai</td>
      <td>One or two times</td>
      <td>684</td>
    </tr>
    <tr>
      <th>39</th>
      <td>China-Shanghai</td>
      <td>Three or four times</td>
      <td>111</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Chinese Taipei</td>
      <td>Five or more times</td>
      <td>180</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Chinese Taipei</td>
      <td>None</td>
      <td>4691</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Chinese Taipei</td>
      <td>One or two times</td>
      <td>888</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Chinese Taipei</td>
      <td>Three or four times</td>
      <td>269</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Colombia</td>
      <td>Five or more times</td>
      <td>178</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Colombia</td>
      <td>None</td>
      <td>5735</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Colombia</td>
      <td>One or two times</td>
      <td>2648</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Colombia</td>
      <td>Three or four times</td>
      <td>441</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Connecticut (USA)</td>
      <td>Five or more times</td>
      <td>36</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Connecticut (USA)</td>
      <td>None</td>
      <td>1177</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Connecticut (USA)</td>
      <td>One or two times</td>
      <td>398</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Connecticut (USA)</td>
      <td>Three or four times</td>
      <td>77</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Costa Rica</td>
      <td>Five or more times</td>
      <td>344</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Costa Rica</td>
      <td>None</td>
      <td>1948</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Costa Rica</td>
      <td>One or two times</td>
      <td>1717</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Costa Rica</td>
      <td>Three or four times</td>
      <td>563</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Croatia</td>
      <td>Five or more times</td>
      <td>122</td>
    </tr>
    <tr>
      <th>57</th>
      <td>Croatia</td>
      <td>None</td>
      <td>3298</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Croatia</td>
      <td>One or two times</td>
      <td>1291</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Croatia</td>
      <td>Three or four times</td>
      <td>277</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Czech Republic</td>
      <td>Five or more times</td>
      <td>140</td>
    </tr>
    <tr>
      <th>61</th>
      <td>Czech Republic</td>
      <td>None</td>
      <td>3917</td>
    </tr>
    <tr>
      <th>62</th>
      <td>Czech Republic</td>
      <td>One or two times</td>
      <td>1085</td>
    </tr>
    <tr>
      <th>63</th>
      <td>Czech Republic</td>
      <td>Three or four times</td>
      <td>166</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Denmark</td>
      <td>Five or more times</td>
      <td>384</td>
    </tr>
    <tr>
      <th>65</th>
      <td>Denmark</td>
      <td>None</td>
      <td>4268</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Denmark</td>
      <td>One or two times</td>
      <td>2081</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Denmark</td>
      <td>Three or four times</td>
      <td>638</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Estonia</td>
      <td>Five or more times</td>
      <td>206</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Estonia</td>
      <td>None</td>
      <td>2745</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Estonia</td>
      <td>One or two times</td>
      <td>1399</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Estonia</td>
      <td>Three or four times</td>
      <td>382</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Finland</td>
      <td>Five or more times</td>
      <td>426</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Finland</td>
      <td>None</td>
      <td>4518</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Finland</td>
      <td>One or two times</td>
      <td>2853</td>
    </tr>
    <tr>
      <th>75</th>
      <td>Finland</td>
      <td>Three or four times</td>
      <td>860</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Florida (USA)</td>
      <td>Five or more times</td>
      <td>54</td>
    </tr>
    <tr>
      <th>77</th>
      <td>Florida (USA)</td>
      <td>None</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>78</th>
      <td>Florida (USA)</td>
      <td>One or two times</td>
      <td>473</td>
    </tr>
    <tr>
      <th>79</th>
      <td>Florida (USA)</td>
      <td>Three or four times</td>
      <td>103</td>
    </tr>
    <tr>
      <th>80</th>
      <td>France</td>
      <td>Five or more times</td>
      <td>123</td>
    </tr>
    <tr>
      <th>81</th>
      <td>France</td>
      <td>None</td>
      <td>3101</td>
    </tr>
    <tr>
      <th>82</th>
      <td>France</td>
      <td>One or two times</td>
      <td>1085</td>
    </tr>
    <tr>
      <th>83</th>
      <td>France</td>
      <td>Three or four times</td>
      <td>218</td>
    </tr>
    <tr>
      <th>84</th>
      <td>Germany</td>
      <td>Five or more times</td>
      <td>81</td>
    </tr>
    <tr>
      <th>85</th>
      <td>Germany</td>
      <td>None</td>
      <td>3325</td>
    </tr>
    <tr>
      <th>86</th>
      <td>Germany</td>
      <td>One or two times</td>
      <td>767</td>
    </tr>
    <tr>
      <th>87</th>
      <td>Germany</td>
      <td>Three or four times</td>
      <td>133</td>
    </tr>
    <tr>
      <th>88</th>
      <td>Greece</td>
      <td>Five or more times</td>
      <td>493</td>
    </tr>
    <tr>
      <th>89</th>
      <td>Greece</td>
      <td>None</td>
      <td>2526</td>
    </tr>
    <tr>
      <th>90</th>
      <td>Greece</td>
      <td>One or two times</td>
      <td>1523</td>
    </tr>
    <tr>
      <th>91</th>
      <td>Greece</td>
      <td>Three or four times</td>
      <td>559</td>
    </tr>
    <tr>
      <th>92</th>
      <td>Hong Kong-China</td>
      <td>Five or more times</td>
      <td>36</td>
    </tr>
    <tr>
      <th>93</th>
      <td>Hong Kong-China</td>
      <td>None</td>
      <td>3912</td>
    </tr>
    <tr>
      <th>94</th>
      <td>Hong Kong-China</td>
      <td>One or two times</td>
      <td>570</td>
    </tr>
    <tr>
      <th>95</th>
      <td>Hong Kong-China</td>
      <td>Three or four times</td>
      <td>62</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Hungary</td>
      <td>Five or more times</td>
      <td>100</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Hungary</td>
      <td>None</td>
      <td>3689</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Hungary</td>
      <td>One or two times</td>
      <td>851</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Hungary</td>
      <td>Three or four times</td>
      <td>134</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Iceland</td>
      <td>Five or more times</td>
      <td>84</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Iceland</td>
      <td>None</td>
      <td>2221</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Iceland</td>
      <td>One or two times</td>
      <td>911</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Iceland</td>
      <td>Three or four times</td>
      <td>192</td>
    </tr>
    <tr>
      <th>104</th>
      <td>Indonesia</td>
      <td>Five or more times</td>
      <td>96</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Indonesia</td>
      <td>None</td>
      <td>4040</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Indonesia</td>
      <td>One or two times</td>
      <td>1253</td>
    </tr>
    <tr>
      <th>107</th>
      <td>Indonesia</td>
      <td>Three or four times</td>
      <td>179</td>
    </tr>
    <tr>
      <th>108</th>
      <td>Ireland</td>
      <td>Five or more times</td>
      <td>119</td>
    </tr>
    <tr>
      <th>109</th>
      <td>Ireland</td>
      <td>None</td>
      <td>3648</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Ireland</td>
      <td>One or two times</td>
      <td>989</td>
    </tr>
    <tr>
      <th>111</th>
      <td>Ireland</td>
      <td>Three or four times</td>
      <td>230</td>
    </tr>
    <tr>
      <th>112</th>
      <td>Israel</td>
      <td>Five or more times</td>
      <td>341</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Israel</td>
      <td>None</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>114</th>
      <td>Israel</td>
      <td>One or two times</td>
      <td>1775</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Israel</td>
      <td>Three or four times</td>
      <td>529</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Italy</td>
      <td>Five or more times</td>
      <td>959</td>
    </tr>
    <tr>
      <th>117</th>
      <td>Italy</td>
      <td>None</td>
      <td>20739</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Italy</td>
      <td>One or two times</td>
      <td>7615</td>
    </tr>
    <tr>
      <th>119</th>
      <td>Italy</td>
      <td>Three or four times</td>
      <td>1527</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Japan</td>
      <td>Five or more times</td>
      <td>32</td>
    </tr>
    <tr>
      <th>121</th>
      <td>Japan</td>
      <td>None</td>
      <td>5691</td>
    </tr>
    <tr>
      <th>122</th>
      <td>Japan</td>
      <td>One or two times</td>
      <td>467</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Japan</td>
      <td>Three or four times</td>
      <td>64</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Jordan</td>
      <td>Five or more times</td>
      <td>361</td>
    </tr>
    <tr>
      <th>125</th>
      <td>Jordan</td>
      <td>None</td>
      <td>4281</td>
    </tr>
    <tr>
      <th>126</th>
      <td>Jordan</td>
      <td>One or two times</td>
      <td>1780</td>
    </tr>
    <tr>
      <th>127</th>
      <td>Jordan</td>
      <td>Three or four times</td>
      <td>410</td>
    </tr>
    <tr>
      <th>128</th>
      <td>Kazakhstan</td>
      <td>Five or more times</td>
      <td>80</td>
    </tr>
    <tr>
      <th>129</th>
      <td>Kazakhstan</td>
      <td>None</td>
      <td>4106</td>
    </tr>
    <tr>
      <th>130</th>
      <td>Kazakhstan</td>
      <td>One or two times</td>
      <td>1425</td>
    </tr>
    <tr>
      <th>131</th>
      <td>Kazakhstan</td>
      <td>Three or four times</td>
      <td>193</td>
    </tr>
    <tr>
      <th>132</th>
      <td>Korea</td>
      <td>Five or more times</td>
      <td>161</td>
    </tr>
    <tr>
      <th>133</th>
      <td>Korea</td>
      <td>None</td>
      <td>3769</td>
    </tr>
    <tr>
      <th>134</th>
      <td>Korea</td>
      <td>One or two times</td>
      <td>868</td>
    </tr>
    <tr>
      <th>135</th>
      <td>Korea</td>
      <td>Three or four times</td>
      <td>229</td>
    </tr>
    <tr>
      <th>136</th>
      <td>Latvia</td>
      <td>Five or more times</td>
      <td>358</td>
    </tr>
    <tr>
      <th>137</th>
      <td>Latvia</td>
      <td>None</td>
      <td>1876</td>
    </tr>
    <tr>
      <th>138</th>
      <td>Latvia</td>
      <td>One or two times</td>
      <td>1488</td>
    </tr>
    <tr>
      <th>139</th>
      <td>Latvia</td>
      <td>Three or four times</td>
      <td>552</td>
    </tr>
    <tr>
      <th>140</th>
      <td>Liechtenstein</td>
      <td>Five or more times</td>
      <td>3</td>
    </tr>
    <tr>
      <th>141</th>
      <td>Liechtenstein</td>
      <td>None</td>
      <td>237</td>
    </tr>
    <tr>
      <th>142</th>
      <td>Liechtenstein</td>
      <td>One or two times</td>
      <td>48</td>
    </tr>
    <tr>
      <th>143</th>
      <td>Liechtenstein</td>
      <td>Three or four times</td>
      <td>3</td>
    </tr>
    <tr>
      <th>144</th>
      <td>Lithuania</td>
      <td>Five or more times</td>
      <td>227</td>
    </tr>
    <tr>
      <th>145</th>
      <td>Lithuania</td>
      <td>None</td>
      <td>2575</td>
    </tr>
    <tr>
      <th>146</th>
      <td>Lithuania</td>
      <td>One or two times</td>
      <td>1447</td>
    </tr>
    <tr>
      <th>147</th>
      <td>Lithuania</td>
      <td>Three or four times</td>
      <td>349</td>
    </tr>
    <tr>
      <th>148</th>
      <td>Luxembourg</td>
      <td>Five or more times</td>
      <td>163</td>
    </tr>
    <tr>
      <th>149</th>
      <td>Luxembourg</td>
      <td>None</td>
      <td>3720</td>
    </tr>
    <tr>
      <th>150</th>
      <td>Luxembourg</td>
      <td>One or two times</td>
      <td>1118</td>
    </tr>
    <tr>
      <th>151</th>
      <td>Luxembourg</td>
      <td>Three or four times</td>
      <td>237</td>
    </tr>
    <tr>
      <th>152</th>
      <td>Macao-China</td>
      <td>Five or more times</td>
      <td>81</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Macao-China</td>
      <td>None</td>
      <td>3984</td>
    </tr>
    <tr>
      <th>154</th>
      <td>Macao-China</td>
      <td>One or two times</td>
      <td>1108</td>
    </tr>
    <tr>
      <th>155</th>
      <td>Macao-China</td>
      <td>Three or four times</td>
      <td>143</td>
    </tr>
    <tr>
      <th>156</th>
      <td>Malaysia</td>
      <td>Five or more times</td>
      <td>208</td>
    </tr>
    <tr>
      <th>157</th>
      <td>Malaysia</td>
      <td>None</td>
      <td>3452</td>
    </tr>
    <tr>
      <th>158</th>
      <td>Malaysia</td>
      <td>One or two times</td>
      <td>1204</td>
    </tr>
    <tr>
      <th>159</th>
      <td>Malaysia</td>
      <td>Three or four times</td>
      <td>311</td>
    </tr>
    <tr>
      <th>160</th>
      <td>Massachusetts (USA)</td>
      <td>Five or more times</td>
      <td>31</td>
    </tr>
    <tr>
      <th>161</th>
      <td>Massachusetts (USA)</td>
      <td>None</td>
      <td>1271</td>
    </tr>
    <tr>
      <th>162</th>
      <td>Massachusetts (USA)</td>
      <td>One or two times</td>
      <td>342</td>
    </tr>
    <tr>
      <th>163</th>
      <td>Massachusetts (USA)</td>
      <td>Three or four times</td>
      <td>61</td>
    </tr>
    <tr>
      <th>164</th>
      <td>Mexico</td>
      <td>Five or more times</td>
      <td>738</td>
    </tr>
    <tr>
      <th>165</th>
      <td>Mexico</td>
      <td>None</td>
      <td>20106</td>
    </tr>
    <tr>
      <th>166</th>
      <td>Mexico</td>
      <td>One or two times</td>
      <td>10796</td>
    </tr>
    <tr>
      <th>167</th>
      <td>Mexico</td>
      <td>Three or four times</td>
      <td>1930</td>
    </tr>
    <tr>
      <th>168</th>
      <td>Montenegro</td>
      <td>Five or more times</td>
      <td>208</td>
    </tr>
    <tr>
      <th>169</th>
      <td>Montenegro</td>
      <td>None</td>
      <td>2874</td>
    </tr>
    <tr>
      <th>170</th>
      <td>Montenegro</td>
      <td>One or two times</td>
      <td>1361</td>
    </tr>
    <tr>
      <th>171</th>
      <td>Montenegro</td>
      <td>Three or four times</td>
      <td>240</td>
    </tr>
    <tr>
      <th>172</th>
      <td>Netherlands</td>
      <td>Five or more times</td>
      <td>149</td>
    </tr>
    <tr>
      <th>173</th>
      <td>Netherlands</td>
      <td>None</td>
      <td>3024</td>
    </tr>
    <tr>
      <th>174</th>
      <td>Netherlands</td>
      <td>One or two times</td>
      <td>1052</td>
    </tr>
    <tr>
      <th>175</th>
      <td>Netherlands</td>
      <td>Three or four times</td>
      <td>173</td>
    </tr>
    <tr>
      <th>176</th>
      <td>New Zealand</td>
      <td>Five or more times</td>
      <td>211</td>
    </tr>
    <tr>
      <th>177</th>
      <td>New Zealand</td>
      <td>None</td>
      <td>2473</td>
    </tr>
    <tr>
      <th>178</th>
      <td>New Zealand</td>
      <td>One or two times</td>
      <td>1177</td>
    </tr>
    <tr>
      <th>179</th>
      <td>New Zealand</td>
      <td>Three or four times</td>
      <td>362</td>
    </tr>
    <tr>
      <th>180</th>
      <td>Norway</td>
      <td>Five or more times</td>
      <td>141</td>
    </tr>
    <tr>
      <th>181</th>
      <td>Norway</td>
      <td>None</td>
      <td>3241</td>
    </tr>
    <tr>
      <th>182</th>
      <td>Norway</td>
      <td>One or two times</td>
      <td>967</td>
    </tr>
    <tr>
      <th>183</th>
      <td>Norway</td>
      <td>Three or four times</td>
      <td>223</td>
    </tr>
    <tr>
      <th>184</th>
      <td>Perm(Russian Federation)</td>
      <td>Five or more times</td>
      <td>187</td>
    </tr>
    <tr>
      <th>185</th>
      <td>Perm(Russian Federation)</td>
      <td>None</td>
      <td>792</td>
    </tr>
    <tr>
      <th>186</th>
      <td>Perm(Russian Federation)</td>
      <td>One or two times</td>
      <td>570</td>
    </tr>
    <tr>
      <th>187</th>
      <td>Perm(Russian Federation)</td>
      <td>Three or four times</td>
      <td>205</td>
    </tr>
    <tr>
      <th>188</th>
      <td>Peru</td>
      <td>Five or more times</td>
      <td>317</td>
    </tr>
    <tr>
      <th>189</th>
      <td>Peru</td>
      <td>None</td>
      <td>2846</td>
    </tr>
    <tr>
      <th>190</th>
      <td>Peru</td>
      <td>One or two times</td>
      <td>2181</td>
    </tr>
    <tr>
      <th>191</th>
      <td>Peru</td>
      <td>Three or four times</td>
      <td>654</td>
    </tr>
    <tr>
      <th>192</th>
      <td>Poland</td>
      <td>Five or more times</td>
      <td>294</td>
    </tr>
    <tr>
      <th>193</th>
      <td>Poland</td>
      <td>None</td>
      <td>2631</td>
    </tr>
    <tr>
      <th>194</th>
      <td>Poland</td>
      <td>One or two times</td>
      <td>1291</td>
    </tr>
    <tr>
      <th>195</th>
      <td>Poland</td>
      <td>Three or four times</td>
      <td>366</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Portugal</td>
      <td>Five or more times</td>
      <td>334</td>
    </tr>
    <tr>
      <th>197</th>
      <td>Portugal</td>
      <td>None</td>
      <td>2501</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Portugal</td>
      <td>One or two times</td>
      <td>2185</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Portugal</td>
      <td>Three or four times</td>
      <td>614</td>
    </tr>
    <tr>
      <th>200</th>
      <td>Qatar</td>
      <td>Five or more times</td>
      <td>553</td>
    </tr>
    <tr>
      <th>201</th>
      <td>Qatar</td>
      <td>None</td>
      <td>6552</td>
    </tr>
    <tr>
      <th>202</th>
      <td>Qatar</td>
      <td>One or two times</td>
      <td>2910</td>
    </tr>
    <tr>
      <th>203</th>
      <td>Qatar</td>
      <td>Three or four times</td>
      <td>811</td>
    </tr>
    <tr>
      <th>204</th>
      <td>Romania</td>
      <td>Five or more times</td>
      <td>319</td>
    </tr>
    <tr>
      <th>205</th>
      <td>Romania</td>
      <td>None</td>
      <td>2749</td>
    </tr>
    <tr>
      <th>206</th>
      <td>Romania</td>
      <td>One or two times</td>
      <td>1597</td>
    </tr>
    <tr>
      <th>207</th>
      <td>Romania</td>
      <td>Three or four times</td>
      <td>391</td>
    </tr>
    <tr>
      <th>208</th>
      <td>Russian Federation</td>
      <td>Five or more times</td>
      <td>420</td>
    </tr>
    <tr>
      <th>209</th>
      <td>Russian Federation</td>
      <td>None</td>
      <td>2731</td>
    </tr>
    <tr>
      <th>210</th>
      <td>Russian Federation</td>
      <td>One or two times</td>
      <td>1609</td>
    </tr>
    <tr>
      <th>211</th>
      <td>Russian Federation</td>
      <td>Three or four times</td>
      <td>442</td>
    </tr>
    <tr>
      <th>212</th>
      <td>Serbia</td>
      <td>Five or more times</td>
      <td>225</td>
    </tr>
    <tr>
      <th>213</th>
      <td>Serbia</td>
      <td>None</td>
      <td>2686</td>
    </tr>
    <tr>
      <th>214</th>
      <td>Serbia</td>
      <td>One or two times</td>
      <td>1411</td>
    </tr>
    <tr>
      <th>215</th>
      <td>Serbia</td>
      <td>Three or four times</td>
      <td>306</td>
    </tr>
    <tr>
      <th>216</th>
      <td>Singapore</td>
      <td>Five or more times</td>
      <td>74</td>
    </tr>
    <tr>
      <th>217</th>
      <td>Singapore</td>
      <td>None</td>
      <td>4364</td>
    </tr>
    <tr>
      <th>218</th>
      <td>Singapore</td>
      <td>One or two times</td>
      <td>947</td>
    </tr>
    <tr>
      <th>219</th>
      <td>Singapore</td>
      <td>Three or four times</td>
      <td>138</td>
    </tr>
    <tr>
      <th>220</th>
      <td>Slovak Republic</td>
      <td>Five or more times</td>
      <td>110</td>
    </tr>
    <tr>
      <th>221</th>
      <td>Slovak Republic</td>
      <td>None</td>
      <td>3410</td>
    </tr>
    <tr>
      <th>222</th>
      <td>Slovak Republic</td>
      <td>One or two times</td>
      <td>944</td>
    </tr>
    <tr>
      <th>223</th>
      <td>Slovak Republic</td>
      <td>Three or four times</td>
      <td>166</td>
    </tr>
    <tr>
      <th>224</th>
      <td>Slovenia</td>
      <td>Five or more times</td>
      <td>306</td>
    </tr>
    <tr>
      <th>225</th>
      <td>Slovenia</td>
      <td>None</td>
      <td>3466</td>
    </tr>
    <tr>
      <th>226</th>
      <td>Slovenia</td>
      <td>One or two times</td>
      <td>1716</td>
    </tr>
    <tr>
      <th>227</th>
      <td>Slovenia</td>
      <td>Three or four times</td>
      <td>355</td>
    </tr>
    <tr>
      <th>228</th>
      <td>Spain</td>
      <td>Five or more times</td>
      <td>1122</td>
    </tr>
    <tr>
      <th>229</th>
      <td>Spain</td>
      <td>None</td>
      <td>16396</td>
    </tr>
    <tr>
      <th>230</th>
      <td>Spain</td>
      <td>One or two times</td>
      <td>5918</td>
    </tr>
    <tr>
      <th>231</th>
      <td>Spain</td>
      <td>Three or four times</td>
      <td>1546</td>
    </tr>
    <tr>
      <th>232</th>
      <td>Sweden</td>
      <td>Five or more times</td>
      <td>383</td>
    </tr>
    <tr>
      <th>233</th>
      <td>Sweden</td>
      <td>None</td>
      <td>2068</td>
    </tr>
    <tr>
      <th>234</th>
      <td>Sweden</td>
      <td>One or two times</td>
      <td>1594</td>
    </tr>
    <tr>
      <th>235</th>
      <td>Sweden</td>
      <td>Three or four times</td>
      <td>591</td>
    </tr>
    <tr>
      <th>236</th>
      <td>Switzerland</td>
      <td>Five or more times</td>
      <td>212</td>
    </tr>
    <tr>
      <th>237</th>
      <td>Switzerland</td>
      <td>None</td>
      <td>8241</td>
    </tr>
    <tr>
      <th>238</th>
      <td>Switzerland</td>
      <td>One or two times</td>
      <td>2232</td>
    </tr>
    <tr>
      <th>239</th>
      <td>Switzerland</td>
      <td>Three or four times</td>
      <td>402</td>
    </tr>
    <tr>
      <th>240</th>
      <td>Thailand</td>
      <td>Five or more times</td>
      <td>233</td>
    </tr>
    <tr>
      <th>241</th>
      <td>Thailand</td>
      <td>None</td>
      <td>4431</td>
    </tr>
    <tr>
      <th>242</th>
      <td>Thailand</td>
      <td>One or two times</td>
      <td>1537</td>
    </tr>
    <tr>
      <th>243</th>
      <td>Thailand</td>
      <td>Three or four times</td>
      <td>394</td>
    </tr>
    <tr>
      <th>244</th>
      <td>Tunisia</td>
      <td>Five or more times</td>
      <td>240</td>
    </tr>
    <tr>
      <th>245</th>
      <td>Tunisia</td>
      <td>None</td>
      <td>2102</td>
    </tr>
    <tr>
      <th>246</th>
      <td>Tunisia</td>
      <td>One or two times</td>
      <td>1655</td>
    </tr>
    <tr>
      <th>247</th>
      <td>Tunisia</td>
      <td>Three or four times</td>
      <td>328</td>
    </tr>
    <tr>
      <th>248</th>
      <td>Turkey</td>
      <td>Five or more times</td>
      <td>250</td>
    </tr>
    <tr>
      <th>249</th>
      <td>Turkey</td>
      <td>None</td>
      <td>2725</td>
    </tr>
    <tr>
      <th>250</th>
      <td>Turkey</td>
      <td>One or two times</td>
      <td>1437</td>
    </tr>
    <tr>
      <th>251</th>
      <td>Turkey</td>
      <td>Three or four times</td>
      <td>402</td>
    </tr>
    <tr>
      <th>252</th>
      <td>United Arab Emirates</td>
      <td>Five or more times</td>
      <td>403</td>
    </tr>
    <tr>
      <th>253</th>
      <td>United Arab Emirates</td>
      <td>None</td>
      <td>7812</td>
    </tr>
    <tr>
      <th>254</th>
      <td>United Arab Emirates</td>
      <td>One or two times</td>
      <td>2621</td>
    </tr>
    <tr>
      <th>255</th>
      <td>United Arab Emirates</td>
      <td>Three or four times</td>
      <td>571</td>
    </tr>
    <tr>
      <th>256</th>
      <td>United Kingdom</td>
      <td>Five or more times</td>
      <td>405</td>
    </tr>
    <tr>
      <th>257</th>
      <td>United Kingdom</td>
      <td>None</td>
      <td>8437</td>
    </tr>
    <tr>
      <th>258</th>
      <td>United Kingdom</td>
      <td>One or two times</td>
      <td>2956</td>
    </tr>
    <tr>
      <th>259</th>
      <td>United Kingdom</td>
      <td>Three or four times</td>
      <td>717</td>
    </tr>
    <tr>
      <th>260</th>
      <td>United States of America</td>
      <td>Five or more times</td>
      <td>145</td>
    </tr>
    <tr>
      <th>261</th>
      <td>United States of America</td>
      <td>None</td>
      <td>3440</td>
    </tr>
    <tr>
      <th>262</th>
      <td>United States of America</td>
      <td>One or two times</td>
      <td>1083</td>
    </tr>
    <tr>
      <th>263</th>
      <td>United States of America</td>
      <td>Three or four times</td>
      <td>244</td>
    </tr>
    <tr>
      <th>264</th>
      <td>Uruguay</td>
      <td>Five or more times</td>
      <td>453</td>
    </tr>
    <tr>
      <th>265</th>
      <td>Uruguay</td>
      <td>None</td>
      <td>2134</td>
    </tr>
    <tr>
      <th>266</th>
      <td>Uruguay</td>
      <td>One or two times</td>
      <td>2002</td>
    </tr>
    <tr>
      <th>267</th>
      <td>Uruguay</td>
      <td>Three or four times</td>
      <td>658</td>
    </tr>
    <tr>
      <th>268</th>
      <td>Vietnam</td>
      <td>Five or more times</td>
      <td>31</td>
    </tr>
    <tr>
      <th>269</th>
      <td>Vietnam</td>
      <td>None</td>
      <td>4154</td>
    </tr>
    <tr>
      <th>270</th>
      <td>Vietnam</td>
      <td>One or two times</td>
      <td>694</td>
    </tr>
    <tr>
      <th>271</th>
      <td>Vietnam</td>
      <td>Three or four times</td>
      <td>71</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Top 5 Countries in which most students skip school
# Omit students that did not skip school and count the rest together
pisa_students_skip = pisa_agg_skip[pisa_agg_skip.SKIPPED_SCHOOL != 'None'].groupby('COUNTRY').sum().sort_values(by= 'COUNT', ascending= False)
pisa_students_skip.head()
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
      <th>COUNT</th>
    </tr>
    <tr>
      <th>COUNTRY</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mexico</th>
      <td>13464</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>10101</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>8586</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>8416</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>6487</td>
    </tr>
  </tbody>
</table>
</div>



##### Findings
The most students that skip school are from Mexico, but countries have different sizes of students participating and the output above must not tell the truth.  
##### Define
A percentage of all students per country will be calculated to receive a more accurate analysis.
##### Code


```python
# Divide student count that have skipped school with all students participating per country
pisa_students_skip_ratio = pisa_students_skip/pisa_agg_skip.groupby('COUNTRY').sum()
# Top 5 countries that students skip the most frequent school
pisa_students_skip_ratio.sort_values(by= 'COUNT', ascending= False).head()
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
      <th>COUNT</th>
    </tr>
    <tr>
      <th>COUNTRY</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Uruguay</th>
      <td>0.593291</td>
    </tr>
    <tr>
      <th>Bulgaria</th>
      <td>0.585086</td>
    </tr>
    <tr>
      <th>Costa Rica</th>
      <td>0.573928</td>
    </tr>
    <tr>
      <th>Latvia</th>
      <td>0.561067</td>
    </tr>
    <tr>
      <th>Portugal</th>
      <td>0.556088</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Top 5 countries that students do not skip school
pisa_students_skip_ratio.sort_values(by= 'COUNT', ascending= True).head()
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
      <th>COUNT</th>
    </tr>
    <tr>
      <th>COUNTRY</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Japan</th>
      <td>0.090022</td>
    </tr>
    <tr>
      <th>Hong Kong-China</th>
      <td>0.145852</td>
    </tr>
    <tr>
      <th>Vietnam</th>
      <td>0.160808</td>
    </tr>
    <tr>
      <th>China-Shanghai</th>
      <td>0.167505</td>
    </tr>
    <tr>
      <th>Liechtenstein</th>
      <td>0.185567</td>
    </tr>
  </tbody>
</table>
</div>



##### Findings
None of the contries in the first analysis have made it in the top 5 list. It is striking that almost an alarming 60% of all students in Uruguay have skipped at least once school. On the other hand, it is remarkable that less than 10% of Japans students have missed school. Congrat's Japan for your outstanding students.

### Bivariate Exploration
##### Define
In the bivariate exploration I want to compare the scores from the countries from the previous analysis with the highest and lowest attendance, which are Japan and Uruguay.
##### Code


```python
# create figure
plt.figure(figsize = [25, 10])
# whitespace between subplots
plt.subplots_adjust(wspace = 0.60) 

plt.suptitle('Score Comparison Japan vs. Uruguay', fontsize= 30)

# 1. subplot
plt.subplot(1, 4, 1)
# set up boxplot
sb.boxplot(x = pisa_skip_school['MATH'], y = pisa_skip_school[pisa_skip_school['COUNTRY'].isin(['Uruguay', 'Japan'])]['COUNTRY'], 
           color=sb.color_palette('Set1')[0]);
# fine-tuning
plt.yticks(fontsize= 10)
plt.xticks(fontsize= 10)
plt.xlabel('MATH', fontsize= 15)
plt.ylabel('COUNTRY',fontsize= 15)

# 2. subplot
plt.subplot(1, 4, 2)
# set up boxplot
sb.boxplot(x = pisa_skip_school['READ'], y = pisa_skip_school[pisa_skip_school['COUNTRY'].isin(['Uruguay', 'Japan'])]['COUNTRY'], 
           color=sb.color_palette('Set1')[1]);
# fine-tuning
plt.yticks(fontsize= 10)
plt.xticks(fontsize= 10)
plt.xlabel('READ', fontsize= 15)
plt.ylabel('COUNTRY',fontsize= 15)

# 3. subplot
plt.subplot(1, 4, 3)
# set up boxplot
sb.boxplot(x = pisa_skip_school['SCIENCE'], y = pisa_skip_school[pisa_skip_school['COUNTRY'].isin(['Uruguay', 'Japan'])]['COUNTRY'], 
           color=sb.color_palette('Set1')[2]);
# fine-tuning
plt.yticks(fontsize= 10)
plt.xticks(fontsize= 10)
plt.xlabel('SCIENCE', fontsize= 15)
plt.ylabel('COUNTRY',fontsize= 15)

# 4. subplot
plt.subplot(1, 4, 4)
# set up boxplot
sb.boxplot(x = pisa_skip_school['AVG_SCORE'], y = pisa_skip_school[pisa_skip_school['COUNTRY'].isin(['Uruguay', 'Japan'])]['COUNTRY'], 
           color=sb.color_palette('Set1')[3]);
plt.yticks(fontsize= 10)
plt.xticks(fontsize= 10)
plt.xlabel('AVG_SCORE', fontsize= 15)
plt.ylabel('COUNTRY',fontsize= 15);

# save plot as png
plt.savefig('bivariate_bp_ScoreComparisonJapUru.png')
plt.show()
```


![png](output_75_0.png)


##### Findings
In each category is Japan receives higher scores than Uruguay. Even the third quantil of Uruguay does not reach the first quantil of Japan. Of course, there are some "outliers" of students that out perform the general students and can compare themselfs with the best students in Japan but short story short Japan has better scoring students.

### Multivariate Exploration
##### Define
Now that the both best countries in each field have been compared, a more thorough visualization will be shown where multiple variables will be shown. For example, see which students perform bad and skipped school.
##### Code


```python
# create figure
plt.figure(figsize = [25, 15])
# make scatterplot
sb.scatterplot(x= 'STUDENT_ID', y= 'AVG_SCORE', hue= 'SKIPPED_SCHOOL', size= 'SKIPPED_SCHOOL', style= 'COUNTRY', data= pisa_skip_school[pisa_skip_school['COUNTRY'].isin(['Uruguay','Japan'])]);
# fine-tuning
plt.title('Score Comparison Japan vs. Uruguay', fontsize= 30)
plt.yticks(fontsize= 15)
plt.xticks(fontsize= 15)
plt.xlabel('Students', fontsize= 20)
plt.ylabel('Average Score',fontsize= 20)
plt.legend(fontsize='x-large', title_fontsize='40')

# save plot as png
plt.savefig('multivariate_sp_ScoreStudents.png')
plt.show()
```


![png](output_78_0.png)


##### Findings
This plot shows clearly that the higher the grade is the lesser the possibility of a student skipping school. This is visible as all students have never skipped school are colored red. There is a threshold at around **550** to see where the students drastically disapear that have skipped school. But of course there are some outliers as well to see, that managed to reach a score of more than 600.  
It appears as in the previous investigations that Uruguay has significantly more students that have skipped school than Japan.

# Conclusion
All my questions coulb be answered. It is interesting to compare two countries that have a bigger gap between the scores. The outliers are much more visible and the findings are easier to see.
