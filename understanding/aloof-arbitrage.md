# Aloof arbitrage
## Background
A quantitative analyst is doing some research to examine the performance of Hidden Markov Models (HMMs) on a theoretical concept they are developing called Arbitrage Drift Prevention. The idea behind it is to hedge currency trades with Foreign Exchange Options before an arbitrage opportunity has occurred to minimize the drift that results from heavy trading volume. The foundation for their theory depends on having sufficient data for training the HMMs, so the researcher has written a function that takes an adjacency matrix of exchange rates as input and answers the question, "does arbitrage exist?" 

## Solution
For now, the researcher ignores price fluctuations and transaction costs. 
```python
from math import inf, log10
def arbitrage_exists(exchange_rates):
    def bellman_ford(weighted_graph, src):
        src_dist = ([inf] * (src-1) + [0] + 
                    [inf] * (n-src))
        for _ in range(1, n):
            updated = False
            for i, row in enumerate(weighted_graph):
                for j, cell in enumerate(row):
                    if (src_dist[i] != inf and 
                        src_dist[j] > src_dist[i] + cell):
                        updated = True
                        src_dist[j] = src_dist[i] + cell
            if not updated:
                return False
            return any(src_dist[i] != inf and 
                       src_dist[j] > src_dist[i] + cell 
                       for i in range(len(weighted_graph)) 
                       for j, cell in enumerate(weighted_graph[i]))
    n = len(exchange_rates)
    return bellman_ford([[-log10(rate) for rate in rates] 
                         for rates in exchange_rates], 0)
```

## Expectations
* To what extent is floating point accuracy an issue? Does the answer depend on programming language (i.e. Python vs C++)? What are some mitigation strategies?
* What is the runtime of this solution? Is it practically feasible, for, say, 1e9 tables?
* Describe the Bellman-Ford algorithm, especially the insight that logarithms allow for the transformation of multiplication into addition. Use an analytic approach to explain why.
* Why can't Dijkstra's algorithm be used for arbitrage? Is the same true for Floyd-Warshall?
* The researcher is more concerned about time than space. In terms of time, is this solution theoretically optimal, practically optimal, or neither?
* In terms of arbitrage, what is the meaning of a negative-weight cycle?
