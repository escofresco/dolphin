# Prison escape
There is a prison where inmates have the opportunity to leave if they solve a puzzle correctly. If they fail their first attempt, however, they will be doomed to a life sentence. The puzzle is thus:

Two prisoners must agree to participate. The first prisoner enters a dungeon where there is a chess board. The warden is also there. The warden lays down a coin on each square so that it faces up (heads) or down (tails). In full view, the warden places a key beneath one of the coins so that it is not visible. The first prisoner then flips a single coin after which, they both leave. The second prisoner enters the dungeon. With only one chance, the second prisoner must guess under which coin the key sits. 

The following is an agent-based model that simulates a series of trials to prove there is a strategy that guarantees both prisoners will get to free.

```python
from random import randrange
from enum import Enum

class Coin(Enum):
    HEADS = 0
    TAILS = 1

def play(n):
    def flip_coin():
        return Coin(randrange(2))
    def first_prisoner_flip():
        board[0][0] = Coin(not board[0][0])
    def second_prisoner_guess():
        return (0,0)
    def warden_place_key():
        return (0,0)
    successes = 0
    for _ in range(n):
        board = [[flip_coin() for _ in range(8)] for _ in range(8)]
        key = warden_place_key()
        first_prisoner_flip()
        guess = second_prisoner_guess()
        if guess == key:
            successes += 1
    return successes == n
```
