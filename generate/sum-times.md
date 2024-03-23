# Some time for sum times
## Background
Consider an expression of the form 
$$c_0\odot c_1\odot c_2 \odot c_3\odot c_4$$
where ⊙ denotes an arithmetic operator. The expression will result in different values based on whether some or all operators are ×, +, etc. There exists a function ƒ that determines the operators for a result and sequence of integers.

For example,
$$ƒ(\text{values}=\lang4,8,2,1\rang, \text{result}=10)=\lang+,-,×\rang$$
because of the result from interpolating these operators:
$$4+8-2×1=10$$

There's a famous NP-complete reduction of this problem that deals with arranging a collection of numbers into two equal-sum partitions. Similarly, we'd like to write a function ƒ' that implements ƒ with only + and × allowed to substitute ⊙.

## Expectations
 Given a sequence of integers and target result, implement ƒ' in Python. It must include a heuristic to improve the *O(n3<sup>n</sup>)* runtime  in some cases.
