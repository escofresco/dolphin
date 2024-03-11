## Sandwich Powerset
### Explanation
A chef named Sabrina has just endeavored to make a world-class sandwich. She is known for her exhaustive approach to recipes, tirelessly asking her friends and family to try every possible combination of ingredients (to an extent). Sabrina is strictly opposed to ruling out any strange combinations from her recipes. After curating only four ingredients, however, the sandwich variations start to become too overwhelming to continue even though order does not matter. Below is the set of all the possible ways of using _bread_, _tomato_, _lettuce_, and _bacon_ to make a sandwich, including where there's only a side-salad but no sandwich at all and serves as the control group.

 $$ \footnotesize 𝒫(S) =\tiny\begin{Bmatrix} \begin{Bmatrix}\end{Bmatrix} \\\ \\\ \begin{Bmatrix} tomato \end{Bmatrix} \begin{Bmatrix} lettuce \end{Bmatrix} \begin{Bmatrix} bacon \end{Bmatrix}\\\ \\\ \begin{Bmatrix} bread \\\ tomato \\\ \end{Bmatrix} \begin{Bmatrix} bread \\\ lettuce \\\ \end{Bmatrix} \begin{Bmatrix} bread \\\ bacon \end{Bmatrix} \begin{Bmatrix} tomato \\\ lettuce \\\ \end{Bmatrix} \begin{Bmatrix} tomato \\\ bacon \\\ \end{Bmatrix} \begin{Bmatrix} lettuce \\\ bacon \\\ \end{Bmatrix} \\\ \\\ \begin{Bmatrix} bread\\\  tomato \\\ lettuce \\\ \end{Bmatrix} \begin{Bmatrix} bread \\\ tomato \\\ bacon \end{Bmatrix} \begin{Bmatrix}bread \\\ lettuce \\\ bacon \end{Bmatrix}\begin{Bmatrix}tomato \\\  lettuce \\\ bacon \end{Bmatrix} \\\ \\\ \begin{Bmatrix} bread & tomato \\\ lettuce & bacon \end{Bmatrix} \end{Bmatrix}$$


As the reader might already be able to tell from this example, manually enumerating sandwich combinations is unfeasible. In fact, exponentially so. The cardinality of the powerset is _2<sup>|S|</sup>_ where _S_ is the four sandwich ingredients in this example. Altogether, Sabrina needs an algorithm that provides the set of all subsets of a set _S_.



### Expected Response
* _Use Python to compute the power set from a list of unique values_.
  * _Provide both the recursive and iterative implementations_.
* _Supply the recursive solution first._
  * _Its runtime must satisfy the recurrence_ C(n) = 2C(n - 1) = O(2<sup>n</sup>).
* _Supply the iterative solution second._
  * _Ensure_ O(n) _space complexity for the iterative implementation._
  * _Derive this from the bijection between the_ 2<sup>n</sup> _bit vectors  of length_ n _and the powerset._

<br/>
<br/>

---
###### 1. Power set, https://en.wikipedia.org/w/index.php?title=Power_set&oldid=1206654169 (last visited Feb. 26, 2024).

