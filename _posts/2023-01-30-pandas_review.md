---
layout: single
title:  "Pandas Review"
categories: pandas
tag: [python]
---

## Pandas Review 

#### Pandas is an open source library built on top of the Numpy library


```python
import numpy as np
import pandas as pd 

labels = ["Naver", "Kakao", "Toss"]
my_data = [10, 20 ,30]
arr = np.array(my_data)
comp_dict = {"Naver":10, "Kakao":20, "Toss":30}
```

#### Series


```python
pd.Series(my_data)
```




    0    10
    1    20
    2    30
    dtype: int64




```python
pd.Series(my_data, labels)
```




    Naver    10
    Kakao    20
    Toss     30
    dtype: int64




```python
pd.Series(arr,labels)
```




    Naver    10
    Kakao    20
    Toss     30
    dtype: int32




```python
pd.Series(comp_dict)
```




    Naver    10
    Kakao    20
    Toss     30
    dtype: int64



#### Series can hold any kind of data type including functions


```python
pd.Series(data = [sum, print, len])
```




    0      <built-in function sum>
    1    <built-in function print>
    2      <built-in function len>
    dtype: object



#### Series Indexing


```python
comp_series = pd.Series(["naver", "kakao", "google", "samsung"], [0, 1, 2, 3])
comp_series
```




    0      naver
    1      kakao
    2     google
    3    samsung
    dtype: object




```python
comp_series[2]
```




    'google'



* Pandas and Numpy will convert all integers to float to retain information 


```python
from numpy.random import * 
seed(101) #Make sure I get the same set of numbers 
```


```python
df = pd.DataFrame(randn(5,4), ['A', 'B', 'C', 'D', 'E'], ['Rock', 'Blues', 'Jazz', 'Hiphop'])
df
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
      <th>Rock</th>
      <th>Blues</th>
      <th>Jazz</th>
      <th>Hiphop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>-0.544439</td>
      <td>-0.668172</td>
      <td>0.007315</td>
      <td>-0.612939</td>
    </tr>
    <tr>
      <th>B</th>
      <td>1.299748</td>
      <td>-1.733096</td>
      <td>-0.983310</td>
      <td>0.357508</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-1.613579</td>
      <td>1.470714</td>
      <td>-1.188018</td>
      <td>-0.549746</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-0.940046</td>
      <td>-0.827932</td>
      <td>0.108863</td>
      <td>0.507810</td>
    </tr>
    <tr>
      <th>E</th>
      <td>-0.862227</td>
      <td>1.249470</td>
      <td>-0.079611</td>
      <td>-0.889731</td>
    </tr>
  </tbody>
</table>
</div>



#### Creating a new column


```python
df["new"] = df["Jazz"] + df["Hiphop"] 
df
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
      <th>Rock</th>
      <th>Blues</th>
      <th>Jazz</th>
      <th>Hiphop</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>-0.544439</td>
      <td>-0.668172</td>
      <td>0.007315</td>
      <td>-0.612939</td>
      <td>-0.605624</td>
    </tr>
    <tr>
      <th>B</th>
      <td>1.299748</td>
      <td>-1.733096</td>
      <td>-0.983310</td>
      <td>0.357508</td>
      <td>-0.625802</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-1.613579</td>
      <td>1.470714</td>
      <td>-1.188018</td>
      <td>-0.549746</td>
      <td>-1.737764</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-0.940046</td>
      <td>-0.827932</td>
      <td>0.108863</td>
      <td>0.507810</td>
      <td>0.616673</td>
    </tr>
    <tr>
      <th>E</th>
      <td>-0.862227</td>
      <td>1.249470</td>
      <td>-0.079611</td>
      <td>-0.889731</td>
      <td>-0.969343</td>
    </tr>
  </tbody>
</table>
</div>



#### axis = 0 for row & axis = 1 for column 
#### inplace = True to make permanent deletion 


```python
df.drop("new", axis=1, inplace=True)
df.shape
```




    (5, 4)



#### Calling by Row


```python
df.loc["A"]
```




    Rock      1.618982
    Blues     1.541605
    Jazz     -0.251879
    Hiphop   -0.842436
    Name: A, dtype: float64




```python
df.iloc[0]
```




    Rock      1.618982
    Blues     1.541605
    Jazz     -0.251879
    Hiphop   -0.842436
    Name: A, dtype: float64




```python
df.loc["A","Jazz"]
```




    -0.251879139213213




