# Python Cheat Sheet

This post is a collection of Python commands and recipes that I have found useful. This is an open post and I will keep updating it with new items.

## Misc Python

#### Timer

```python
import time
get_time = time.perf_counter
t0 = get_time()
### some code ###
t1 = get_time()
print('Time elapsed = {}'.format(t1 - t0))
```
