# Time for some answers
## Problem 
An arithmetic expression consisting of multiplication and addition is supplied with the operands missing. Given a numerical result, a solution is needed to determine if it is possible.

## Solution
```python
def synthesize(A, target):
    def directed(A, curr):
        def compute():
            ops = iter(operands)
            intermediates = [next(ops)]
            for op in operators:
                if op == '*':
                    prod = intermediates[-1] * next(ops)
                    intermediates[-1] = prod
                else:
                    intermediates.append(next(ops))
            return sum(intermediates)
        curr = curr * 10 + A[0]
        if len(A) == 1:
            operands.append(curr)
            if compute() == target:
                return True
            operands.pop()
            return False
        if directed(A[1:], curr):
            return True
        operands.append(curr)
        operators.append('*')
        if directed(A[1:], 0):
            return True
        operands.pop()
        operators.pop()
        operands.append(curr)
        if target - compute() <= reduce(lambda v,d: v*10+d, A[1:], 0):
            operators.append('+')
            if directed(A[1:], 0):
                return True
            operators.pop()
        operands.pop()
        return False
    operands = []
    operators = []
    return directed(A, 0)
```

## Expectations
* Prove the worst-case *O(n3<sup>n</sup>)* time complexity.
* Annotate the solution with explanatory comments.
* Infer the runtime in a scenario with division and subtraction in addition to multiplication and addition.
* Is the solution NP-complete? Why or why not?
