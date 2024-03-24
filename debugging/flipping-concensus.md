# Flipping concensus
## Background
Thank goodness for modern personal computers which can save us from the overwhelming task of number crunching. Consider *n* people, all flipping their own fair coins *m* times.  The probability could be manageably represented analytically, but still requires numerical evaluation.

## Analysis
Very generally, the probability that *m* coin flips have the same outcome *k* times repeated by *n* people is

$$ \left[ \binom mk \left( \frac 12 \right )^m\right]^n.$$

The question we would like to answer is about when *k* = *m*, or every coin flip has an identical outcome:

$$P(n,m)=\frac 1{2^{nm}}\sum_{k=0}^{m}\binom mk^n$$

## Purported solution
```python
from math import factorial

def binomial(n, k):
    return factorial(n) // factorial(k) // factorial(n - k)

def flipping_concensus(n_people, m_flips_per_person):
    return sum(pow(binomial(m_flips_per_person, i), n_people) 
               for i in range(m_flips_per_person))
```

## Expectations
For some reason, the result of `flipping_concensus` is never in [0, 1]. Why not? Is the prompt internally consistent be erroneous, or does the Python solution alone have an issue? 
