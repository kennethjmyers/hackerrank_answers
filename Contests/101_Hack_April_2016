# 101 Hack April 2016

Contest.

## Super Reduced String

```
S = list(input().strip())

if len(S) == 1:
    print(S[0])
else:
    i = 0
    while i <= len(S)-1:
        # This step can only be done if not on the last letter
        if i < len(S)-1:
            # Check next letter
            if S[i] == S[i+1]:
                S.pop(i+1)
                S.pop(i)
                continue
        # Check previous letter
        if S[i] == S[i-1] and i>0:
            S.pop(i)
            S.pop(i-1)
            i-=1 # Move backwards, helps with near the end of strings
        else:
            i+=1

    if S:
        print(''.join(S))
    else:
        print('Empty String')
```

## Super Humble Matrix

```
b = 1000000007

facts = {0:1,1:1}
for i in range(2,2*10**6+1):
    facts[i] = ((i)*(facts[i-1]))%b

N,M = list(map(int,input().strip().split()))

# The solution is found by multiplying together each
# factorial of the number of elements in a diagonal
counts = 1
if N==M==1:
    print(1) # only one way to make this matrix
elif N==1 or M ==1:
    print(1) # only one way to make this type of matrix
else:
    if (N+M-1) %2  == 0: # Check if # of diagonals is even
        for i in range((N+M-1)//2):
            j = min(i+1,min(N,M))
            counts = ((counts%b)*(facts[j]%b))%b
            counts = ((counts%b)*(facts[j]%b))%b

    else: # if odd # of diagonals
        for i in range((N+M-1)//2):
            j = min(i+1,min(N,M)) # amount in diag. cant exceed min(N,M)
            counts = ((counts%b)*(facts[j]%b))%b
            counts = ((counts%b)*(facts[j]%b))%b
        if N==M: #if square the middle diagonal is one longer
            counts = ((counts%b)*(facts[j+1]%b))%b
        else: #if not square the middle diagonal is same as previous
            counts = ((counts%b)*(facts[j]%b))%b

    print(counts)
```

## Super Maximum Cost Queries

Didn't finish this one
```
from collections import defaultdict

N,Q = list(map(int,input().strip().split()))

edge_weights = defaultdict(int)
edges = []
for _ in range(N-1):
    edge = list(map(int,input().strip().split()))
    ordered_edge = [min(edge[0],edge[1]),max(edge[0],edge[1])]
    weight = edge[2]
    for j in range(ordered_edge[0]+1,N+1):
        if edge_weights[tuple([ordered_edge[0],j])] == 0:
            edge_weights[tuple([ordered_edge[0],j])] = weight
        else:
            edge_weights[tuple([ordered_edge[0],j])] =\
                        max(weight,edge_weights[tuple([ordered_edge[0],j])])
    for j in range(1,ordered_edge[1]+1):
        if edge_weights[tuple([j,ordered_edge[1]])] == 0:
            edge_weights[tuple([j,ordered_edge[1]])] = weight
        else:
            edge_weights[tuple([j,ordered_edge[1]])] =\
                        max(weight,edge_weights[tuple([j,ordered_edge[1]])])
    if ordered_edge[1]-ordered_edge[0] == 1:
        edge_weights[tuple([ordered_edge[0],ordered_edge[1]])] = weight

for k,v in edge_weights.items():
    print(k,v)
```
