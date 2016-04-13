# Implementation exercises (python3)

## Angry Professor

```
#!/bin/python3

import sys


t = int(input().strip())
for a0 in range(t):
    n,k = input().strip().split(' ')
    n,k = [int(n),int(k)]
    a = [int(a_temp) for a_temp in input().strip().split(' ')]

    ontime = 0
    for i in a:
        if i <= 0:
            ontime +=1
    if ontime < k:
        print('YES')
    else:
        print('NO')
```

## Sherlock and the Beast

```
#!/bin/python3

import sys


t = int(input().strip())
for a0 in range(t):
    n = int(input().strip())
    dm = divmod(n,3)
    if dm[1] == 2:
        for _ in range(dm[0]-1):
            print(555,end='')
        if dm[0] > 0:
            print(33333)
        else:
            print(-1)
    elif dm[0] >= 3 and dm[1] == 1:
        for _ in range(dm[0]-3):
            print(555,end='')
        print(3333333333)
    elif dm[1] == 0:
        for _ in range(dm[0]):
            print(555,end='')
        print()
    else:
        print(-1)
```

## Utopian Trees

```
#!/bin/python3

import sys


t = int(input().strip())
for a0 in range(t):
    n = int(input().strip())
    num = 1
    for i in range(n):
        if i % 2 == 0:
            num *= 2
        else:
            num +=1
    print(num)
```

## Find Digits

```
#!/bin/python3

import sys


t = int(input().strip())
for a0 in range(t):
    n = int(input().strip())
    count = 0
    n_copy = n
    while n_copy != 0:
        digit = n_copy%10
        try:
            if n%digit == 0:
                count += 1
        except:
            pass
        n_copy//=10
    print(count)
```

## Sherlock and squares

```
#!/bin/python3

import sys
from math import sqrt,ceil,floor

t = int(input().strip())
for a0 in range(t):
    a,b = input().strip().split()
    a,b = int(a),int(b)
    sqa = ceil(sqrt(a))
    sqb = floor(sqrt(b))
    print(sqb-sqa+1)
```

## Service Lane

```
#!/bin/python3

import sys


n,t = input().strip().split(' ')
n,t = [int(n),int(t)]
width = [int(width_temp) for width_temp in input().strip().split(' ')]
for a0 in range(t):
    i,j = input().strip().split(' ')
    i,j = [int(i),int(j)]
    print(min(width[i:j+1]))
```

## Cut the sticks

```
#!/bin/python3

import sys


n = int(input().strip())
arr = [int(arr_temp) for arr_temp in input().strip().split(' ')]

while arr:
    print(len(arr))
    minima = min(arr)
    arr = [i-minima for i in arr if i-minima > 0]
```

## Chocolate Feast

```
#!/bin/python3

import sys


t = int(input().strip())
for a0 in range(t):
    n,c,m = input().strip().split(' ')
    n,c,m = [int(n),int(c),int(m)]

    total_bars = n//c
    wrappers = total_bars
    while wrappers >= m:
        extra_bars = wrappers//m
        total_bars += extra_bars
        wrappers %= m
        wrappers += extra_bars
    print(total_bars)
```

## Lisas workbook


```

```
