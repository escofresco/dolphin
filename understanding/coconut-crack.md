# To crack a coconut
## Background
A forager is going around the forest gathering coconuts. When they see some that look ripe, the forager climbs to the top of the tree, grabs a coconut, and plops it onto the ground. Sometimes they crack, which is not good. 

Given a unit of length, the forager wants to know how many coconuts would be needed to determine the highest point they can be dropping in tact. 

## Rules
Our goal is to determine the highest point coconuts can be dropped from without them cracking. The following are assumed to be true:
* If a coconut cracks from being dropped, it will also crack at any higher point.
* A coconut that remains in tact can be reused, a cracked one must be tossed.
* Coconuts are fungible.

## Python implementation
```python
def drop_height(coconuts, drops):
    def _drop_height(coconuts, drops):
        if 0 in (coconuts, drops):
            return 0
        if coconuts == 1:
            return drops
        if cache[coconuts][drops] is None:
            cache[coconuts][drops] = (_drop_height(coconuts, drops-1) + 
                                      _drop_height(coconuts-1, drops-1) + 1)
        return cache[coconuts][drops]
    cache = [[None]*(drops+1) for _ in range(coconuts+1)]
    return _drop_height(coconuts, drops)
```

## Expectations
* Explain the recurrence

$$R(c+1,d)=R(c,d-1)+R(c+1,d-1)+1.$$

* How do the recursive and dynamic programming implementations compare in terms of asymptotic complexity?
* What would need to be changed for the original implementation to use less space?
