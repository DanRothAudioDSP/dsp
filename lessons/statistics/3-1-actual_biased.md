[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import nsfg
import first
import thinkstats2

resp = nsfg.ReadFemResp()

numkids_pmf = thinkstats2.Pmf(resp.numkdhh, label='actual')
numkids_pmf_biased = BiasPmf(numkids_pmf, label='observed')
thinkplot.PrePlot(2)
thinkplot.Pmfs([numkids_pmf, numkids_pmf_biased])
thinkplot.Config(xlabel='Number of Kids', ylabel='PMF')

print('Actual mean', numkids_pmf.Mean())
print('Observed mean', numkids_pmf_biased.Mean())
```

![Response Plot](https://i.ibb.co/4dTGZRJ/ex3-1.png)

Actual mean 1.024205155043831

Observed mean 2.403679100664282
