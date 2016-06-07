# Introduction

## [Say "Hello, World!" With Python](https://www.hackerrank.com/challenges/py-hello-world)

```
print('Hello, World!')
```

## [Raw Input](https://www.hackerrank.com/challenges/python-raw-input)

```
print(input())
```

## [Arithmetic Operators](https://www.hackerrank.com/challenges/python-arithmetic-operators)

```
a = int(input())
b = int(input())
print(a+b)
print(a-b)
print(a*b)
```

## [Python: Division](https://www.hackerrank.com/challenges/python-division)

```
from __future__ import division

a = int(input())
b = int(input())
print(a//b)
print(a/b)
```

## [Mod Divmod](https://www.hackerrank.com/challenges/python-mod-divmod)

```
a = int(input())
b = int(input())
print(a//b)
print(a%b)
print('({}, {})'.format(a//b,a%b))
```

## [Power - Mod Power](https://www.hackerrank.com/challenges/python-power-mod-power)

```
a = int(input())
b = int(input())
m = int(input())
print('{}\n{}'.format(pow(a,b),pow(a,b,m)))
```

## [Integers Come In All Sizes](https://www.hackerrank.com/challenges/python-integers-come-in-all-sizes)

```
a = int(input())
b = int(input())
c = int(input())
d = int(input())

print(a**b+c**d)
```

## [Loops](https://www.hackerrank.com/challenges/python-loops)

```
N = int(input())
for i in range(N):
    print(i**2)
```

## [What's Your Name?](https://www.hackerrank.com/challenges/whats-your-name)

```
print('Hello {} {}! You just delved into python.'.format(input(),input()))
```

## [Interchange Two Numbers](https://www.hackerrank.com/challenges/interchange-two-numbers)

```
a = tuple([int(input()),int(input())])
print('{}\n{}'.format(a[1],a[0]))
```

## [Finding the Percentage](https://www.hackerrank.com/challenges/finding-the-percentage)

```
N = int(input())
avgs = {}
for _ in range(N):
    arr = input().strip().split()
    name = arr[0]
    grades = [float(i) for i in arr[1:]]
    avgs[name] = sum(grades)/len(grades)

print("{0:.2f}".format(avgs[input()]))
```

## [Print Function](https://www.hackerrank.com/challenges/python-print)

```
print(*range(1,int(input())+1), sep='',end='')
```
