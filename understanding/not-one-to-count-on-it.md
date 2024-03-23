# Not one two count on it
## Background
The fibonacci sequence is regarded as one of the most universal, straightforward patterns in nature. The simple rule *F<sub>n</sub>* = *F<sub>n-1</sub>* + *F<sub>n-2</sub>* is easy to generate for any *n*, but what of its proof? Not quite as simple. 

The insight someone had was to count the combinations of 1,2 sequences that sum to *n* - 1<sup>1</sup>. 

$$\begin{align\*}F_0 = 0 &= |\lbrace\rbrace| \newline F_1 = 1 &= |\lbrace () \rbrace| \newline  F_2 = 1 &= |\lbrace (1) \rbrace| \newline   F_3 = 2 &= |\lbrace (1,1),(2) \rbrace| \newline  F_4= 3 &= |\lbrace (1,1,1),(1,2),(2,1) \rbrace| \newline  F_5 = 5 &= |\lbrace (1,1,1,1),(1,1,2),(1,2,1),(2,1,1),(2,2) \rbrace| \newline \end{align\*}$$

If you are skeptical like me, you might wish to verify this claim. Great! Read on. 

## Empirical validation
We'll skip past the analytical proof and instead generate cardinalities of 1,2 sequence combinations for any *n*. 

```python
def verify(n):
    def combinations_cardinality(n):
        def combinations(n):
            if n <= 0:
                if n == 0:
                    return 1
                return 0
            return combinations(n-1) + combinations(n-2)
        return combinations(n-1)
    def fibonacci(n):
        if n <= 1:
            return n
        return fibonacci(n-1) + fibonacci(n-2)
    return fibonacci(n) == combinations_cardinality(n)

def verify_all(n_trials):
    return all(verify(n+1) for n in range(n_trials))

print(verify_all(10))
```
Something surprising is how similar `combinations_cardinality` and `fibonacci` look. Further explanation is needed.

## Expectations
The notion that counting 1,2 combinations summing to *n* will yield *F<sub>n</sub>* is a little unintuitive. Why does the recursive implementation of `fibonacci` look so similar to the recursive implementation of 1,2 combinations? Explain the connection analytically.

---
<font size=1>

<sup>1</sup>[Fibonacci sequence](https://en.wikipedia.org/wiki/Fibonacci_sequence), (last visited Mar. 22, 2024)

</font>
