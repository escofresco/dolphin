A district in Sweden chooses a new private company to supply voting machines for the upcoming election. There are three candidates, May, Feebee, and Gracie who run for office with a total of 100,000 votes submitted. When it's time to determine the winner, they notice something strange after all the votes are tallied. The total add up to more than 100,000! They subsequently perform a recount and the total is different again. This time it *does* total 100,000. It's not immediately obvious why there was originally a miscalculation until it occurs to somebody to view the vote counts in binary.

<br>

$$\footnotesize\text{Original Vote Count:}$$

<center>

|  |  |  |
|---:|---:|:---|
| May | `25,894` | `0b00110010100100110` |
| Feebee | `82,319` | `0b10100000110001111` |
| Gracie | `57,323` | `0b01101111111101011` |
| **Total** | <code><strong>165,536</code></strong> | <code><strong>0b11000011010100000</code></strong> |

</center>

<br>

$$\footnotesize\text{After Vote Recount:}$$

<center>

||||
|---:|---:|:---|
| May | `25,894` | `0b00110010100100110` |
| Feebee | `16,783` | `0b00100000110001111` |
| Gracie | `57,323` | `0b01101111111101011` |
| **Total**  | <code><strong>100,000 | <code><strong>0b11000011010100000</strong></code> |

</center>

<br>

Sure enough, there's a single mismatch for Feebee, specifically: the leftmost bit is flipped! It turns out that while vote counts were stored with sufficient data-loss prevent, the voting machine company 
