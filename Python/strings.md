# Introduction

## [sWAP cASE](https://www.hackerrank.com/challenges/swap-case)

```
def swap_case(s):
    if s.islower():
        return s.upper()
    return s.lower()

print(''.join(list(map(swap_case,list(input().strip())))))
```

## [String Split and Join](https://www.hackerrank.com/challenges/python-string-split-and-join)

```
print('-'.join(input().strip().split()))
```

## [Mutations](https://www.hackerrank.com/challenges/python-mutations)

```
arr = list(input().strip())
a = input().strip().split()
arr[int(a[0])] = a[1]
print(''.join(arr))
```

## [Find a String](https://www.hackerrank.com/challenges/find-a-string)

```
s1 = input()
s2 = input()
count = 0
for i in range(len(s1)-len(s2)+1):
    if s1[i:i+len(s2)] == s2:
        count+=1
print(count)
```

## [String Validators](https://www.hackerrank.com/challenges/string-validators)

```
s = list(input())
d = {'alnum':False,'alpha':False,'digit':False,'lower':False,'upper':False}
for x in s:
    if x.isalnum():
        d['alnum'] = True
    if x.isalpha():
        d['alpha'] = True
    if x.isdigit():
        d['digit'] = True
    if x.islower():
        d['lower'] = True
    if x.isupper():
        d['upper'] = True

for i in ['alnum','alpha','digit','lower','upper']:
    print(d[i])
```
