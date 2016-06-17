# Sets

## [Introduction to Sets](https://www.hackerrank.com/challenges/py-introduction-to-sets)

```
N = int(input())
heights = set([int(i) for i in input().strip().split()])
print(sum(heights)/len(heights))
```

## [No Idea!](https://www.hackerrank.com/challenges/no-idea)

```
n,m = [int(i) for i in input().strip().split()]
arr = [int(i) for i in input().strip().split()]
A = set([int(i) for i in input().strip().split()])
B = set([int(i) for i in input().strip().split()])

h = 0    
for i in arr:
    if i in A:
        h+=1
    if i in B:
        h-=1

print(h)
```

## [Set.add()](https://www.hackerrank.com/challenges/py-set-add)

```
n = int(input())
s = set()
for _ in range(n):
    s.add(input())

print(len(s))
```

## [Set .discard(), .remove() & .pop()](https://www.hackerrank.com/challenges/py-set-discard-remove-pop)

```
def act(s, action, val=None):
    '''
    >>> act({1,2,3,4},'discard',4)
    {1, 2, 3}
    '''
    if action == 'pop':
        s.pop()
    elif action == 'discard':
        s.discard(val)
    elif action == 'remove':
        s.remove(val)
    return s


if __name__ == '__main__':
    import doctest
    doctest.testmod()

    n = int(input())
    s = set(map(int, input().split()))
    N = int(input())

    for _ in range(N):
        act_val = input().split()
        if act_val[0] == 'pop':
            s = act(s, 'pop')
        else:
            s = act(s, act_val[0], int(act_val[1]))

    print(sum(s))
```

## [Set .union() Operation](https://www.hackerrank.com/challenges/py-set-union)

```
n = int(input())
arr1 = set([int(i) for i in input().split()])
b = int(input())
arr2 = set([int(i) for i in input().split()])

print(len(arr1.union(arr2)))
```

## [Set .intersection() Operation](https://www.hackerrank.com/challenges/py-set-intersection-operation)

```
n = int(input())
arr1 = set([int(i) for i in input().split()])
b = int(input())
arr2 = set([int(i) for i in input().split()])

print(len(arr1&arr2))
```
