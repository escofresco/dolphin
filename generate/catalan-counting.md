# Catalan counting
## Background
The Catalan numbers *C<sub>1</sub>, C<sub>2</sub>, C<sub>3</sub>, ..., C<sub>n</sub>* are known to have the formula
$$C_n=\frac 1 {n+1} \binom{2n}{n}$$ which has applications in myriad combinatoric problems. One of those problems is counting Dyck ("deeck") sequences of length *n*. A Dyck word consists of the letters X and Y in equal number. Also, no prefix is allowed to have more Ys than Xs. For instance, XXYY is valid but YYXX is not. 

## Proof
We would like to run an experiment that proves *C<sub>n</sub>* for Dyck words of any length. This should be done by running *n* Bernoulli trials and counting the number of Dyck words. The algorithm might describe it thus:
$$

---
<font size=1>
<sup>1</sup> https://brilliant.org/wiki/catalan-numbers/

<sup>2</sup> Wikipedia contributors, "Dyck language," Wikipedia, The Free Encyclopedia, https://en.wikipedia.org/w/index.php?title=Dyck_language&oldid=1200731623 (accessed March 14, 2024).
</font>
