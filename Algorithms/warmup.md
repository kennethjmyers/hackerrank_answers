# Warm up exercises (python3)

## Solve me first

```
def solveMeFirst(a,b):
    return a + b


num1 = int(input())
num2 = int(input())
res = solveMeFirst(num1,num2)
print(res)
```

## Simple Array Sum

```
#!/bin/python3

import sys


n = int(input().strip())
arr = [int(arr_temp) for arr_temp in input().strip().split(' ')]
print(sum(arr))
```

## A very big sum

```
#!/bin/python3

import sys


n = int(input().strip())
arr = [int(arr_temp) for arr_temp in input().strip().split(' ')]
print(sum(arr))
```

## Diagonal Difference

```
#!/bin/python3

import sys


n = int(input().strip())
a = []
for a_i in range(n):
   a_t = [int(a_temp) for a_temp in input().strip().split(' ')]
   a.append(a_t)

fw = sum((a[i][i] for i in range(len(a))))
bw = []
for i in range(len(a)):
    try:
        bw.append(a[i][len(a)-1-i])
    except:
        pass
bw = sum(bw)
print(abs(fw-bw))
```

## Plus Minus

```
#!/bin/python3

import sys


n = int(input().strip())
arr = [int(arr_temp) for arr_temp in input().strip().split(' ')]
pos = 0
neg = 0
zer = 0
len_arr = len(arr)
for i in arr:
    if i > 0:
        pos += 1
    elif i == 0:
        zer += 1
    else:
        neg += 1

print(pos/len_arr)
print(neg/len_arr)
print(zer/len_arr)
```

## Staircase

```
#!/bin/python3

import sys


n = int(input().strip())
for i in range(n):
    print(' '*(n-1-i),end='')
    print('#'*(i+1),end='')
    print()
```

## Time Conversion

```
#!/bin/python3

import sys


time = input().strip()
if time[-2:] == 'PM':
    if time[:2] == '12':
        print('12'+time[2:-2])
    else:
        print(str(int(time[:2])+12)+time[2:-2])
else:
    if time[:2] == '12':
        print('00'+time[2:-2])
    else:
        print(time[:-2])
```
