# Sorting

## Intro to tutorial challenges

There didn't seem to be rules saying you can't use builtin functions.
```
V = int(input().strip())
N = int(input().strip())
arr = list(map(int,input().strip().split()))

print(arr.index(V))
```

## Insertion Sort Part 1

```
S = int(input().strip())

arr = list(map(int,input().strip().split()))

unsort_elem = arr[-1]
for i in range(-2,-len(arr)-1,-1):
    arr[i+1] = arr[i]
    print(' '.join(list(map(str,arr))))
    if i == -len(arr):
        arr[i] = unsort_elem
        print(' '.join(list(map(str,arr))))
    elif unsort_elem < arr[i] and unsort_elem > arr[i-1]:
        arr[i] = unsort_elem
        print(' '.join(list(map(str,arr))))
        break
```

## Insertion Sort Part 2

```
S = int(input().strip())

arr = list(map(int,input().strip().split()))

sorted_part = arr[0:1]
unsorted_part = arr[1:]

for _ in range(len(arr)-1):
    sorted_part.append(unsorted_part.pop(0))
    x = sorted_part[-1]
    if x > sorted_part[-2]:
        print(' '.join(list(map(str,sorted_part+unsorted_part))))
        continue
    for i in range(-2,-len(sorted_part)-1,-1):
        sorted_part[i+1] = sorted_part[i]
        if i == -len(sorted_part):
            sorted_part[i] = x
            print(' '.join(list(map(str,sorted_part+unsorted_part))))
        elif x < sorted_part[i] and x > sorted_part[i-1]:
            sorted_part[i] = x
            print(' '.join(list(map(str,sorted_part+unsorted_part))))
            break
```

## Correctness and Loop Invariant

```

```

## 
