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

[Helpful video on this theorem](https://www.youtube.com/watch?v=gdmfOwyQlcI)
```
from collections import defaultdict


T = int(input().strip())

for _ in range(T):
    N,M = [int(i) for i in input().strip().split()]
    weight_matrix = [[0]*N for _ in range(N)]
    for e in range(M):
        x,y,r = [int(i) for i in input().strip().split()]
        weight_matrix[x-1][y-1] = min(list(filter(None,[weight_matrix[x-1][y-1],r])))
        weight_matrix[y-1][x-1] = min(list(filter(None,[weight_matrix[y-1][x-1],r])))
    S = int(input().strip())
    min_distance_dict = defaultdict(lambda:100000000)
    #print(weight_matrix)

    #Dijkstra
    next_node = S-1
    explored_nodes = set()
    to_be_explored = set([next_node])
    min_distance_dict[next_node] = 0
    while to_be_explored:
        for i,x in enumerate(weight_matrix[next_node]):
            if x!=0:
                to_be_explored.add(i) #add connected nodes to the set to be explored
                #set the distance to the min of the current distance and the distance
                #the previous node plus the weight of this edge
                min_distance_dict[i] = min(min_distance_dict[i],min_distance_dict[next_node]+x)
                #remove this edge from the matrix as it has now been explored
                weight_matrix[next_node][i],weight_matrix[i][next_node] = 0,0
        explored_nodes.add(next_node)
        to_be_explored.remove(next_node)
        if not to_be_explored:
            break
        next_node = min(to_be_explored,key=lambda x:min_distance_dict[x])

    #print results
    for i in range(N):
        if min_distance_dict[i] == 100000000:
            print(-1, end=' ')
        elif i!=S-1:
            print(min_distance_dict[i], end=' ')

    print()
```

## [Prim's (MST): Special Subtree](https://www.hackerrank.com/challenges/primsmstsub)

Learned Prim's from [this video](https://www.youtube.com/watch?v=z1L3rMzG1_A). My first solution used the matrix representation of a graph but after doing some reading I found that that method can be slow due to iterating over all possible connections every node inspection. Using the hashtable-list method is more space and time efficient.

```
from collections import defaultdict

N,M = [int(i) for i in input().strip().split()]

distances = defaultdict(list)

for _ in range(M):
    x,y,r = [int(i) for i in input().strip().split()]
    distances[x].append([y,r])
    distances[y].append([x,r])

S = int(input().strip())

parent_weights = defaultdict(list)
for i in range(1,N+1):
    parent_weights[i] = [i,100000000,None] #thisnode, distance, parentnode

parent_weights[S] = [S,0,None]

min_comparison = 100000000
min_node = S

min_distance = 0
unexamined_set = set(list(range(1,N+1)))
examined_set = set()

while len(examined_set)<N:
    min_distance += parent_weights[min_node][1]
    for x in distances[min_node]:
        if parent_weights[x[0]][1] > x[1] and x[0] not in examined_set:
            parent_weights[x[0]] = [x[0],x[1],min_node]

    unexamined_set.remove(min_node)
    examined_set.add(min_node)

    next_min_node_dist = 100000000
    for x in unexamined_set:
        if parent_weights[x][1] < next_min_node_dist:
            next_min_node_dist = parent_weights[x][1]
            min_node = x

print(min_distance)
```
