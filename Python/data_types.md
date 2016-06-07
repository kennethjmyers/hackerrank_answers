# Introduction

## [Lists](https://www.hackerrank.com/challenges/python-lists)

```
N = int(input())
arr = []
for _ in range(N):
    action = input().strip().split()
    if action[0] == 'insert':
        arr.insert(int(action[1]),int(action[2]))
    elif action[0] == 'append':
        arr.append(int(action[1]))
    elif action[0] == 'sort':
        arr.sort()
    elif action[0] == 'remove':
        arr.remove(int(action[1]))
    elif action[0] == 'pop':
        arr.pop()
    elif action[0] == 'reverse':
        arr = arr[::-1]
    elif action[0] == 'print':
        print(arr)
```

## [Tuples](https://www.hackerrank.com/challenges/python-tuples)

```
N = int(input())
print(hash(tuple([int(i) for i in input().strip().split()])))
```

## [Sets - Symmetric Difference](https://www.hackerrank.com/challenges/sets)

```
M = int(input())
s1 = set(input().strip().split())
N = int(input())
s2 = set(input().strip().split())

print(*sorted([int(i) for i in ((s1-s2)|(s2-s1))]), sep='\n')
```

## [List Comprehensions](https://www.hackerrank.com/challenges/list-comprehensions)

```
X = int(input())
Y = int(input())
Z = int(input())
N = int(input())
print([[i,j,k] for i in range(X+1) for j in range(Y+1) for k in range(Z+1) if sum([i,j,k]) != N])
```

## [Find the Second Largest Number](https://www.hackerrank.com/challenges/find-second-maximum-number-in-a-list)

```
N = int(input())
arr = [int(i) for i in input().strip().split()]
maxes = [-9999,-9999]
for i in arr:
    if i > maxes[1]:
        maxes[0], maxes[1] = maxes[1], i
    elif i > maxes[0] and i != maxes[1]:
        maxes[0] = i

print(maxes[0])
```

## [Nested Lists](https://www.hackerrank.com/challenges/nested-list)

```
N = int(input())
arr = []
for _ in range(N):
    arr.append([input(),float(input())])

arr = sorted(arr, key=lambda x:x[1])
lowest = arr[0][1]
new_arr = []
for i in arr:
    if i[1] != lowest:
        if new_arr and i[1]!=second_lowest:
            break
        new_arr.append(i[0])
        second_lowest = i[1]
print(*sorted(new_arr), sep='\n')
```
