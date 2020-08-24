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
