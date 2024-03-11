
## Securing Elections: A Simple Error Detection Technique for Accurate Vote Counts
### Scenario
A district in Sweden chooses a new private company to supply voting machines for the upcoming election. There are three candidates, May, Feebee, and Gracie who run for office. A total of 100,000 votes are submitted. When it's time to determine the winner, they notice something strange. After all the votes are tallied, the total adds up to more than 100,000! They subsequently perform a recount and the total is different again. This time it *does* sum to 100,000. It's not immediately obvious why there was originally a miscalculation until someone decides to analyze the vote counts in binary.

<br/>

$$\small\text{Original Vote Count:}$$


<center>


|  |  |  |
|---:|---:|:---|
| May | `(25,894)`₁₀ | `(0b00110010100100110)`₂ |
| Feebee | `(82,319)`₁₀ | `(0b10100000110001111)`₂ |
| Gracie | `(57,323)`₁₀ | `(0b01101111111101011)`₂ |
| **Total** | <code><strong>(165,536)</strong></code><strong>₁₀</strong> | <code><strong>(0b11000011010100000)</strong></code><strong>₂</strong> |

</center>

<br/>

$$\small\text{After Vote Recount:}$$

<center>

||||
|---:|---:|:---|
| May | `(25,894)`₁₀ | `(0b00110010100100110)`₂ |
| Feebee | `(16,783)`₁₀ | `(0b00100000110001111)`₂ |
| Gracie | `(57,323)`₁₀ | `(0b01101111111101011)`₂ |
| **Total**  | <code><strong>(100,000)</strong></code><strong>₁₀</strong> | <code><strong>(0b11000011010100000)</strong></code><strong>₂</strong> |

</center>

<br/>

<br/>

Sure enough, there's a single mismatch for Feebee, specifically: the leftmost bit is flipped! It turns out that while vote counts were stored with sufficient mechanisms to prevent data loss, the voting machine company neglected to do any error detection. When high-energy particles and gamma radiation occasionally collide with transistors, their the internal voltage can switch<sup>[1]</sup>. Disparate voting centers transmit information to a central server for aggregation after the election, subject to the possibility of Single Event Upsets (SEUs). 

## Error Checking in Python
The solution? Send a parity bit alongside each word. Check for any mismatches by counting the number of ones from its base-2 representation when it is sent and after it is received. Determine if the count is even or odd and use a 0 or 1, respectively. 

The worst solution would be to check every bit, which has _theta(n)_ time complexity. A better solution is to only count the 1 bits.

<br/>

##### Solution A
```python
def parity(x):
    result = 0
    while x:
        result ^= 1
        x &= x - 1
    return result
```
By iteratively dropping the lowest bit, the time complexity is improved to _O(k)_ where _k_ is the number of 1s. This will do well on sparse inputs.

Still though, we can do better. By taking advantage of the associativity and commutativity of XOR, a number can be continuously folded in half, all the while ignoring the leading bits. This means that parity can be computed in _O(log n)_ time where _n_ is the word size.

<br/>


##### Solution B

```python
def parity(x):
    """Determines odd or even 1s count of 64-bit word."""
    x ^= x >> 32
    x ^= x >> 16
    x ^= x >> 8
    x ^= x >> 4
    x ^= x >> 2
    x ^= x >> 1
    return x & 0x1
```

<br/>


<br/>

### _Instructions: Explanation Criteria_
* *Demonstrate the differing applicability between the _O(k)_ and _O(log n)_ solutions.*
* *Elaborate on the significance of returning `x & 0x1` instead of `x & 1` in "Solution A".*
* *Compare practical and theoretical performance of both solutions to the bruce-force algorithm.*
* *Derive "Solution B" from first principles.*

---

###### 1. https://www.bbc.com/future/article/20221011-how-space-weather-causes-computer-errors
