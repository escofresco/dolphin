The game team at Bindows responsible for Solitaire are looking to make performance improvements. One task is to eliminate animation latency for card shuffles. The existing event loop currently uses `ArrayList` for the deck data structure. However, one thing someone on the team is doing is using a 64-bit number instead of an array. Below is the "bit to label" mapping, which depicts the ordered bijection of bit sets and their corresponding cards.

$$\begin{matrix} \lbrack 0^0\ ,0^{13} \rparen : & \text 2\spadesuit\ \text 3\spadesuit\ \text 4\spadesuit\ \text 5\spadesuit\ \text 6\spadesuit\ \text 7\spadesuit\ \text 8\spadesuit\ \text 9\spadesuit\ \text 10\spadesuit\ \text J\spadesuit\ \text Q\spadesuit\ \text K\spadesuit\ \text A\clubs\ \\\  \lbrack 0^{13} ,0^{26} \rparen : & \text 2\hearts \ \text 3\hearts \text 4\hearts\ \text 5\hearts\ \text 6\hearts\ \text 7\hearts\ \text 8\hearts\ \text 9\hearts\ \text 10\hearts\ \text J\hearts\ \text Q\hearts\ \text K\hearts\ \text A\hearts\ \\\  \lbrack 0^{26} ,0^{39}  \rparen : & \text 2\clubs\ \text 3\clubs\ \text 4\clubs\ \text 5\clubs\ \text 6\clubs\ \text 7\clubs\  \text 8\clubs\ \text 9\clubs\ \text 10\clubs\ \text J\clubs\ \text Q\clubs\ \text K\clubs\ \text A\clubs\ \\\  \lbrack 0^{39} ,0^{52} \rparen : & \text 2\blacklozenge\ \text 3\blacklozenge\ \text 4\blacklozenge\ \text 5\blacklozenge\ \text 6\blacklozenge\ \text 7\blacklozenge\ \text 8\blacklozenge\ \text 9\blacklozenge\ \text 10\blacklozenge\ \text J\blacklozenge\ \text Q\blacklozenge\ \text K\blacklozenge\ \text A\blacklozenge\ \end{matrix}$$

For instance the two of clubs equals the 26th bit set. Furthermore, the one-on-one correspondence for an arbitrary deck of five cards would be this:

$$\tiny\\begin{matrix}000000000000000&0&0000000000&0&0000000000000000000000&0&00\\\ &\ \text{K}\clubs &\ &\ 2\clubs&\ & 4\spadesuit \end{matrix}$$
##### Extended class for little endian devices.
```python

```

In addition t