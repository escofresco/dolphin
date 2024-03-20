Find the number of subsets of {1,2,3,4,...,n} whose sum is divisible by 5. O(2<sup>n</sup>)

p(x) = (1+x^1)(1+x^2)(1+x^3)(1+x^4)...(1+x^n)
f(x) = ∑_n=0^N c_n x^n = c_0 + c_1x + c_2x^2
coefficient indicates number of subsets
exponent indicates sum of corresponding subsets
