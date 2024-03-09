## Positively missing
### Scenario
A school district is allocating the annual budget and this year they have decided to change the way that age demographics are factored in. This year, a bonus will be allotted in diminishing value for a collection of age brackets such that
$$budget_{\text{age}}\propto \frac{1}{age}$$
To help every school maximize how much money they get, the district would like to write a web app that would identify the age group under the minimum requirement that would do this. The user would provide a list of student ages and the program would determine the target age group, if one exists. 

### Example
$$ \text{student ages: }A^{\prime} = [8, 8, 12, 8, 9, 10]\\\\ \text{min req'd to receive bonus: } r  = 2\\\ \text{age range of students: } ages \isin [8,14]$$
$$\thereforeƒ(A^{\prime}, r, ages) = 9$$


### Requirements
Running as a serverless function, *ƒ*, on a web service that bills for compute time, the program must minimize total cost. It should accept the following as input:
* Mutable list of ages, *A*. Unlike *A'* from the  example above, this is a collection of unique natural numbers represents the ages for which a bonus has been receive. Extending the example *A'* above would yield the following transformation:
$$A^{\prime} \xRightarrow{A} [8]$$
For this reason, *r* and *ages* are not needed to find a solution since the information is implicitly embedded in *A*.

### Solution
```python
def first_missing(A: List[int], ages: List[int]) -> int:
    A[:] = map(lambda x: x-ages[0], A)
    i = 0
    while i < len(A):
        if 0 < A[i] <= len(A) and A[i] != A[A[i]-1]:
            A[A[i]-1], A[i] = A[i], A[A[i]-1]
        else:
            i += 1
    for i, a in enumerate(A):
        if i+1 != a:
            return i+1+ages[0]
    return len(A)+1+ages[0]
```

### Expected Response
* Demonstrate the importance this solution has for compute time as compared to sorting the input.
* Explain the purpose of the first line subtracting every number from the minimum age in range `ages`.
* Create a variable table for `i` and `A` to represent the states of the while loop.
* Explain the meaning of the second pass. Why can this be consolidated with the while loop?
