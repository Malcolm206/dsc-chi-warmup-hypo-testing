# Z-test warmup!

do you have what it takes

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


```python
#__SOLUTION__

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


```python
#__SOLUTION__

df = pd.read_csv('data/data.csv')

df.sample(5, axis=0)
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
      <th>department</th>
      <th>last_name</th>
      <th>first_name</th>
      <th>job_title</th>
      <th>hourly_rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>3762</td>
      <td>3762</td>
      <td>Seattle City Light</td>
      <td>Gansz</td>
      <td>Bambi</td>
      <td>Mat Handling Supv,General-BU</td>
      <td>42.000</td>
    </tr>
    <tr>
      <td>6857</td>
      <td>6857</td>
      <td>Seattle Public Utilities</td>
      <td>Mantchev</td>
      <td>Eugene</td>
      <td>StratAdvsr2,Engrng&amp;Plans Rev</td>
      <td>62.670</td>
    </tr>
    <tr>
      <td>9553</td>
      <td>9553</td>
      <td>Human Services Department</td>
      <td>Santor</td>
      <td>Samantha</td>
      <td>Manager2,Human Svcs</td>
      <td>54.583</td>
    </tr>
    <tr>
      <td>8801</td>
      <td>8801</td>
      <td>Seattle Center</td>
      <td>Price</td>
      <td>Qiao-Ai</td>
      <td>Janitor-SC/Parks/SPU</td>
      <td>23.280</td>
    </tr>
    <tr>
      <td>1430</td>
      <td>1430</td>
      <td>Seattle Dept of Transportation</td>
      <td>Buchholz</td>
      <td>Bow</td>
      <td>Bridge Maint Mechanic</td>
      <td>40.100</td>
    </tr>
  </tbody>
</table>
</div>



![](viz/seattle.gif)

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


```python
#__SOLUTION__

print('''
Null hypothesis: 

there is no difference in the means of `hourly_rate`
for Seattle employees as a whole and Seattle employees whose last 
names start with 'B'

Alternative hypothesis: 

there is a difference in the means of 
`hourly_rate` for Seattle employees as a whole and Seattle employees 
whose last names start with 'B'
''')
```

    
    Null hypothesis: 
    
    there is no difference in the means of `hourly_rate`
    for Seattle employees as a whole and Seattle employees who's last 
    names start with 'B'
    
    Alternative hypothesis: 
    
    there is a difference in the means of 
    `hourly_rate` for Seattle employees as a whole and Seattle employees 
    who's last names start with 'B'
    


### Confidence Level Selection

#### Provide the following answers about the next steps of our analysis

- What is our test statistic?  (IOW: we are going to make a calculation and see how "extreme" that calculation is.  What specific calculation are we going to make?)  

- Why are we using *this* statistic as opposed to a different one?

- Are we running an upper, lower, or two-sided test?  Why? 


```python
# your code here
```


```python
#__SOLUTION__

print('''
Since we know:

- the population standard deviation

- the size of our sample is greater than 30

- we are comparing the sample mean to the population mean

we are going to run a one-sample z-test.

(If we didn't know either parameter or our sample size was <30,  
we would use a t-test)

Since we want to know:

- if the sample mean is *different* from the population mean

we are running a two-tailed test.

(How would this be different if we just wanted to know if the
sample mean was higher than the population mean?  Lower?)

''')
```

    
    Since we know:
    
    - the population standard deviation
    
    - the size of our sample is greater than 30
    
    - we are comparing the sample mean to the population mean
    
    we are going to run a one-sample z-test.
    
    (If we didn't know either parameter or our sample size was <30,  
    we would use a t-test)
    
    Since we want to know:
    
    - if the sample mean is *different* from the population mean
    
    we are running a two-tailed test.
    
    (How would this be different if we just wanted to know if the
    sample mean was higher than the population mean?  Lower?)
    
    


#### We'll use an alpha of .05 as the cutoff for significance

#### Using that value of alpha, what is the value of the critical test statistic(s) we will compare our calculated test statistic against?


```python
# your code here
```


```python
#__SOLUTION__

alpha = .05

'''stats.norm.ppf is inverse of cdf for a normal curve
in other words, it will return what the specific point values are
for a given distance on the x-axis 
(eg, at a given significance level, it will return the critical 
test statistic)'''

stats.norm.ppf(alpha/2), stats.norm.ppf(1-alpha/2)

#Why do we have two critical test statistics instead of 1?

#Why use alpha/2 and 1-alpha/2 here?
```




    (-1.9599639845400545, 1.959963984540054)



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


```python
#__SOLUTION__

b_filter = [True 
            if val[0]=='B' 
            else False 
            for val 
            in df['last_name']
           ]

b_last_sample = (
    df[b_filter]
    .sample(
        100,
        axis=0,
        random_state=33
    )
)

b_last_sample_mean = b_last_sample['hourly_rate'].mean()

pop_mean = df['hourly_rate'].mean()

pop_std = df['hourly_rate'].std()

sample_size = len(b_last_sample)

# #used for tests
# pkl_dump([
#     (b_last_sample, 'b_last_sample'),
#     (b_last_sample_mean, 'b_last_sample_mean'),
#     (pop_mean, 'pop_mean'),
#     (pop_std, 'pop_std'),
#     (sample_size, 'sample_size')
# ])
```


```python
#run this cell to check b_last_sample
run_test(b_last_sample, 'b_last_sample')
```


```python
#run this cell to check b_last_sample_mean
run_test(b_last_sample_mean, 'b_last_sample_mean')
```


```python
#run this cell to check pop_mean
run_test(pop_mean, 'pop_mean')
```


```python
#run this cell to check pop_std
run_test(pop_std, 'pop_std')
```


```python
#run this cell to check sample_size
run_test(sample_size, 'sample_size')
```

### Test statistic calculation

- Calculate the specific test statistic you determined was appropriate above

- Store it as `test_stat`


```python
#your code here
```


```python
#__SOLUTION__

test_stat = (
    (b_last_sample_mean - pop_mean)
    /
    (pop_std/np.sqrt(sample_size))
)

# #used for tests
# pkl_dump([
#     (test_stat, 'test_stat'),
# ])

test_stat
```




    0.46568880436878846




```python
#run this cell to check test_stat
run_test(test_stat, 'test_stat')
```

## The MOMENT OF TRUTH

#### Do we have evidence indicating we should reject the null hypothesis at alpha=.05?  Why or why not?

#### Your final sentence should write out your full conclusion w/o referencing "null hypothesis"


```python
'''# your answer here'''
```


```python
#__SOLUTION__

print('''
Because the value of our test statistic is both:

- larger than the min critical test stat we calculated
- smaller than the max critical test stat we calculated

at an alpha level of .05, it does not lie in the range which
we determined we would accept as sufficiently unlikely and providing 
evidence that we're seeing data that isn't attributable to chance

Therefore, we did not find evidence that we can reject the comparison
of people whose last names begin with B having no significantly 
different mean "hourly_rate" than the population mean of "hourly_rate"
''')
```

    
    Because the value of our test statistic is both:
    
    - larger than the min critical test stat we calculated
    - smaller than the max critical test stat we calculated
    
    at an alpha level of .05, it does not lie in the range which
    we determined we would accept as sufficiently unlikely and providing 
    evidence that we're seeing data that isn't attributable to chance
    
    Therefore, we did not find evidence that we can reject the comparison
    of people whose last names begin with B having no significantly 
    different mean "hourly_rate" than the population mean of "hourly_rate"
    



```python

```
