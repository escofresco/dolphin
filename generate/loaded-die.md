# Loaded Die
## Background
A magician is allowing people to guess which of their dice is loaded. Just from observation, it's not possible to tell them apart. The magician places all *n* dice in three rows so that they each contain *x*, *y* and *z* dice respectively. Participants are allowed to ask if a subset of a particular row contains the loaded die and the magician will answer honestly. The magician offers a reward to anyone who can identify the loaded die in the fewest questions. In order to determine is a participant has answered correctly, the magician needs a program that provides the answer in a reasonable amount of time.

## Instructions
Let's call the minimum number of guesses required to narrow down the dice *g(x,y,z)*. Write a function for the magician that computes *g(x,y,z)* such that 1 ≤ x + y + z < ∞.

## Examples
$$g(0,0,1) = 0\\\ g(0,1,1) = 1 \\\ g(1,2,3) = 3 \\\ g(2,3,3) = 4$$

## Requirements
* Use Python 3.12.
* Prioritize time complexity over space.
* Prove by induction that the solution is correct for all Natural numbers *x*, *y*, *z*.


---

<font size=1>

*Based on ["Jack's Bean"](https://projecteuler.net/problem=847).
