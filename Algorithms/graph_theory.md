# Graph Theory

## Breadth First Search: Shortest Reach

```
from collections import defaultdict


T = int(input().strip())

for _ in range(T):
    N, M = list(map(int,input().strip().split()))

    adj_vertices = [[0]*N for _ in range(N)]

    for edge in range(M):
        e = list(map(int,input().strip().split()))
        if adj_vertices[e[0]-1][e[1]-1] == 0:
            adj_vertices[e[0]-1][e[1]-1] += 1
            adj_vertices[e[1]-1][e[0]-1] += 1

    S = int(input().strip())

    distances = defaultdict(int)
    visited = {S-1}
    Q = [S-1]
    while Q:
        next_node = Q.pop(0)
        for i,x in enumerate(adj_vertices[next_node]):
            if x == 1 and i not in visited:
                distances[i+1] += distances[next_node+1]+6
                visited.add(i)
                Q.append(i)

    #set any zeros to -1
    for i in (i for i in range(1,N+1) if i != S):
        if distances[i] == 0:
            distances[i] = -1
        print(distances[i], end=' ')

    print()
```

## Dijkstra: Shortest Reach 2

```

```
