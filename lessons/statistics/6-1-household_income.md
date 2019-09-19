[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import thinkstats2
import thinkplot

import hinc
income_df = hinc.ReadData()

log_sample = InterpolateSample(income_df, log_upper=6.0)
sample = np.power(10, log_sample)
sample_mu = Mean(sample)

Median(sample), sample_mu, Skewness(sample), PearsonMedianSkewness(sample)
```
(51226.45447894046, 74278.70753118739, 4.949920244429579, 0.7361258019141795)
```python
sample_cdf = thinkstats2.Cdf(sample)
sample_cdf.PercentileRank(sample_mu)
```
66.0005879566872

This indicates that 66% of people report incomes lower than the mean, which makes sense in the context of the positive skew reported by the skewness calculations.  

Now we increase the upper bound to 10 million:
```python
log_sample7 = InterpolateSample(income_df, log_upper=7.0)
sample7 = np.power(10, log_sample7)
Median(sample7), Mean(sample7), Skewness(sample7), PearsonMedianSkewness(sample7)
```
(51226.45447894046, 124267.39722164693, 11.603690267537795, 0.39156450927742104)

When the upper bound is increased to 10 million the skew becomes less positive, which makes sense as the mean shifts but the median remains the same.  The non-Pearson skewness is much more heavily affected by large outliers and reports a much more dramatic shift in skewness, but the Pearson skewness makes more sense as the upper income ranges will seem more sparse in comparison.
