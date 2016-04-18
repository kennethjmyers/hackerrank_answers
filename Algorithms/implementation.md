# Implementation Exercises (python3)

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
from math import ceil


n,k = input().strip().split()
n,k = int(n),int(k)
t_arr = input().strip().split()
t_arr = [int(i) for i in t_arr]

page = 1
count = 0
for ti in t_arr:
    problems_by_page = [[j for j in range(i*k+1,min(ti+1,i*k+k+1))] for i in range(ceil(ti/k))]
    for problems in problems_by_page:
        if page in problems:
            count += 1
        page +=1

print(count)
```

## The Grid Search

```
#!/bin/python3

import sys


t = int(input().strip())
for a0 in range(t):
    R,C = input().strip().split(' ')
    R,C = [int(R),int(C)]
    G = []
    G_i = 0
    for G_i in range(R):
       G_t = str(input().strip())
       G.append(G_t)
    r,c = input().strip().split(' ')
    r,c = [int(r),int(c)]
    P = []
    P_i = 0
    for P_i in range(r):
       P_t = str(input().strip())
       P.append(P_t)

    check = False
    for i in range(R-r+1):
        if G[i].find(P[0],0)==-1:
            continue
        else:
            for j in range(C-c+1):
                if P == [x[j:j+c] for x in G[i:i+r]]:
                    check = True
                    break
        if check == True:
            break
    if check == True:
        print('YES')
    else:
        print('NO')
```

## Cavity Map

```
#!/bin/python3

import sys


n = int(input().strip())
grid = []
grid_i = 0
for grid_i in range(n):
   grid_t = str(input().strip())
   grid.append(grid_t)

for i in range(1,n-1):
    for j in range(1,n-1):
        if (grid[i][j] > grid[i][j+1] and\
        grid[i][j] > grid[i][j-1] and\
        grid[i][j] > grid[i+1][j] and\
        grid[i][j] > grid[i-1][j]) and\
        'X' not in [grid[i-1][j],grid[i+1][j],grid[i][j-1],grid[i][j+1]]:
            grid[i] = grid[i][:j]+'X'+grid[i][j+1:]

for row in grid:
    print(row)
```

## Caesar Cipher

```
#!/bin/python3

import sys


n = int(input().strip())
s = input().strip()
k = int(input().strip())

result = []
for i in s:
    if not i.isalpha():
        result.append(i)
        continue
    if i.islower():
        result.append(chr(((ord(i)-97)+k)%26+97))
    else:
        result.append(chr(((ord(i)-65)+k)%26+65))
print(''.join(result))
```

## Library Fine

```
#!/bin/python3

import sys


d1,m1,y1 = input().strip().split(' ')
d1,m1,y1 = [int(d1),int(m1),int(y1)]
d2,m2,y2 = input().strip().split(' ')
d2,m2,y2 = [int(d2),int(m2),int(y2)]

if y1 < y2:
    print(0)
elif y1 > y2:
    print(10000)
else:
    if m1 > m2:
        print(500*(m1-m2))
    elif m1 < m2:
        print(0)
    else:
        if d1>d2:
            print(15*(d1-d2))
        elif d1 <= d2:
            print(0)
```

## Manasa and Stones

```
t = int(input().strip())

for _ in range(t):
    n = int(input().strip())
    a = int(input().strip())
    b = int(input().strip())

    solutions = []
    for i in range(n):
        solutions.append(a*i+b*(n-1-i))

    solutions = sorted(list(set(solutions)))
    for i in solutions:
        print(i,end=' ')
    print()
```

## ACM ICPC Team

```
#!/bin/python3

import sys


n,m = input().strip().split(' ')
n,m = [int(n),int(m)]
topic = []
topic_i = 0
for topic_i in range(n):
   topic_t = str(input().strip())
   topic.append(topic_t)

bin_class = []
max_topics = 0
teams_w_max = 0
for t in topic:
    bin_class.append(int(t,2))

for i,x in enumerate(bin_class):
    for y in bin_class[i+1:]:
        b = bin(x|y)
        count = b.count('1')
        if count > max_topics:
            max_topics = count
            teams_w_max = 1
        elif count == max_topics:
            teams_w_max += 1

print(max_topics)
print(teams_w_max)
```

## Extra Long Factorials

```
n = int(input().strip())

from math import factorial

