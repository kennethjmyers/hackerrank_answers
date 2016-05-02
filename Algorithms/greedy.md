# Greedy

## [Grid Challenge](https://www.hackerrank.com/challenges/grid-challenge)

Originally I was going to do this problem properly (by applying a bubble sort) but I thought (and I may be thinking of this wrong) that it didn't matter since I would still be sorting (O(N^2)) and then doing row by row comparisons whenever an element reached its final position. But I could just python sort it (tim sort, O(NlogN)) and then pass over it (O(NlogN) + O(N)). So I just went for the python sort.
```
T = int(input().strip())

for _ in range(T):
    N = int(input().strip())
    grid = []
    for n in range(N):
        grid.append(sorted(list(input().strip())))

    good = True
    for i in range(1,N):
        if not good:
            break
        for j in range(N):
            if grid[i][j] < grid[i-1][j]:
                good = False
                break

    if good:
        print('YES')
    else:
        print('NO')
```

## [Beautiful Pairs](https://www.hackerrank.com/challenges/beautiful-pairs)

```
from collections import Counter

N = int(input().strip())

A = [int(i) for i in input().strip().split()]
B = [int(i) for i in input().strip().split()]

a_count = Counter(A)
b_count = Counter(B)

a_excess = 0
b_excess = 0

a_not_in_b = 0
b_not_in_a = 0

pair_counts = 0
examined_nums = set() #keep track so we dont examine things twice
for k,v in a_count.items():
    if k in b_count:
        pair_counts += min(a_count[k],b_count[k]) #we can only make pairs from the minimum matching
        if a_count[k] < b_count[k]:
            b_excess +=1
        elif a_count[k] > b_count[k]:
            a_excess +=1
    else:
        a_not_in_b +=1
    examined_nums.add(k)

for k,v in b_count.items():
    if k not in examined_nums:
        b_not_in_a +=1

if a_not_in_b > 0 and b_not_in_a > 0:
    print(pair_counts+1)
elif (b_not_in_a > 0 and a_excess > 0) or (a_not_in_b > 0 and b_excess > 0):
    print(pair_counts+1)
else:
    print(pair_counts-1)
    #this is important, you always have to swap a B
    #but if you cant make a match then you lose a match
```

## [Jim and the Orders](https://www.hackerrank.com/challenges/jim-and-the-orders)

```
N = int(input().strip())

when_delivered = []
for n in range(N):
    order = tuple(int(i) for i in input().strip().split())

    delivered_at = order[0]+order[1] #we only need to know when its delivered to place it in the order sequence
    if not when_delivered:
        when_delivered.append([n+1,delivered_at])
    else:
        inserted = False
        for i in range(len(when_delivered)):
            if delivered_at > when_delivered[i][1]:
                continue
            elif delivered_at == when_delivered[i][1]:
                to_insert_at = i
                while n+1 > when_delivered[to_insert_at][0] and \
                delivered_at == when_delivered[to_insert_at][1]:
                    to_insert_at +=1
                    if to_insert_at == len(when_delivered):
                        break

                when_delivered.insert(to_insert_at,[n+1,delivered_at])
                inserted = True
                break

            elif delivered_at < when_delivered[i][1]:
                when_delivered.insert(i,[n+1,delivered_at])
                inserted = True
                break

        if not inserted:
            when_delivered.append([n+1,delivered_at]) #if its never inserted, stick it at the end

for i in range(len(when_delivered)):
    print(when_delivered[i][0], end=' ')
```
