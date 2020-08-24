# Miscellaneous

#### Timer

```python
import time
get_time = time.perf_counter
t0 = get_time()
### some code ###
t1 = get_time()
print('Time elapsed = {}'.format(t1 - t0))
```

#### Path names
```python
import os
pathname = os.path.join('dir1', 'dir2', 'filename')
# MacOS/Linux: dir1/dir2/filename
# Windows: dir1\dir2\filename
```

#### Executing in terminal
To run ```script.py``` you can use the following terminal command:
```bash
python script.py
```
However, if you want to run it as an executable file without calling the ```python``` command, just add the following text to the head of ```script.py```:
```python
#!/usr/bin/env python
# coding: utf-8
```
Then you can run the script using
```bash
./script.py
```

#### Packages
Useful resources:
- https://packaging.python.org/tutorials/packaging-projects/
- https://kiwidamien.github.io/making-a-python-package.html
- https://medium.com/@joel.barmettler/how-to-upload-your-python-package-to-pypi-65edc5fe9c56

Load package from inside directory:
```bash
python -m pip install .
```

Reload package (e.g., if made edits):
```bash
python -m pip install --upgrade --force-reinstall ..
```

#### Save/load data (json)
Note that this does not work for np.ndarrays - for those see NumPy section.
```python
import json
data = {'a' : [1, 2, 3], 'b' : ('hello', 'world')} # dictionary

# save
with open('data.json', 'w') as outfile:
  json.dump(data, outfile)
  
# load
with open('data.json', 'r') as infile:
  data = json.load(infile)
```
