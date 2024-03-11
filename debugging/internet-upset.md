## Internet Upset
### Scenario
An internet service provider (ISP) is looking to identify subscribers whose usage exceeds 1% to throttle their access during busy times. Anytime a user makes a request, their unique id is appended to a common file. The ISP would like to generate a report of any time granularity. For security purposes, the software program cannot read a dataset more than twice without needing to re-request permission. At the same time that there's guaranteed to be enough space to store the solution, the entire dataset is too large to fit into memory.

### Solution
The existing code reads a stream of user ids and identifies the ones occurring more than *n/k* times. 
```python
def frequent_items(k, data_stream):
    candidates = collections.Counter()
    n = 0
    threshold = n / k

    for user_id in data_stream:
        candidates[user_id] += 1
        n += 1
        if len(candidates) == k:
            for candidate in candidates:
                candidates[candidate] -= 1
        candidates = +candidates

    for candidate in candidates:
        candidates[candidate] = 0

    for user_id in data_stream:
        if user_id in candidates:
            candidates[candidate] += 1
    return [candidate for candidate, count in candidates.items() if count > threshold]
```

### Expectations
There's a problem. `frequent_items` returns user frequencies that are below the *n/k* threshold, some only occurring once. Help the ISP fix their algorithm so they can get back to reducing heavy traffic.
