![Futuristic electric car charging](ev_charging.png)

The US Government's Alternative Fuels Data Center collects records of electric vehicle (EV) charging infrastructure, including charging ports and station locations, as well as sales of electric vehicles. With the EV market rapidly evolving, understanding trends in charging facilities and sales is essential to inform strategic planning.

As a data scientist working for a leading EV charging network operator, you recognize the potential in this data and start wrangling and visualizing the aggregated yearly data. 

This yearly data captured in December of each year encompasses a record of EV charging port installations and station localities spanning roughly ten years, capturing both public and private charging environments. 
___

### The Data
&nbsp;

`private_ev_charging.csv`

| Variable   | Description                                          |
|------------|------------------------------------------------------|
| `year` |  Year of data collection |
| `private_ports`| The number of available charging ports owned by private companies in a given year  |
| `private_station_locations`   | The number of privately owned station locations for EV charging

___

`public_ev_charging.csv`
 
| Variable   | Description                                          |
|------------|------------------------------------------------------|
| `year` |  Year of data collection  |
| `public_ports`| The number of available charging ports under public ownership in a given year  |
| `public_station_locations`   | The number of publicly owned station locations for EV charging

___

The sales information is available for each model and year in the `ev_sales.csv` file:

| Variable   | Description                                          |
|------------|------------------------------------------------------|
| `Vehicle` |  Electric vehicle model |
| `year`| Year of data collection |
| `sales`   | The number of vehicles sold in the US


```python
# Import required libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
```


```python
# Start coding here
# Loading the data
private_ev_charging = pd.read_csv('private_ev_charging.csv')
public_ev_charging = pd.read_csv('public_ev_charging.csv')
ev_sales = pd.read_csv('ev_sales.csv')
```


```python
private_ev_charging.head(10)
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
      <th>year</th>
      <th>private_ports</th>
      <th>private_station_locations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014</td>
      <td>3695</td>
      <td>1825</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>4150</td>
      <td>1962</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016</td>
      <td>5763</td>
      <td>2331</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>6048</td>
      <td>2370</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018</td>
      <td>6812</td>
      <td>2489</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019</td>
      <td>9955</td>
      <td>3078</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2020</td>
      <td>10647</td>
      <td>2768</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2021</td>
      <td>18867</td>
      <td>4074</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2022</td>
      <td>19993</td>
      <td>4435</td>
    </tr>
  </tbody>
</table>
</div>




```python
public_ev_charging.head(10)
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
      <th>year</th>
      <th>public_ports</th>
      <th>public_station_locations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2013</td>
      <td>16619</td>
      <td>6938</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014</td>
      <td>22470</td>
      <td>9207</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015</td>
      <td>26532</td>
      <td>10710</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016</td>
      <td>33165</td>
      <td>13150</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017</td>
      <td>45789</td>
      <td>16170</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2018</td>
      <td>56842</td>
      <td>19893</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2019</td>
      <td>73838</td>
      <td>23282</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2020</td>
      <td>96190</td>
      <td>28602</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2021</td>
      <td>114451</td>
      <td>46407</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2022</td>
      <td>136513</td>
      <td>53764</td>
    </tr>
  </tbody>
</table>
</div>




```python
ev_sales.head()
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
      <th>Vehicle</th>
      <th>year</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chevy Volt</td>
      <td>2011</td>
      <td>7671.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chevy Volt</td>
      <td>2012</td>
      <td>23461.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chevy Volt</td>
      <td>2013</td>
      <td>23094.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chevy Volt</td>
      <td>2014</td>
      <td>18805.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chevy Volt</td>
      <td>2015</td>
      <td>15393.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
private_ev_charging.dtypes
```




    year                         int64
    private_ports                int64
    private_station_locations    int64
    dtype: object




```python
public_ev_charging.dtypes
```




    year                        int64
    public_ports                int64
    public_station_locations    int64
    dtype: object




```python
ev_sales.isna().sum()
```




    Vehicle      0
    year         0
    sales      254
    dtype: int64




```python
ev_sales.value_counts
```




    <bound method DataFrame.value_counts of          Vehicle  year    sales
    0     Chevy Volt  2011   7671.0
    1     Chevy Volt  2012  23461.0
    2     Chevy Volt  2013  23094.0
    3     Chevy Volt  2014  18805.0
    4     Chevy Volt  2015  15393.0
    ..           ...   ...      ...
    490  Kia Niro EV  2015      NaN
    491  Kia Niro EV  2016      NaN
    492  Kia Niro EV  2017      NaN
    493  Kia Niro EV  2018      NaN
    494  Kia Niro EV  2019   1562.0
    
    [495 rows x 3 columns]>