print(factorial(n))
```

## Taum and B'day

```
#!/bin/python3

import sys


t = int(input().strip())
for a0 in range(t):
    b,w = input().strip().split(' ')
    b,w = [int(b),int(w)]
    x,y,z = input().strip().split(' ')
    x,y,z = [int(x),int(y),int(z)]

    if z+x < y:
        print((w+b)*x + w*z)
    elif z+y < x:
        print((w+b)*y + b*z)
    else:
        print(b*x+w*y)
```

## The Time in Words

```
#!/bin/python3

import sys


h = int(input().strip())
m = input().strip()
m1,m2 = int(m[0])*10,int(m[1])
m = int(m)

num_dict = {0:'',1:'one',2:'two',3:'three',4:'four',\
            5:'five',6:'six',7:'seven',8:'eight',\
             9:'nine',10:'ten',11:'eleven',12:'twelve',\
            13:'thirteen',14:'fourteen',15:'quarter',16:'sixteen',\
            17:'seventeen',18:'eighteen',19:'nineteen',\
            20:'twenty', 30:'half'}

if m == 0:
    print(num_dict[h],'o\' clock')

elif m == 1 or m == 59:
    if m == 1:
        print('one minute past', num_dict[h])
    else:
        print('one minute to', num_dict[(h+1)%13])

elif m == 30:
    print('half past', num_dict[h])

elif m == 15:
    print('quarter past', num_dict[h])
elif m == 45:
    print('quarter to', num_dict[(h+1)%13])
elif m < 30:
    if m <= 20:
        print(num_dict[m2],'minutes past',num_dict[h])
    elif m > 20:
        print(num_dict[m1], num_dict[m2], 'minutes past', num_dict[h])
else:
    if m < 40:
        print(num_dict[m1-10], num_dict[10-m2], 'minutes to', num_dict[(h+1)%13])
    else:
        print(num_dict[60-m], 'minutes to', num_dict[(h+1)%13])
```

## Modified Kaprekar Numbers

```
p = int(input().strip())
q = int(input().strip())

kap_nums = []
found = False
for i in range(p, q+1):
    num = i**2
    r_digits = 1
    r = 0
    while num > 0:
        r += 10**(r_digits-1) * (num%10)
        num //= 10
        r_digits +=1
        if r == 0:
            continue
        if num + r == i:
            num2 = num
            l_digits = 1
            while num2 > 0:
                num2 //= 10
                l_digits += 1
            #check to make sure left and right digits are equal or 1 less on left
            if l_digits == r_digits or l_digits == r_digits - 1:
                print(i,end=' ')
                found = True
                break
            elif r_digits - l_digits >= 2:
                break
if not found:
    print('INVALID RANGE')
```

## Encryption

```
from math import ceil,floor,sqrt


s = input().strip()

l = len(s)
sqrtl = sqrt(l)
ul = ceil(sqrtl)
ll = floor(sqrtl)
if ul*ll < l:
    r = c =ul
elif ul*ul == l:
    r = c = ul
elif ll*ll == l:
    r = c = ll
else:
    r = ll
    c = ul

first_grid = [[ch for j,ch in enumerate(s) if j//c == i] for i in range(r)]

for i in range(c):
    for j in range(r):
        if j != r-1:
            print(first_grid[j][i],end='')
        else:
            try:
                print(first_grid[j][i],end=' ')
            except:
                print(' ',end='')
```

## Larrys Array

Further reading on this question:
[Parity of a Permutation](https://en.wikipedia.org/wiki/Parity_of_a_permutation)
[http://www.math.ubc.ca/~cass/courses/m308-02b/projects/grant/fifteen.html]
[The 15 puzzle problem]()
```
#parity checker taken from http://code.activestate.com/recipes/578227-generate-the-parity-or-sign-of-a-permutation/

T = int(input().strip())

for _ in range(T):
    N = int(input().strip())
    arr = list(map(int,input().strip().split()))

    s_arr = sorted(arr)

    parity = 1
    for i in range(0,len(arr)-1):
        if arr[i] != s_arr[i]:
            parity *= -1
            mn = min(range(i,len(arr)), key=arr.__getitem__)
            arr[i],arr[mn] = arr[mn],arr[i]
    if parity == 1:
        print('YES')
    else:
        print('NO')
```

## [Algo] Matrix Rotation

```

```