```python
df.loc[["A","B"], ["Jazz", "Rock"]]
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
      <th>Jazz</th>
      <th>Rock</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>-0.251879</td>
      <td>1.618982</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.731000</td>
      <td>0.184519</td>
    </tr>
  </tbody>
</table>
</div>



#### Conditional Selection


```python
df[df<1]
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
      <th>Rock</th>
      <th>Blues</th>
      <th>Jazz</th>
      <th>Hiphop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.251879</td>
      <td>-0.842436</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.184519</td>
      <td>0.937082</td>
      <td>0.731000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-0.326238</td>
      <td>0.055676</td>
      <td>0.222400</td>
      <td>-1.443217</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-0.756352</td>
      <td>0.816454</td>
      <td>0.750445</td>
      <td>-0.455947</td>
    </tr>
    <tr>
      <th>E</th>
      <td>NaN</td>
      <td>-1.690617</td>
      <td>-1.356399</td>
      <td>-1.232435</td>
    </tr>
  </tbody>
</table>
</div>



#### When passing multiple columns, use a list!


```python
df[df["Rock"]<1][["Blues", "Jazz"]]
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
      <th>Blues</th>
      <th>Jazz</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>B</th>
      <td>0.937082</td>
      <td>0.731000</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.055676</td>
      <td>0.222400</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.816454</td>
      <td>0.750445</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[(df["Rock"]<1) & (df["Jazz"]>0.5)]
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
      <th>Rock</th>
      <th>Blues</th>
      <th>Jazz</th>
      <th>Hiphop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>B</th>
      <td>0.184519</td>
      <td>0.937082</td>
      <td>0.731000</td>
      <td>1.361556</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-0.756352</td>
      <td>0.816454</td>
      <td>0.750445</td>
      <td>-0.455947</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[(df["Rock"]<1) | (df["Jazz"]>0.5)]
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
      <th>Rock</th>
      <th>Blues</th>
      <th>Jazz</th>
      <th>Hiphop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>B</th>
      <td>0.184519</td>
      <td>0.937082</td>
      <td>0.731000</td>
      <td>1.361556</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-0.326238</td>
      <td>0.055676</td>
      <td>0.222400</td>
      <td>-1.443217</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-0.756352</td>
      <td>0.816454</td>
      <td>0.750445</td>
      <td>-0.455947</td>
    </tr>
  </tbody>
</table>
</div>



#### df.reset_index() makes the current index a column<br/>Remember why df.reset_index() is important!


```python
df.reset_index()
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
      <th>index</th>
      <th>Rock</th>
      <th>Blues</th>
      <th>Jazz</th>
      <th>Hiphop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>-0.544439</td>
      <td>-0.668172</td>
      <td>0.007315</td>
      <td>-0.612939</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>1.299748</td>
      <td>-1.733096</td>
      <td>-0.983310</td>
      <td>0.357508</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>-1.613579</td>
      <td>1.470714</td>
      <td>-1.188018</td>
      <td>-0.549746</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>-0.940046</td>
      <td>-0.827932</td>
      <td>0.108863</td>
      <td>0.507810</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E</td>
      <td>-0.862227</td>
      <td>1.249470</td>
      <td>-0.079611</td>
      <td>-0.889731</td>
    </tr>
  </tbody>
</table>
</div>



#### If I want a column to be the index I use df.set_index() 


```python
new_ind = "Seoul Incheon Sejong Daejeon Daegu".split()
df["Cities"] = new_ind
df.set_index("Cities")
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
      <th>Rock</th>
      <th>Blues</th>
      <th>Jazz</th>
      <th>Hiphop</th>
    </tr>
    <tr>
      <th>Cities</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Seoul</th>
      <td>-0.544439</td>
      <td>-0.668172</td>
      <td>0.007315</td>
      <td>-0.612939</td>
    </tr>
    <tr>
      <th>Incheon</th>
      <td>1.299748</td>
      <td>-1.733096</td>
      <td>-0.983310</td>
      <td>0.357508</td>
    </tr>
    <tr>
      <th>Sejong</th>
      <td>-1.613579</td>
      <td>1.470714</td>
      <td>-1.188018</td>
      <td>-0.549746</td>
    </tr>
    <tr>
      <th>Daejeon</th>
      <td>-0.940046</td>
      <td>-0.827932</td>
      <td>0.108863</td>
      <td>0.507810</td>
    </tr>
    <tr>
      <th>Daegu</th>
      <td>-0.862227</td>
      <td>1.249470</td>
      <td>-0.079611</td>
      <td>-0.889731</td>
    </tr>
  </tbody>
</table>
</div>



#### Multi-index Dataframe Hierarchy 
