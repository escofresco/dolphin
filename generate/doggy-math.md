# Doggy Math
## Background
#### **Problem statement**
Your dog has a litter of four, what is the likelihood of two males and two females?<sup>*</sup> 

#### **Arithmetic solution**
This is a Bernoulli sequence of four trials, therefore the number of possible outcomes is
$$n = 2^t = 2^4 = 16$$

If your dog has just three puppies, the probability, *p*, of *k* males and *1-k* females is found by applying the binomial theorem:

$$\underbrace{\dbinom{n}{k}}_{\frac{n!}{k!(n-k)!}}  p^k(1-p)^{n-k}$$

so when the chance of each puppy being male or female is equal, the chance of there being 1 male and 2 females out of three pups is summarized,
$$\text{1 male}\land\text{2 females}\\\ \Downarrow\\\ P(k=1)=\underbrace{\dbinom{3}{1}}_{\frac{3!}{1!(2)!}=\frac 6 2=3} \left({\frac 1 2}\right)^1 \left(1-{\frac 1 2}\right)^{3-1} \\\ \\\ =3\times\frac 1 2\times \left(\frac 1 2 \right)^2=\frac 3 {2^3}=\frac 3 8$$

####  **Empirical verification**
Since a Bernoulli trial has two possible outcomes, and in this scenario each outcome is equally likely, binary numbers can be used to represent a series of trials. Three trials (puppies) has the following 8 possibilities:
$$\begin{matrix}0=000 & 4=100 \\\ 1=001 & 5=101  \\\ 2=010 & 6=110 \\\ 3=011 & 7=111\end{matrix}$$
Out the 8 possible outcomes, 3 of them meet the criteria for "1 male and 2 females out of three pups". Namely, outcomes 1, 2, and 4 have *k* 0s.

## Expected outcome
Design an algorithm to optimally compute *P(k)* given these constraints:
* No devision, multiplication, addition, or subtraction.
* Time must be prioritized over space. If there are options of two symmetric but imbalanced asymptotic complexity, pick the one that is more time efficient.
* Implement with parallelization in Python 3.

---
<font size=1><sup>*</sup>Based on the August 10, 1997 issue from the "Ask Marilyn" column of *Parade* magazine.</font>
