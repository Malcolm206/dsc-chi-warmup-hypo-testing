## Imports


```python
#data manip
import pandas as pd
import numpy as np

#data calc
from scipy import stats

#used for tests
from test_background import pkl_dump, run_test_dict, run_test
from test_background import load_test_dict as load
```

#### Read in `data.csv` from `data` and print a random sample of five rows.  (Looking at a random sample of five rows instead of `df.head()` avoids the problem of getting an impression of a dataset that is sorted in some way)

#### Does this dataset look familiar?  


```python
#your code here
```

#### For purposes of this problem, let's say we know this dataset represents the entirety of city employees from Seattle

## The Problem

### Is the `hourly_rate` of people whose last name begins with 'B' significantly different than the `hourly_rate` of the Seattle employees as a whole?

#### Let's mimic a data analysis scenario where we have aggregated info about:

- the mean of `hourly_rate` for all Seattle employees

- the std of `hourly_rate` for same

but we have to sample to find more-granular data about people whose last name begins with 'B'

---

### Hypothesis Generation

What are the null and alternative hypotheses?  (Jake, we will single you out at standup and ask what your hypotheses are)


```python
#your answer here
```

### Confidence Level Selection

#### Provide the following answers about the next steps of our analysis

- What is our test statistic?  (IOW: we are going to make a calculation and see how "extreme" that calculation is.  What specific calculation are we going to make?)  

- Why are we using *this* statistic as opposed to a different one?

- Are we running an upper, lower, or two-sided test?  Why? 


```python
# your code here
```

#### We'll use an alpha of .05 as the cutoff for significance

#### Using that value of alpha, what is the value of the critical test statistic(s) we will compare our calculated test statistic against?


```python
# your code here
```

#### Make the following calculations

- Store a random sample of 100 employees whose last name starts with 'B' in the variable `b_last_sample`
    - use `random_state=33` so that we all get the same 100 random employees


- Store that sample's mean of `hourly_rate` as `b_last_sample_mean`


- Store the sample size as `sample_size`
    - use a calculation, don't hard code it

- Store the population mean of `hourly_rate` as `pop_mean`

- Store the population std of `hourly_rate` as `pop_std`


```python
#you might create other variables than this, but these
#are provided for your convenience 

b_last_sample = #your code here

b_last_sample_mean = #your code here

sample_size = #your code here

pop_mean = #your code here 

pop_std = #your code here
```

### Test statistic calculation

- Calculate the specific test statistic you determined was appropriate above

- Store it as `test_stat`


```python
#your code here
```

## The MOMENT OF TRUTH

#### Do we have evidence indicating we should reject the null hypothesis at alpha=.05?  Why or why not?

#### Your final sentence should write out your full conclusion w/o referencing "null hypothesis"


```python
'''# your answer here'''
```


```python

```
