# Dart Pie
## Background
### **Problem statement**
Attributed to Comte de Buffon (1707 – 1788), the Buffon needle tossing experiment is a way of estimating π through a series of trials. The experiment begins with a sheet of paper and parallel lines drawn across it. The lines are *d* units apart. There are also *n* short needles of length *l*, which is less than *d*. Each trial consists of tossing a needle onto the paper and noting if it crosses through a line.<sup>1</sup> It is known that the probability of intersection approaches
$$P(T)=\frac{2l}{πd}\ .$$
This can be rearranged in terms of π, using an approximation of P,
$$π=4\left(1-\frac 1 3 + \frac 1 5 - \frac 1 7 + \frac 1 9 - \mathellipsis \right)$$

so a Python program has been written to estimate π by enscribing a circle within a square and counting the number of darts that hit the inner circle. That way we avoid generating a random needle angle which would paradoxically require knowing π. The other constraint is that the presumed dart thrower must not be experienced enough to skew the probability towards the center. Programmatically, this is done by generating uniform random coordinates. 

Below is a module that demonstrates the estimation of π by showing how the precision `margin_error` increases roughly with the number of trials `t`.
```python
from datetime import datetime
from random import seed, uniform
from math import floor, log10, inf, pi

def piedarts(t):
    seed(datetime.now().timestamp())
    darts = 0
    for _ in range(int(t)):
        x = random.uniform(0, 1)
        y = random.uniform(0, 1)
        r = x*x + y*y
        if r < 1:
            darts += 1
    pi = 4*darts/t
    return pi

if __name__ == '__main__':
    def dec_place(dec):
        return inf if dec == 0 else -floor(log10(abs(dec))) - 1
    t = 1_000_000
    pi_ish = piedarts(t)
    margin_error = 0.005
    print(pi_ish, margin_error)
    abs_error = abs(pi_ish - math.pi)
    assert(abs_error <= margin_error)
    print(f'Estimate after {t} trials is '
          f'correct up to {dec_place(abs_error)} decimal places.')
```

A few things, however, need further explanation.

### Expected outcome
For one thing, how does precision scale, if at all, with the number of trials? The  `math.pi` const is accurate to 15 decimal places. How many trials, roughly, would it take to achieve this accuracy with our program?

The formula used in the `piedarts` function uses only a quarter of the original circle. How is this so? Explain how we are able to take a quarter of the circle-inside-a-square (where the ratio of exposed square to the circle area is the same for every quarter).

---

<font size=1><sup>1</sup> Buffon's needle problem, https://en.wikipedia.org/w/index.php?title=Buffon%27s_needle_problem&oldid=1212227562 (last visited Mar. 14, 2024).



