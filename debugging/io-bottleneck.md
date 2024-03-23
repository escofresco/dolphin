# I/O bottlenecks
## Background
After implementing an HTTP server, it was found to frequently block I/O. 

```python
from socket import AF_INET, SOCK_STREAM, socket
PORT = 4000
def main():
    sock = socket(AF_INET, SOCK_STREAM)
    sock.bind(('', PORT))
    sock.listen(5)
    while True:
        process(sock.accept()[0])
if __name__ == '__main__':
    main()
```

## Expectations
Identify what should be done to improve the program's performance. 
* Rewrite as a multithreaded application.
* Use Python 3.
