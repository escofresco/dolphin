## Max profit from, at most, one transaction

### Scenario
Suppose a new cryptocurrency is created, Psychic Coin, that provides its own future exchange rates, `arr`. Aspiring investors are racing to get in on the action. While the general rule of thumb is to "buy low, sell high", it is very possible that the global max precedes the minimum price. 

### A naive solution
The most straightforward but inefficient solution is to search for the greatest positive difference between every possible pair of _`n`_ dates:
$$\begin{pmatrix}n \\\ 2\end{pmatrix} = \cfrac{n^{\underline{k}}}{2!} \rightarrow \cfrac{n^2 - {\xcancel{n}}}{\xcancel{2}} \propto \Theta(n^2)$$

### A better solution
A categorical improvement comes from the insight to apply a divide-and-conquer strategy. The max subarray is, _ipso facto_, always in _`arr`_ and an index `mid` can be chosen to demarcate two halves of _`arr`_. For that reason, the max subarray will be in one of three places: 
* the left half _`arr[low : mid]`_,
* the right half _`arr[mid + 1  : high]`_, 
* across the midpoint _`arr[low : high]`_.

The solution algorithm begins by finding three candidates. The input array is recursively split in half. For each half, a max subarray is computed unless the subarray has just one element. Otherwise, the potential answers are combined by deciding if a max subarray that must cross over the midpoint has a great profit than either of the two halves.


##### Helper function to find the max subarray that necessarily overlaps `mid`
```python
def max_crossing_subarray(arr, low, mid, high):
    left_sum = float('-inf')
    max_left = 0
    cross_sum = 0
    for i in reversed(range(mid, low)):
        cross_sum += arr[i]
        if cross_sum > left_sum:
            left_sum = cross_sum
            max_left = i
    right_sum = float('-inf')
    max_right = 0
    cross_sum = 0
    for j in range(mid+1, high):
        cross_sum += arr[j]
        if cross_sum > right_sum:
            right_sum = cross_sum
            max_right = j
    return max_left, max_right, left_sum + right_sum
```

##### Solution function to recursively select the three best candidates 
```python
def max_subarray(arr, low, high):
    if high == low:
        return low, high, arr[low]
    mid = (lo + hi) // 2 
    left_low, left_high, left_sum = max_subarray(arr, low, mid)
    right_low, right_high, right_sum = max_subarray(arr, mid, high)
    cross_low, cross_high, cross_sum = max_crossing_subarray(arr, low, mid, high)
    if left_sum >= right_sum and left_sum >= cross_sum:
        return left_low, left_high, left_sum
    elif right_sum >= left_sum and right_sum >= cross_sum:
        return right_low, right_high, right_sum
    return cross_low, cross_high, cross_sum
```

<br/>

### _Debugging criteria_
* _Identify off-by-one errors for_ `max_subarray` _and_ `max_crossing_subarray`.
* _Prevent stack overflow for large inputs._
* _Prevent integer overflow for_ `(lo + hi) // 2` _in_ `max_subarray` _given there is a possibility of this occurring in Python._
* _Show your work. Provide a line-by-line walkthrough of_ `max_subarray` _solving for the array_ `[112,113,109,86,105,102,86,63,81,102,99]` _which demonstrates that verifies the function's correctness._
* _Use the recurrence below as a basis for verification of_ `max_subarray` _and_ `max_crossing_subarray`_:_

$$T(n) = \begin{cases}\Theta(1)&\text{if }n = 1\\\2T(\cfrac{n}{2}) + \Theta(n)&\text{if } n > 1\end{cases}$$
* _Ensure the recurrence above is true_.

<br/>
<br/>
<br/>

---
###### 1. _Introduction to Algorithms_ Third Edition by Thomas H. Cormen, Charles E. Leisierson, Ronald L. Rivest, Clifford Stein (p. 68 – 72, 74).
###### 2. Binomial coefficient, https://en.wikipedia.org/w/index.php?title=Binomial_coefficient&oldid=1209721718 (last visited Feb. 25, 2024).
