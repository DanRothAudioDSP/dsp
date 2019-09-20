[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import random

import thinkstats2
import thinkplot

import first

live, firsts, others = first.MakeFrames()

class DiffMeansPermute(thinkstats2.HypothesisTest):

    def TestStatistic(self, data):
        group1, group2 = data
        test_stat = abs(group1.mean() - group2.mean())
        return test_stat

    def MakeModel(self):
        group1, group2 = self.data
        self.n, self.m = len(group1), len(group2)
        self.pool = np.hstack((group1, group2))

    def RunModel(self):
        np.random.shuffle(self.pool)
        data = self.pool[:self.n], self.pool[self.n:]
        return data
        
class DiffMeansResample(DiffMeansPermute):
    
    def RunModel(self):
        group1 = np.random.choice(self.pool, self.n, replace=True)
        group2 = np.random.choice(self.pool, self.m, replace=True)
        return group1, group2
        
lngdata = firsts.prglngth.values, others.prglngth.values
lnght_perm = DiffMeansPermute(lngdata)
lngperm_pvalue = lnght_perm.PValue()
lngperm_pvalue
```
0.166
```python
lnght_res = DiffMeansResample(lngdata)
lngres_pvalue = lnght_res.PValue()
lngres_pvalue
```
0.174
```python
wgtdata = firsts.totalwgt_lb.values, others.totalwgt_lb.values
wgtht_perm = DiffMeansPermute(wgtdata)
wgtperm_pvalue = wgtht_perm.PValue()
wgtperm_pvalue
```
0.0
```python
wgtht_res = DiffMeansResample(wgtdata)
wgtres_pvalue = wgtht_perm.PValue()
wgtres_pvalue
```
0.0

These results indicate that the altered model does little to change the results of the tests.

