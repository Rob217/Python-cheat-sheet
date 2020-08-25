# Pandas

```python 
import pandas as pd
```

#### Load/save a dataframe from csv
```python
df = pd.read_csv('data.csv')
df.to_csv('data.csv')
```

#### Iterate through rows
```python
>>> df = pd.DataFrame(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['a', 'b', 'c'])
   a  b  c
0  1  2  3
1  4  5  6
2  7  8  9
>>> for i, j in df.iterrows():
>>>   print(j['a']) 
1
4
7
>>> for i, a, b, c in df.itertuples():
>>>   print(a)
1
4
7
```

#### Add new column to dataframe
```python
df['new_col'] = '' # empty column
df['new_col'] = val # fill with some value
df['new_col'] = [1, 2, 3] # fill with list
df.insert(loc, col_name, vals, allow_duplicates) # add a new column in location loc with name col_name and values vals
```
`allow_duplicates` is a boolean which allows `col_name` to be the same as an already existing column name or not.

#### Size of dataframe
```python
df.shape # (2, 3)
len(df.index) # number of rows
```
