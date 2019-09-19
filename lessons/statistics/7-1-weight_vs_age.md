[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import thinkstats2
import thinkplot
import first

live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])

birthwgt = live.totalwgt_lb
pregage = live.agepreg

thinkplot.Scatter(pregage, birthwgt, alpha=0.5)
thinkplot.Config(xlabel='Mother\'s Age',
                 ylabel='Birth Weight (lb)',
                 legend=False)
```

![Scatter Plot](https://i.ibb.co/jzdBhQJ/7-1scatter.png)

```python
bins = np.arange(0, 200, 5)
indices = np.digitize(pregage, bins)
groups = live.groupby(indices)
mean_ages = [group.agepreg.mean() for i, group in groups]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups]

for percent in [75, 50, 25]:
    weight_percentiles = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(mean_ages, weight_percentiles, label=label)
    
thinkplot.Config(xlabel='Mother\'s Age',
                 ylabel='Birth Weight (lb)',
                 axis=[10, 45, 0, 16],
                 legend=True)
```

![Percentile Plot](https://i.ibb.co/4KGkVWd/7-1perc.png)

```python
Corr(birthwgt, pregage), SpearmanCorr(birthwgt, pregage)
```
(0.06883397035410908, 0.09461004109658228)

The correlation is not very strong between these two variables but there is a slightly stronger correlation reported by Spearman's correlation coefficient which may indicate a more nonlinear relationship between a mother's age and the weight of a child at birth.  A scatter plot is more informational in this context and relays that mothers that are older may have a tighter grouping for potential weights for children at birth.
