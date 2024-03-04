Entropy Corp. is a galactic agency that enforces the second law of thermodynamics. Their Department of Shuffling is responsible for maximizing the disarray of ordered collections. The department has been using the Fisher-Yates algorithm<sup>1</sup> to shuffle numerical arrays. 
$$shuffle(A) : [swap(i)\ |\ 0 \leq i \lt |A|) \\\ swap : j ←random(i),\ [A_j,A_i] =[A_i , A_j]\\\ random :\\{c\\}→[c, |A|]$$
Having a culture of innovation, Entropy Corp. is always looking for new ways to sew chaos. Engineers at the Department of Shuffling decide to not only shuffle arrays, but shuffle the binary representation of each number as well. 

Here's the class that shuffles each binary number in an array in addition to shuffling the array itself:
```python
class ChaoticShuffle:

    def __init__(self, nums: List[int]):
        self.nums = nums
        self._nums = nums[:]
        
    def reset(self) -> List[int]:
        self.nums = self._nums[:]
        return self.nums
        
    def shuffle(self) -> List[int]:
        for j in reversed(range(len(self.nums))):
            i = random.randint(0, j)
            self.swap(i, j)
            self.shufflebits(j)
        return self.nums

    def shufflebits(self, i) -> int:
        nbits = math.ceil(math.log2(nums[i]))
        for j in range(nbits):
            i = random.randit(j, nbits - 1)
            self.swapbits(i, j)
        return nums[i]

    def swap(self, i, j):
        self.nums[i], self.nums[j] = self.nums[j], self.nums[i]

    def swapbits(self, x, i, j) -> int:
        j = nbits - i - 1
        ibit = (x >> i) & 1
        jbit = (x >> j) & 1
        mask = (1 << i) | (1 << j)
        if ibit != jbit:
            x ^= mask   
        return x
```

### Expected Outcome
Your job is to generate documentation for the `ChaoticShuffle` class. Future engineers need to be able to get up to speed on the functionality as well as practical and theoretical constraints. There also needs to be an "Abstract" section that helps leadership understand the *why*. That is, the Abstract must explain what about `ChaoticShuffle` aligns with the mission of Entropy Corp. 

Finally you must provide a criticism of the project. Presumably `ChaoticShuffle` is applied on arrays of thermodynamic quantities to increase disorder of system.

---
<font size=1>1. Fisher–Yates shuffle, https://en.wikipedia.org/w/index.php?title=Fisher%E2%80%93Yates_shuffle&oldid=1210716156 (last visited Mar. 3, 2024).</font>
