[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import thinkstats2
import thinkplot
import scipy.stats
import brfss

df = brfss.ReadBrfss()

male_heights = df.loc[df.sex==1.0].htm3.dropna()
male_mu = male_heights.mean()
male_sigma = male_heights.std()
male_dist = scipy.stats.norm(loc=mu, scale=sigma)

male_dist.cdf(male_mu+male_sigma) - male_dist.cdf(male_mu)
```

0.34071883767465827

To qualify for the Blue Man Group you must be one standard deviation above the mean (5'10").  The above code computes the percentage of the population in this range by subtracting the CDF of the mean (50%) from the CDF of entries one standard deviation above the mean (84%) and results in approximately 34% of the population.
