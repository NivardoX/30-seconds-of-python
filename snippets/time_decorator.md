---
title: time_decorator
tags: utility,intermediate
---

This snippet provides a wrapper function to calculate the time spent in execution.

- Gets the time before calling the function
- Calls the function
- Gets the time after the function returned
- Prints time in a readable way

```py
import datetime
import time
  
def time_decorator(function):
  """Wrapper to calculate time spent in function"""

  def wraps(*args, **kwargs):
    start_time = time.time()
    result = function(*args, **kwargs)
    end_time = time.time()

    time_spent = str(datetime.timedelta(seconds=end_time-start_time))
    print("{} took {} to run.".format(function.__name__,time_spent))
   
    return result

  return wraps
```

```py
@time_decorator
def multiply_list(list):
  result = 1
  for element in list:
    result = result * element
  return result

multiply_list(range(50)) # multiply_list took 0:00:00.000002 to run.
multiply_list(range(10000**2)) # multiply_list took 0:00:02.724385 to run.
```
