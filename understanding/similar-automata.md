# Similar simplex
## Background
Cellular automata (CA) is a fantastic way to produce self-similar patterns. The program we have below uses some simple rules to create nested triangular wedges.

```python
import numpy as np
import matplotlib.pyplot as plt

n = 258
m = 128

img = np.zeros([m, n], dtype=int)
img[0, n//2] = 1

for i in range(1, m):
    for j in range(1, n-1):
        if img[i-1, j+1] + img[i-1, j-1] == 1:
            img[i,j] = 1
    img[i, 0] = img[i, n-2]
    img[i, n-1] = img[i, 1]
plt.imshow(img, interpolation='nearest')
plt.show()
```

## Expectations
* Explain the following about our Python script:
  * Compare the macroscopic and microscopic patterns produced.
  * What makes it 1-dimensional?
  * Infer the four rules dictating cellular behavior here.
  * To what extent is the graphical geometric pattern self-similar and does that make it a fractal?
  * Which category of CA is this: class I, class II, or class III? 
  * Is the pattern a 2-dimensional simplex?
