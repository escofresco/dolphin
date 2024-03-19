# Honestly, yes
## Background
A university researcher is investigating embarrassing at-home activities. One way of surveying students is to ask that classrooms anonymously fill out a form consisting of a single yes-or-no question, *q*. In this scenario, students are likely to answer honestly. After all, there's no way of knowing who answered what. 

Perhaps, however, the researcher doesn't have the luxury of surveying students en masse. Instead, they must do so on an ad hoc basis, say, by asking a student to visit their office. The true anonymity would be lost, in this case. So what can we do?

## Approach
When the student arrives, ask them to go into a private room where there is a fair coin. They should then flip the coin and if it turns up heads, they would answer yes or no to *q*. Otherwise, they should flip the coin again and write yes if it shows heads and no if it shows tails. When the student hands the form back, there will be a single yes or no answer.<sup>1</sup> 

When the researcher is done with their study, there are a total of *Y* yes responses and *N* no responses. *Y<sub>q</sub>* therefore denotes the number of yes responses to *q*, *Y<sub>non-q</sub>* denotes yes responses to the question where the first coin flip turned up tails but the subsequent flip was heads, and so forth.

We know the following initially:

$$m = Y + N\\\P(coin) = \frac 1 2\\\ Y_{q} + N_{q} = \frac 1 2 m$$

In other words, half the responses will be for *q*, half for *non-q*. Therefore, a quarter of the answers to *non-q* will be yes and a quarter will be no. From that, we can infer the number of yes responses to *q*:

$$Y_{q} = Y - \frac 1 4 m$$

So, the ratio of *Y<sub>q</sub>* answers to total *q* answers is

$$\frac {Y_q} {\frac 1 2 m} = \frac {Y - \frac 1 4 m} {\frac 1 2 m} = \boxed{ \frac {2Y} {m} - \frac 1 2 }$$

## Analytical Result
For *m* = 100,000, *Y* = 70312, *N* = 29688,

$$\frac {70312 - \frac 1 4 100,000} {\frac 1 2 100,000} \approx 90.6\\%$$

or about 90,000 admitted to doing the embarrassing act. (*m* was sufficiently large and, with our approach, respondents would have no reason to lie.)

## Empirical Result
We would like to run a simulation that verifies our analytical result, so agent-based modeling is used. The agent will have a 90.6% chance of answering yes to *q* (we run *m* Bernoulli trials with *P*(success) = 0.96). In other words, we survey 100,000 agents and ask them to reply based on the rules already discussed.

```python
from enum import Enum
from math import isclose
from random import randrange, seed
from sys import version_info
from time import monotonic

seed(monotonic())

if version_info[:2] == (3,12):
    from random import binomialvariate
else:
    from random import random
    def binomialvariate(n, p):
        return sum(random() < p for i in range(n))

class Coin(Enum):
    HEADS = 0
    TAILS = 1

class Answer(Enum):
    NO = 0
    YES = 1
    
def agent_model(m, p_yes_q, yesses_expected):
    def flip_coin():
        return Coin(randrange(2) == 0)
    def answer_q():
        return Answer(binomialvariate(1, p_yes_q))
    yesses_actual = 0
    for _ in range(m):
        if flip_coin() == Coin.HEADS:
            if answer_q() is Answer.YES:
                yesses_actual += 1
        elif flip_coin() is Coin.HEADS:
            yesses_actual += 1
    print(yesses_actual)
    return isclose(yesses_actual, yesses_expected, rel_tol=0.01)

print(agent_model(100_000, .906, 70312))
```

## Expectations
* Tabulate the Python solution into three columns:
 1. The first column should correspond to a semantically meaningful block of code.
 2. The second column should to be a row-wise explanation.
 3. The third column should be the analytical representation of the row-wise code block.
* To what extent is the empirical solution an agent-based model?
* 


---

<font size=1>

<sup>1</sup>Stanley L. Warner, "Randomized Response: A Survey Technique for Eliminating Evasive Answer Bias," *Journal of the American Statistical Association*, vol. 60, March 1965, pp. 63–69.

</font>
