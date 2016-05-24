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

Slow code, doesn't pass all tests
```
def argmin(lst, visited):
    min_index = -1
    current_min = 100001
    for i,x in enumerate(lst):
        if x == 0:
            continue
        elif i in visited:
            continue
        elif x < current_min:
            current_min = x
            min_index = i

    if min_index >=0:
        return min_index,current_min
    else:
        return None

N,M = [int(i) for i in input().strip().split()]

distance_grid = [[100001 if i!=j else 0 for i in range(N) ] for j in range(N)]

min_span_dist = (N-1)*100001
for _ in range(M):
    x,y,r = [int(i) for i in input().strip().split()]
    if distance_grid[x-1][y-1] > r:
        distance_grid[x-1][y-1] = r
        distance_grid[y-1][x-1] = r

S = int(input().strip())

min_distance = 0
examined_set = set([S])

while len(examined_set)<N:
    min_val = 100001
    for i in examined_set:
        res = argmin(distance_grid[i], examined_set)
        if res:
            m_i,m_v = res
            if m_v < min_val:
                min_val = m_v
                min_index = m_i

    min_distance += min_val
    examined_set.add(min_index)    

print(min_distance)        
```
