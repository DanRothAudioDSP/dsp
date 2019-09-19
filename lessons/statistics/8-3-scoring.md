[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)


```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import random

import thinkstats2

def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L
    
def EstimateGoals(lam=2, iters=1000):

    means = []
    for _ in range(iters):
        L = SimulateGame(lam)
        means.append(L)

    print('rmse L', RMSE(means, lam))
    print('mean error L', MeanError(means, lam))

EstimateGoals()
```
rmse L 1.3917614738165445
mean error L 0.019

This estimator is unbiased as the mean error approaches 0 as iterations are increased.
