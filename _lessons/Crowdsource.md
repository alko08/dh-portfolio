---
layout: page
title: Crowdsourced Data Normalization with Python and Pandas
description: This lesson uses Python and Pandas to normalize crowdsourced data.
---

## Source
[Programming Historian Crowdsourced Data Normalization with Python and Pandas](https://discord.com/channels/877073567307665469/877073568779862038/1029160663882407936)

## Reflection
Crowdsourcing is an important concept. It is used daily to collect, refine, and analyze data. I personally helped run a crowdsourcing volunteer program using the tool BillionGraves, to record and transcribe graves from my local cemetery. It would take a long time for one human to go around and take photos of every grave on the planet, so BillionGraves lets anyone takes pictures and upload them to their site. Then on the site, the photos are categorized and transcribed by people using their site. After that, the photos are then just uploaded to their site for anyone to view. Though as Brandon Walsh covers, there are a few problems with this idea. 

For one, what if we used a machine to transcribe the graves instead of humans? Well, transcribing all these graves would be computationally expensive, and sometimes not even work if the photo quality is poor. Then along those lines, what happens to the poor-quality photos or old graves that not even a human can categorize? This would be where the analysis of data through a program does come into play. Using a script like used here, BillionGraves can make sure that graves with no possible transcription get sorted separately and do not contaminate the data that the transcribers look through. That way they can make sure that the valuable time of the transcribers is first spent on actually possible graves instead of ones that are impossible. This algorithm could even assign transcribers to previously transcribed graves to check for user error or generate partial prefilled transcriptions to speed up their jobs (which BillionGraves does).
 

## Code


```python
# First make sure pandas is installed.
pip install pandas==1.2.0
```


      Input In [1]
        pip install pandas==1.2.0
            ^
    SyntaxError: invalid syntax
    



```python
import pandas as pd

# Read from data from file "Menu.csv"
df = pd.read_csv("Menu.csv")

# Display the first 5 rows (0 through 4)
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
      <th>id</th>
      <th>name</th>
      <th>sponsor</th>
      <th>event</th>
      <th>venue</th>
      <th>place</th>
      <th>physical_description</th>
      <th>occasion</th>
      <th>notes</th>
      <th>call_number</th>
      <th>keywords</th>
      <th>language</th>
      <th>date</th>
      <th>location</th>
      <th>location_type</th>
      <th>currency</th>
      <th>currency_symbol</th>
      <th>status</th>
      <th>page_count</th>
      <th>dish_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12463</td>
      <td>NaN</td>
      <td>HOTEL EASTMAN</td>
      <td>BREAKFAST</td>
      <td>COMMERCIAL</td>
      <td>HOT SPRINGS, AR</td>
      <td>CARD; 4.75X7.5;</td>
      <td>EASTER;</td>
      <td>NaN</td>
      <td>1900-2822</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4/15/1900</td>
      <td>Hotel Eastman</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>complete</td>
      <td>2</td>
      <td>67</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12464</td>
      <td>NaN</td>
      <td>REPUBLICAN HOUSE</td>
      <td>[DINNER]</td>
      <td>COMMERCIAL</td>
      <td>MILWAUKEE, [WI];</td>
      <td>CARD; ILLUS; COL; 7.0X9.0;</td>
      <td>EASTER;</td>
      <td>WEDGEWOOD BLUE CARD; WHITE EMBOSSED GREEK KEY ...</td>
      <td>1900-2825</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4/15/1900</td>
      <td>Republican House</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>complete</td>
      <td>2</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12465</td>
      <td>NaN</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>FRUHSTUCK/BREAKFAST;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>CARD; ILLU; COL; 5.5X8.0;</td>
      <td>NaN</td>
      <td>MENU IN GERMAN AND ENGLISH; ILLUS, STEAMSHIP A...</td>
      <td>1900-2827</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>complete</td>
      <td>2</td>
      <td>84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12466</td>
      <td>NaN</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>LUNCH;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>CARD; ILLU; COL; 5.5X8.0;</td>
      <td>NaN</td>
      <td>MENU IN GERMAN AND ENGLISH; ILLUS, HARBOR SCEN...</td>
      <td>1900-2828</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>complete</td>
      <td>2</td>
      <td>63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12467</td>
      <td>NaN</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>DINNER;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>FOLDER; ILLU; COL; 5.5X7.5;</td>
      <td>NaN</td>
      <td>MENU IN GERMAN AND ENGLISH; ILLUS, HARBOR SCEN...</td>
      <td>1900-2829</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>complete</td>
      <td>4</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Display the list of all columns names
df.columns 
```




    Index(['id', 'name', 'sponsor', 'event', 'venue', 'place',
           'physical_description', 'occasion', 'notes', 'call_number', 'keywords',
           'language', 'date', 'location', 'location_type', 'currency',
           'currency_symbol', 'status', 'page_count', 'dish_count'],
          dtype='object')




```python
# Now we will be removing unimportant columns that clutter the data and take up space. (And are just confusing)
dropped_col = ['notes', 'call_number', 'currency', 'currency_symbol', 'physical_description', 'status']
df.drop(dropped_col, inplace=True, axis=1)

# Display columns left (should be 14)
df.shape    # Displays as (rows, colums)
```




    (17546, 14)




```python
# Find if any duplicate rows exist (one does)
df[df.duplicated(keep=False)]

# Remove duplicate rows
df.drop_duplicates(inplace=True)

# Display rows left (should be one minus rows before)
df.shape    # Displays as (rows, colums)
```




    (17545, 14)




```python
# print how much null data appears in each column (out of rows shown above)
df.isnull().sum()
```




    id                   0
    name             14348
    sponsor           1561
    event             9391
    venue             9426
    place             9422
    occasion         13754
    keywords         17545
    language         17545
    date               586
    location             0
    location_type    17545
    page_count           0
    dish_count           0
    dtype: int64




```python
# lets drop all data columns that are over 75% null 
menu = df.dropna(thresh=df.shape[0]*0.25,how='all',axis=1)
menu.shape
```




    (17545, 9)




```python
# I know the tutorial says 25% but their code does 75% for some reason. As shown below.
menu.isnull().sum()
```




    id               0
    sponsor       1561
    event         9391
    venue         9426
    place         9422
    date           586
    location         0
    page_count       0
    dish_count       0
    dtype: int64




```python
# Now lets drop rows with missing data and complete a dataset with only complete rows.
dropped_na = menu.dropna()
dropped_na
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
      <th>id</th>
      <th>sponsor</th>
      <th>event</th>
      <th>venue</th>
      <th>place</th>
      <th>date</th>
      <th>location</th>
      <th>page_count</th>
      <th>dish_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12463</td>
      <td>HOTEL EASTMAN</td>
      <td>BREAKFAST</td>
      <td>COMMERCIAL</td>
      <td>HOT SPRINGS, AR</td>
      <td>4/15/1900</td>
      <td>Hotel Eastman</td>
      <td>2</td>
      <td>67</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12464</td>
      <td>REPUBLICAN HOUSE</td>
      <td>[DINNER]</td>
      <td>COMMERCIAL</td>
      <td>MILWAUKEE, [WI];</td>
      <td>4/15/1900</td>
      <td>Republican House</td>
      <td>2</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12465</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>FRUHSTUCK/BREAKFAST;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>2</td>
      <td>84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12466</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>LUNCH;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>2</td>
      <td>63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12467</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>DINNER;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>4</td>
      <td>33</td>
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
    </tr>
    <tr>
      <th>10212</th>
      <td>27695</td>
      <td>CONFRERIE DE LA CHAINE DES ROTISSEURS, NEW ORL...</td>
      <td>DINNER</td>
      <td>OTHER (PRIVATE CLUB)</td>
      <td>PLIMSOLL CLUB, NEW ORLEANS, LA</td>
      <td>5/13/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs, New Orl...</td>
      <td>5</td>
      <td>37</td>
    </tr>
    <tr>
      <th>10213</th>
      <td>27696</td>
      <td>CONFRERIE DE LA CHAINE DES ROTISSEURS, GEORGIA...</td>
      <td>DINNER</td>
      <td>OTHER (PRIVATE CLUB)</td>
      <td>PIEDMONT DRIVING  CLUB,  [ATLANTA?] GEORGIA</td>
      <td>5/18/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs</td>
      <td>3</td>
      <td>22</td>
    </tr>
    <tr>
      <th>10214</th>
      <td>27697</td>
      <td>FRANKFURTER STUBB</td>
      <td>DAILY MENU</td>
      <td>HOTEL; FOR</td>
      <td>HOTEL FRANKFURTER, FRANFURT AM MAIN, GERMANY</td>
      <td>6/3/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs</td>
      <td>3</td>
      <td>34</td>
    </tr>
    <tr>
      <th>10215</th>
      <td>27698</td>
      <td>HOTEL EUROPAISCHER HOF</td>
      <td>DINNER</td>
      <td>HOTEL; FOR</td>
      <td>HEIDELBERG, GERMANY</td>
      <td>6/26/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs, New Orl...</td>
      <td>1</td>
      <td>31</td>
    </tr>
    <tr>
      <th>10216</th>
      <td>27699</td>
      <td>CONFRERIE DE LA CHAINE DES ROTISSEURS, OKLAHOM...</td>
      <td>INAUGURATION OF THE OKLAHOME CHAPTER</td>
      <td>OTHER (PRIVATE CLUB)</td>
      <td>OKLAHOMA CITY GOLF AND COUNTRY CLUB, OKLAHOMA ...</td>
      <td>7/1/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs</td>
      <td>4</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
<p>7236 rows × 9 columns</p>
</div>




```python
# Now lets deal with dates.
# There are many ways to put in the same date, so we will use pandas to make our data have a universal pattern.

# This code returns an error of an out of range date, which we change below.
# pd.to_datetime(dropped_na['date'], dayfirst = False, yearfirst = False)

# Change out of range date, then save data as a new CSV file!
replaced_date = dropped_na.replace('0190-03-06', '12-31-2220')
replaced_date.to_csv("NYPL_NormalMenus.csv")
```


```python
# Display final data
replaced_date
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
      <th>id</th>
      <th>sponsor</th>
      <th>event</th>
      <th>venue</th>
      <th>place</th>
      <th>date</th>
      <th>location</th>
      <th>page_count</th>
      <th>dish_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12463</td>
      <td>HOTEL EASTMAN</td>
      <td>BREAKFAST</td>
      <td>COMMERCIAL</td>
      <td>HOT SPRINGS, AR</td>
      <td>4/15/1900</td>
      <td>Hotel Eastman</td>
      <td>2</td>
      <td>67</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12464</td>
      <td>REPUBLICAN HOUSE</td>
      <td>[DINNER]</td>
      <td>COMMERCIAL</td>
      <td>MILWAUKEE, [WI];</td>
      <td>4/15/1900</td>
      <td>Republican House</td>
      <td>2</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12465</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>FRUHSTUCK/BREAKFAST;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>2</td>
      <td>84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12466</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>LUNCH;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>2</td>
      <td>63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12467</td>
      <td>NORDDEUTSCHER LLOYD BREMEN</td>
      <td>DINNER;</td>
      <td>COMMERCIAL</td>
      <td>DAMPFER KAISER WILHELM DER GROSSE;</td>
      <td>4/16/1900</td>
      <td>Norddeutscher Lloyd Bremen</td>
      <td>4</td>
      <td>33</td>
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
    </tr>
    <tr>
      <th>10212</th>
      <td>27695</td>
      <td>CONFRERIE DE LA CHAINE DES ROTISSEURS, NEW ORL...</td>
      <td>DINNER</td>
      <td>OTHER (PRIVATE CLUB)</td>
      <td>PLIMSOLL CLUB, NEW ORLEANS, LA</td>
      <td>5/13/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs, New Orl...</td>
      <td>5</td>
      <td>37</td>
    </tr>
    <tr>
      <th>10213</th>
      <td>27696</td>
      <td>CONFRERIE DE LA CHAINE DES ROTISSEURS, GEORGIA...</td>
      <td>DINNER</td>
      <td>OTHER (PRIVATE CLUB)</td>
      <td>PIEDMONT DRIVING  CLUB,  [ATLANTA?] GEORGIA</td>
      <td>5/18/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs</td>
      <td>3</td>
      <td>22</td>
    </tr>
    <tr>
      <th>10214</th>
      <td>27697</td>
      <td>FRANKFURTER STUBB</td>
      <td>DAILY MENU</td>
      <td>HOTEL; FOR</td>
      <td>HOTEL FRANKFURTER, FRANFURT AM MAIN, GERMANY</td>
      <td>6/3/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs</td>
      <td>3</td>
      <td>34</td>
    </tr>
    <tr>
      <th>10215</th>
      <td>27698</td>
      <td>HOTEL EUROPAISCHER HOF</td>
      <td>DINNER</td>
      <td>HOTEL; FOR</td>
      <td>HEIDELBERG, GERMANY</td>
      <td>6/26/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs, New Orl...</td>
      <td>1</td>
      <td>31</td>
    </tr>
    <tr>
      <th>10216</th>
      <td>27699</td>
      <td>CONFRERIE DE LA CHAINE DES ROTISSEURS, OKLAHOM...</td>
      <td>INAUGURATION OF THE OKLAHOME CHAPTER</td>
      <td>OTHER (PRIVATE CLUB)</td>
      <td>OKLAHOMA CITY GOLF AND COUNTRY CLUB, OKLAHOMA ...</td>
      <td>7/1/1968</td>
      <td>Confrerie De La Chaine Des Rotisseurs</td>
      <td>4</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
<p>7236 rows × 9 columns</p>
</div>


