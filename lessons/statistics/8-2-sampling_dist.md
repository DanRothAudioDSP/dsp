[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import thinkstats2
import thinkplot

def SimulateExpSample(lam=2, n=10, iters=1000):
    xbars = []
    for j in range(iters):
        xs = np.random.exponential(1.0/lam, n)
        L = 1 / np.mean(xs)
        xbars.append(L)
    return xbars

expbars = SimulateExpSample()

Lcdf = thinkstats2.Cdf(expbars)
thinkplot.Cdf(Lcdf)
thinkplot.Config(xlabel='Sample mean',
                 ylabel='CDF')
```
![Sampling Distribution of Exponential Distribution of L](https://i.ibb.co/KGFyL4T/8-2sampdist.png)
```python
Estimate3(n=10)
```
rmse L 0.8173795666807528
```python
ci = Lcdf.Percentile(5), Lcdf.Percentile(95)
ci
```
(1.20330574054977, 3.592896118833198)
```python
def Estimate3Plot(n=7, iters=1000):
    lam = 2

    means = []
    for _ in range(iters):
        xs = np.random.exponential(1.0/lam, n)
        L = 1 / np.mean(xs)
        means.append(L)
        
    stderr = RMSE(means, lam)
    return stderr

size = range(1,11)
error = []

for samples in size:
    error.append(Estimate3Plot(n=samples))

thinkplot.Plot(size, error)
thinkplot.Config(xlabel='Sample Size',
                 ylabel='Standard Error')
```
![Plot Sampling Error vs n](https://i.ibb.co/kMcZYwq/8-2plot.png)