```python
ev_sales_mean = ev_sales.groupby('year')['sales'].mean()
```


```python
ev_sales_mean
```




    year
    2011    4440.750000
    2012    4833.727273
    2013    6068.875000
    2014    5403.727273
    2015    4223.074074
    2016    5320.533333
    2017    4770.268293
    2018    8029.222222
    2019    7258.755556
    Name: sales, dtype: float64




```python
np.std(ev_sales['sales'])
```




    14734.032428474804




```python
np.mean(ev_sales['sales'])
```




    5992.103734439834




```python
# Join the public and private DataFrames
df_comblined = private_ev_charging.merge(public_ev_charging, on='year', how='outer', indicator=True)
```


```python
df_comblined
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
      <th>year</th>
      <th>private_ports</th>
      <th>private_station_locations</th>
      <th>public_ports</th>
      <th>public_station_locations</th>
      <th>_merge</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014</td>
      <td>3695.0</td>
      <td>1825.0</td>
      <td>22470</td>
      <td>9207</td>
      <td>both</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>4150.0</td>
      <td>1962.0</td>
      <td>26532</td>
      <td>10710</td>
      <td>both</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016</td>
      <td>5763.0</td>
      <td>2331.0</td>
      <td>33165</td>
      <td>13150</td>
      <td>both</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>6048.0</td>
      <td>2370.0</td>
      <td>45789</td>
      <td>16170</td>
      <td>both</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018</td>
      <td>6812.0</td>
      <td>2489.0</td>
      <td>56842</td>
      <td>19893</td>
      <td>both</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019</td>
      <td>9955.0</td>
      <td>3078.0</td>
      <td>73838</td>
      <td>23282</td>
      <td>both</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2020</td>
      <td>10647.0</td>
      <td>2768.0</td>
      <td>96190</td>
      <td>28602</td>
      <td>both</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2021</td>
      <td>18867.0</td>
      <td>4074.0</td>
      <td>114451</td>
      <td>46407</td>
      <td>both</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2022</td>
      <td>19993.0</td>
      <td>4435.0</td>
      <td>136513</td>
      <td>53764</td>
      <td>both</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2013</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>16619</td>
      <td>6938</td>
      <td>right_only</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Filter out missing data
df_temp = df_comblined[df_comblined['_merge']=='both']
```


```python
df_temp
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
      <th>year</th>
      <th>private_ports</th>
      <th>private_station_locations</th>
      <th>public_ports</th>
      <th>public_station_locations</th>
      <th>_merge</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014</td>
      <td>3695.0</td>
      <td>1825.0</td>
      <td>22470</td>
      <td>9207</td>
      <td>both</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>4150.0</td>
      <td>1962.0</td>
      <td>26532</td>
      <td>10710</td>
      <td>both</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016</td>
      <td>5763.0</td>
      <td>2331.0</td>
      <td>33165</td>
      <td>13150</td>
      <td>both</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>6048.0</td>
      <td>2370.0</td>
      <td>45789</td>
      <td>16170</td>
      <td>both</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018</td>
      <td>6812.0</td>
      <td>2489.0</td>
      <td>56842</td>
      <td>19893</td>
      <td>both</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019</td>
      <td>9955.0</td>
      <td>3078.0</td>
      <td>73838</td>
      <td>23282</td>
      <td>both</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2020</td>
      <td>10647.0</td>
      <td>2768.0</td>
      <td>96190</td>
      <td>28602</td>
      <td>both</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2021</td>
      <td>18867.0</td>
      <td>4074.0</td>
      <td>114451</td>
      <td>46407</td>
      <td>both</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2022</td>
      <td>19993.0</td>
      <td>4435.0</td>
      <td>136513</td>
      <td>53764</td>
      <td>both</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Remove irrelevant columns
df_temp = df_temp.drop(columns=['_merge'])
```


