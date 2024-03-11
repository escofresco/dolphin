# Metal chain interleaving
## Scenario
An elevator manufacturer has run into an irreversible supply issue: the metal chains they ordered to support box-lift functionality arrived linked in strictly increasing strength such that the weight of any chain link is proportional to its strength. Moreover, when the assembled chain lies hanging vertically, any link *L<sub>i</sub>* must support the sum of weights of all links beneath it. The elevator's chain must operate bidirectionally where the order of links will be reversed depending on whether the elevator box is at the top or bottom of the lift. In other words, the elevator manufacturer cannot simply orient the chain in decreasing weight which would minimize the cumulative weight on any individual link because the order of links will be reversed depending on the lift's vertical position. 
## Solution
The manufacture would like to test several chain-link configurations as efficiently as possible. One configuration is the subject of this solution: chain interleaving. They have a factory robot that consists of two arms which are capable of swapping any to chain-links and would like to write a python algorithm that interleaves the head and tail of a metal chain. 

### Example
Below is a generalization of the desired reconfiguration. It shows the first link connected to the last link, the second link connected to the second to last link, and so forth.


$$\text{original chain}\\\\ \ \\\\ \boxed{L}\rarr \boxed{l_0}\rarr \boxed{l_1}\rarr \boxed{l_2}\rarr \dotso\rarr\boxed{l_{n-1}}\rarr \boxed{l_n}\rarr \varnothing \\\ \ \\\ \text{weaved chain}\\\\ \ \\\\ \boxed{L}\rarr \boxed{l_0}\rarr \boxed{l_n}\rarr \boxed{l_1}\rarr \boxed{l_{n-1}}\rarr \boxed{l_2}\rarr \dotso\rarr\varnothing$$

### Robot module
```python
def interleaved_chain(head: ListNode) -> Optional[ListNode]:
    if not (head and head.next):
        return head
    slow = head
    fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    midpoint = slow.next
    slow.next = None
    midpoint = reversed_chain(midpoint)
    h1 = head
    h2 = midpoint
    while h2:
        h1_next = h1.next
        h2_next = h2.next
        h1.next = h2
        h2.next = h1.next
        h2 = h2_next
        h1 = h1_next
    return head

class ListNode:
    def __init__(self, next_node):
        self.next = next_node

def reversed_chain(head):
    x = head
    while x and x.next:
        y = x.next
        z = y.next
        x.next = z
        y.next = head
        head = y
    return head
```

## Expected response
When the program above is executed, the robot eventually connects the head and tail so that it is perpetually rearranging the metal chain until a factory worker has to manually shut it off. 
* Identify the error in the Python module above that prevents `interleave_chain` from halting by providing correction for the line(s) at fault. Do not provide the entire rewritten file unless the error is systemic. 
* Offer advice about preventing errors like this in the future.
* Use a specific example that proves the correctness of the proposed solution.
