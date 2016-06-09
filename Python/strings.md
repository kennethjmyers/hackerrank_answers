# Strings

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

## [Text Alignment](https://www.hackerrank.com/challenges/text-alignment)

```
#Replace all ______ with rjust, ljust or center.

thickness = int(input()) #This must be an odd number
c = 'H'

#Top Cone
for i in range(thickness):
    print((c*i).rjust(thickness-1)+c+(c*i).ljust(thickness-1))

#Top Pillars
for i in range(thickness+1):
    print((c*thickness).center(thickness*2)+(c*thickness).center(thickness*6))

#Middle Belt
for i in range((thickness+1)//2):
    print((c*thickness*5).center(thickness*6))    

#Bottom Pillars
for i in range(thickness+1):
    print((c*thickness).center(thickness*2)+(c*thickness).center(thickness*6))    

#Bottom Cone
for i in range(thickness):
    print(((c*(thickness-i-1)).rjust(thickness)+c+(c*(thickness-i-1)).ljust(thickness)).rjust(thickness*6))  
```

## [Text Wrap](https://www.hackerrank.com/challenges/text-wrap)

```
s = input()
n = int(input())

for i in range(len(s)):
    print(s[i], end='')
    if (i+1)%n == 0:
        print('')
```

## [Designer Door Mat](https://www.hackerrank.com/challenges/designer-door-mat)

```
N, M = map(int,input().split()) # More than 6 lines of code will result in 0 score. Blank lines are not counted.
for i in range(1,N,2):
    print(('.|.'*i).center(M,'-'))
print('WELCOME'.center(M,'-'))
for i in range(N-2,-1,-2):
    print(('.|.'*i).center(M,'-'))
```

## [String Formatting](https://www.hackerrank.com/challenges/python-string-formatting)

```
N = int(input())

w = len(bin(N)[2:])
for i in range(1,N+1):
    print(str(i).rjust(w), end=' ')
    print(oct(i)[2:].rjust(w), end=' ')
    print(hex(i)[2:].upper().rjust(w), end=' ')
    print(bin(i)[2:].rjust(w))
```

## [Alphabet Rangoli](https://www.hackerrank.com/challenges/alphabet-rangoli)

```
N = int(input())

w = N+N-1 + (N+N-1)-1
for i in range(0,N,1):
    line = '-'.join([chr(97+N-1-abs(j)) for j in (list(range(0,i+1))+list(range(-i+1,1)))])
    print(line.center(w,'-'))
for i in range(N-2,-1,-1):
    line = '-'.join([chr(97+N-1-j) for j in (list(range(0,i))+list(range(i,-1,-1)))])
    print(line.center(w,'-'))
```

## [Capitalize](https://www.hackerrank.com/challenges/capitalize)

```
s = input()
print(''.join([x.upper() if i == 0 else x.upper() if not s[i-1].isalnum() else x for i,x in enumerate(s)]))
```

## [The Minion Game](https://www.hackerrank.com/challenges/the-minion-game)

```
S = input()
stuart = 0
kevin = 0
vowels = {'A','E','I','O','U'}

for i,s in enumerate(S):
    if s in vowels:
        kevin += len(S)-i
    else:
        stuart += len(S)-i

if kevin > stuart:
    print('Kevin',kevin)
elif stuart > kevin:
    print('Stuart',stuart)
else:
    print('Draw')
```
