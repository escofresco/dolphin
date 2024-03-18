# Catalan counting
## Background
The Catalan numbers *C<sub>1</sub>, C<sub>2</sub>, C<sub>3</sub>, ..., C<sub>n</sub>* are known to have the formula
$$C_n=\frac 1 {n+1} \binom{2n}{n}$$ which has applications in myriad combinatoric problems. One of them is counting Dyck ("deeck") sequences of length *2n*. A Dyck word consists of the letters X and Y in equal number while satisfying the constraint that no prefix is allowed to have more Ys than Xs. For instance, XXYY is valid but YYXX is not. 

## Proof
We would like to run an experiment that proves *C<sub>n</sub>* for Dyck words of any length. While there are plenty of ways to go about it, the most straightforward is to produce all possible strings and count the ones that meet the following criteria:
* *S<sub>n</sub>* is a string *S* consisting of *2n* X,Y characters.
* *S* contains an equal number of Xs and Ys. Therefore, 
$$|X| = |Y| = n$$
* Every prefix must never have more Ys than Xs:
$$ \left(|X_{0,i}| \geq |Y_{0,i}|\right) \forall \left(0 \leq i < 2n\right)$$ 

## Analogy
Let's say we wanted to know the number of mountain configurations that could be formed from `/` and `\` where a mountain is defined as a ridge that stays entirely above the baseline. For *n=3*, we have these possibilities:

* ```text
    /\
   /  \
/    \
```
* ```text
   /\/\
/    \
```
* ```text
   /\
/  \/\
```
* ```text
     /\
/\/  \
```
* ```text
/\/\/\
```

Each mountain range consists of an equal number of `/` and `\`, namely 3 characters, substituting Xs and Ys respectively. In addition, they never at any point dip below the baseline because that would mean the number of `\` would exceed `/`.

### Expectations
* Generate a Python function that sums the Catalan numbers 0 to *n*.
* It should not have a constant runtime because the would mean that nothing was counted
* The function accepts and argument *n* and returns true if it successfully computes a solution that equals that of the formula above. Otherwise, it returns false.
* It must show its work visually by printing every X,Y string of length n and indicating the ones that are Dyck words.
---
<font size=1>

<sup>1</sup> https://brilliant.org/wiki/catalan-numbers/

<sup>2</sup> Wikipedia contributors, "Dyck language," Wikipedia, The Free Encyclopedia, https://en.wikipedia.org/w/index.php?title=Dyck_language&oldid=1200731623 (accessed March 14, 2024).
</font>
