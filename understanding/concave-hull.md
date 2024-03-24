# Concave cityscape
## Background
The view of a crowded city is mostly occluded by rectangular buildings. The problem herein assumes buildings are on a level horizon, where each one is represented by the sequence

$$B_i=\langle \text{left, right, height} \rangle.$$

We are only concerned with the upper region since the bottom is trivially known to be interval [left<sub>0</sub>, right<sub>*n*</sub>). The issue arises from overlapping rectangles where we are asked to create a new series that do not overlap but still represent the same skyline. In short, a concave shape<sup>†</sup>.

## Example
Given the buildings

$$ B=\lbrace\langle 0,4,3\rangle, \langle 4,13,6 \rangle, \langle 8,16,5\rangle ,\langle 14,21,8\rangle, \langle 21,32,3\rangle \rbrace,$$

the illustration is this:

```text
              ,------.
              |      |
    ,-------. |      |
    |   ,___|_|_.    |
    |   |       |    |
,---|   |       |    |----------.
|   |   |       |    |          |
|   |   |       |    |          |
⌊___|___|_______|____|__________⌋
```
becomes
```text
              ,------.
              |      |
    ,-------. |      |
    |       |_|      |
    |       | |      |
,---|       | |      |----------.
|   |       | |      |          |
|   |       | |      |          |
⌊___|_______|_|______|__________⌋

```
## Solution
```python
from collections import namedtuple
Rect = namedtuple('Rect', ('left', 'right', 'height'))

def concave_hull(buildings: List[Rect]) -> List[Rect]:
    min_x = min(buildings, key=lambda b: b.left).left
    max_x = max(buildings, key=lambda b: b.right).right
    heights = [0] * (max_x - min_x + 1)
    for building in buildings:
        for x in range(building.left, building.right + 1):
            delta = x - min_x
            heights[delta] = max(heights[delta], building.height)
    skyline = []
    left = 0
    for y in range(1, len(heights)):
        if heights[y] != heights[y-1]:
            skyline.append(
                Rect(left+min_x, y-1+min_x, heights[y-1])
            )
            left = y
    return skyline + [Rect(left+min_x, max_x, heights[-1])]
```

## Expectations
* Explain how this solution compares to the divide-and-conquer textbook solution. When does it perform better? When does it perform worse?
* Justify the *O(nm)* runtime, where *m* is the largest width.
* Without providing code, extend the solution to a scenario where buildings are equilateral triangles instead of rectangles. 

---

<font size=1>

<sup>†</sup>Concavity and convexity are two comparable space-filling paradigms. A convex hull is an enclosure of all points such that any line connecting two points will also be enclosed. On the other hand, a concave hull is one that encloses all points while minimizing the total area. This problem concerns the latter. 

</font>
