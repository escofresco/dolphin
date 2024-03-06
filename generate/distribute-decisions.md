### Distributor decisions
A clothing brand is looking automate the way they choose to replace items for their store locations. Every store is expected to have shirts and pants in equal number. They use the letter *d* to denote the difference in quantities of tops (positive) and bottoms (negative). At the end of the day, every store requests *d* replacement items. The brand's distributor looks at the orders and attempts to ship a pair of new items in their entirety so as to leave nothing more of that item left over. 

The distributor begins with a list *A* of *n* items in absolute sorted order. (Remember, the quantity of bottoms is multiplied by -1.) For every order request, they would like to determine if there's a pair of quantities that will sum to *k* to restore the store's inventory *d*, where *k=-d*. If there is, they need to know the pair's indices. 

Take the distributor's available items below for example.

$$\begin{array}{}-3 & 3 & 3 & 5 & -7 & -8 & 12 & 59\end{array}$$

The order function for *d=-5* should select *A<sub>4,6</sub>* for *k=5* since this would replace five bottoms missing from the store's inventory. 

### Expected outcome
* Write a python function `select_items_by_sum` that identifies a pair of item-indices from an absolute sorted array *A* whose quantities add to *k*. It must run in *Θ(n)* time and constant space.
* How would you generalize `select_items_by_sum` to work with more than two items?