```python
df_temp
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
      <th>year</th>
      <th>private_ports</th>
      <th>private_station_locations</th>
      <th>public_ports</th>
      <th>public_station_locations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014</td>
      <td>3695.0</td>
      <td>1825.0</td>
      <td>22470</td>
      <td>9207</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>4150.0</td>
      <td>1962.0</td>
      <td>26532</td>
      <td>10710</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016</td>
      <td>5763.0</td>
      <td>2331.0</td>
      <td>33165</td>
      <td>13150</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>6048.0</td>
      <td>2370.0</td>
      <td>45789</td>
      <td>16170</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018</td>
      <td>6812.0</td>
      <td>2489.0</td>
      <td>56842</td>
      <td>19893</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019</td>
      <td>9955.0</td>
      <td>3078.0</td>
      <td>73838</td>
      <td>23282</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2020</td>
      <td>10647.0</td>
      <td>2768.0</td>
      <td>96190</td>
      <td>28602</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2021</td>
      <td>18867.0</td>
      <td>4074.0</td>
      <td>114451</td>
      <td>46407</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2022</td>
      <td>19993.0</td>
      <td>4435.0</td>
      <td>136513</td>
      <td>53764</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Join with aggregated sales DataFrame
# Group by year and add sales
ev_total_sales = ev_sales.groupby('year')['sales'].sum().reset_index()
```


```python
# Inspect the data
ev_total_sales.head(15)
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
      <th>year</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011</td>
      <td>17763.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2012</td>
      <td>53171.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013</td>
      <td>97102.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014</td>
      <td>118882.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>114023.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2016</td>
      <td>159616.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2017</td>
      <td>195581.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2018</td>
      <td>361315.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2019</td>
      <td>326644.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save the variable
ev_sales_2018 =361315
```


```python
# Performing a left join
df_complete = df_temp.merge(ev_total_sales, how='left', on='year')
```


```python
df_complete
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
      <th>year</th>
      <th>private_ports</th>
      <th>private_station_locations</th>
      <th>public_ports</th>
      <th>public_station_locations</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014</td>
      <td>3695.0</td>
      <td>1825.0</td>
      <td>22470</td>
      <td>9207</td>
      <td>118882.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>4150.0</td>
      <td>1962.0</td>
      <td>26532</td>
      <td>10710</td>
      <td>114023.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016</td>
      <td>5763.0</td>
      <td>2331.0</td>
      <td>33165</td>
      <td>13150</td>
      <td>159616.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>6048.0</td>
      <td>2370.0</td>
      <td>45789</td>
      <td>16170</td>
      <td>195581.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018</td>
      <td>6812.0</td>
      <td>2489.0</td>
      <td>56842</td>
      <td>19893</td>
      <td>361315.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019</td>
      <td>9955.0</td>
      <td>3078.0</td>
      <td>73838</td>
      <td>23282</td>
      <td>326644.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2020</td>
      <td>10647.0</td>
      <td>2768.0</td>
      <td>96190</td>
      <td>28602</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2021</td>
      <td>18867.0</td>
      <td>4074.0</td>
      <td>114451</td>
      <td>46407</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2022</td>
      <td>19993.0</td>
      <td>4435.0</td>
      <td>136513</td>
      <td>53764</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_complete.isna().sum()
```




    year                         0
    private_ports                0
    private_station_locations    0
    public_ports                 0
    public_station_locations     0
    sales                        3
    dtype: int64




```python
# Drop any rows with null values
df_complete = df_complete.dropna(subset='sales')
```


```python
df_complete
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
      <th>year</th>
      <th>private_ports</th>
      <th>private_station_locations</th>
      <th>public_ports</th>
      <th>public_station_locations</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014</td>
      <td>3695.0</td>
      <td>1825.0</td>
      <td>22470</td>
      <td>9207</td>
      <td>118882.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>4150.0</td>
      <td>1962.0</td>
      <td>26532</td>
      <td>10710</td>
      <td>114023.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016</td>
      <td>5763.0</td>
      <td>2331.0</td>
      <td>33165</td>
      <td>13150</td>
      <td>159616.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>6048.0</td>
      <td>2370.0</td>
      <td>45789</td>
      <td>16170</td>
      <td>195581.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018</td>
      <td>6812.0</td>
      <td>2489.0</td>
      <td>56842</td>
      <td>19893</td>
      <td>361315.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019</td>
      <td>9955.0</td>
      <td>3078.0</td>
      <td>73838</td>
      <td>23282</td>
      <td>326644.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a graph with multiple lines
# Create a figure and axis object
fig, ax = plt.subplots()

# Plot each line
sns.lineplot(data=df_complete, x='year', y='private_ports', label='Private Port')
sns.lineplot(data=df_complete, x='year', y='public_ports', label='Public Port')
sns.lineplot(data=df_complete, x='year', y='sales', label='Total Sales', linestyle=':')

# Adding titles and labels
ax.set_title('EV Ports and Sales Over Time')
ax.set(xlabel='Year', ylabel='Count')

# Show the legend
ax.legend(loc='upper left')

# Show the plot
plt.show()
```


    
![png](output_29_0.png)
    



```python
trend = 'same'
```

