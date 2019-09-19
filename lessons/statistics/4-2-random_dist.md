[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import thinkstats2
import thinkplot

numbers = np.random.random(1000)
pmf = thinkstats2.Pmf(numbers, 'random numbers')
thinkplot.Pmf(pmf)
thinkplot.Config(xlabel='Random Numbers', ylabel='PMF')
```
![PMF Plot](https://i.ibb.co/MGKrw2f/4-2pmf.png)

The probabilities for the 1000 random numbers are uniform and just create a pure noise PMF that is hard to draw conclusions from.

```python
cdf = thinkstats2.Cdf(numbers)
thinkplot.Cdf(cdf)
thinkplot.config(xlabel='Random Numbers', ylabel='CDF')
```

![CDF Plot](https://i.ibb.co/dg1c156/4-2cdf.png)

The CDF is more clear and shows that there is a uniform distribution of numbers between 0 and 1 as the percentiles match the percentile ranks.  This proves the CDF to be a better visualization for the large number of samples.
