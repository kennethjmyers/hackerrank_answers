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

This was a fix the code problem
```
def insertion_sort(l):
    for i in range(1, len(l)):
        j = i-1
        key = l[i]
        while (j >= 0) and (l[j] > key):
           l[j+1] = l[j]
           j -= 1
        l[j+1] = key


m = int(input().strip())
ar = [int(i) for i in input().strip().split()]
insertion_sort(ar)
print(" ".join(map(str,ar)))
```

## Running Time of Algorithms

```
def shifts_count(l):
    shifts = 0
    for i in range(1, len(l)):
        j = i-1
        key = l[i]
        while (j >= 0) and (l[j] > key):
           l[j+1] = l[j]
           shifts +=1
           j -= 1
        l[j+1] = key
    return shifts


m = int(input().strip())
ar = [int(i) for i in input().strip().split()]
print(shifts_count(ar))
```

## Quicksort 1 - Partition

```
N = int(input().strip())

arr = [int(i) for i in input().strip().split()]

p = arr[0]
left,equal,right = [],[],[]

for i in arr:
    if i < p:
        left.append(i)
    elif i == p:
        equal.append(i)
    else:
        right.append(i)

print(' '.join([str(i) for i in left+equal+right]))
```

## Quicksort 2 - Sorting

```
N = int(input().strip())

arr = [int(i) for i in input().strip().split()]

def quicksort(arr):
    if not arr:
        return []
    p = arr[0]
    left,equal,right = [],[],[]
    for i in arr:
        if i < p:
            left.append(i)
        elif i == p:
            equal.append(i)
        else:
            right.append(i)
    # this if/else statement is necessary for this challenge
    # but not for quicksort (more print statements without it)
    if not left and not right:
        return equal
    else:
        result = quicksort(left)+equal+quicksort(right)
        print(' '.join([str(i) for i in result]))
        return result

quicksort(arr)
```

## Quicksort In-Place

Used the Lomuto partition [algorithm here](https://en.wikipedia.org/wiki/Quicksort#Algorithm)
```
def partition(arr,low_index,high_index):
    p = arr[high_index]
    i = low_index
    for j in range(low_index,high_index):
        if arr[j] <= p:
            arr[j],arr[i] = arr[i],arr[j]
            i+=1
    arr[high_index],arr[i] = arr[i],arr[high_index]
    print(' '.join([str(i) for i in arr]))
    return i

def quicksort(arr,low_index,high_index):
    if low_index < high_index:
        p = partition(arr,low_index,high_index)
        quicksort(arr,low_index,p-1)
        quicksort(arr,p+1,high_index)

N = int(input().strip())

arr = [int(i) for i in input().strip().split()]
quicksort(arr,0,len(arr)-1)
```

## Bigger is Greater

This [link helps](https://www.nayuki.io/page/next-lexicographical-permutation-algorithm)
```
from copy import deepcopy

N = int(input().strip())

def get_string(S_in):
    S = deepcopy(S_in)
    if len(S) == 1:
        return 'no answer'
    last = S[-1]
    second_to_last = S[-2]
    if last > second_to_last: #if last > next to last then swap
        S[-1],S[-2] = S[-2],S[-1]
        return ''.join(S)
    else:
        pivot = 1
        for i in range(-2,-len(S)-1,-1): #loop to find pivot
            if S[i] < S[i+1]:
                pivot = i
                break

        if pivot == 1: # if no pivot value could be found then no answer
            return 'no answer'

        for i in range(pivot+1,0,1): #loop to find next nearest
            if S[i+1] <= S[pivot] or i == -1:
                S[pivot],S[i] = S[i],S[pivot]
                break

        for i in range(-1,(pivot-1)//2,-1): #swap values in the descending suffix
            #print(S)
            S[i],S[pivot-i] = S[pivot-i],S[i]
        #print(S)
        return ''.join(S)



for _ in range(N):
    S_in = list(input().strip())
    result = get_string(S_in)
    if result == ''.join(S_in):
        print('no answer')
    else:
        print(result)
```

## [Running Time of Quicksort](https://www.hackerrank.com/challenges/quicksort4)

```
from copy import deepcopy

#Insertion sort
def insertion_shifts_count(l):
    shifts = 0
    for i in range(1, len(l)):
        j = i-1
        key = l[i]
        while (j >= 0) and (l[j] > key):
           l[j+1] = l[j]
           shifts +=1
           j -= 1
        l[j+1] = key
    return shifts

#Quick sort
quick_sort_shifts = 0
def partition(arr,low_index,high_index):
    global quick_sort_shifts
    p = arr[high_index]
    i = low_index
    for j in range(low_index,high_index):
        if arr[j] <= p:
            arr[j],arr[i] = arr[i],arr[j]
            quick_sort_shifts+=1
            i+=1
    arr[high_index],arr[i] = arr[i],arr[high_index]
    quick_sort_shifts+=1
    #print(' '.join([str(i) for i in arr]))
    return i

def quicksort(arr,low_index,high_index,top_level=True):
    global quick_sort_shifts
    if top_level:
        quick_sort_shifts = 0
    if low_index < high_index:
        p = partition(arr,low_index,high_index)
        quicksort(arr,low_index,p-1,False)
        quicksort(arr,p+1,high_index,False)
    return quick_sort_shifts

N = int(input().strip())

arr = [int(i) for i in input().strip().split()]
arr1,arr2 = deepcopy(arr),deepcopy(arr)
i_count = insertion_shifts_count(arr1)
q_count = quicksort(arr2,0,len(arr)-1)
print(i_count-q_count)
```

## [Counting Sort 1](https://www.hackerrank.com/challenges/countingsort1)

```
from collections import Counter

N = int(input().strip())

arr = [int(i) for i in input().strip().split()]
c = Counter(arr)
for i in range(100):
    print(c[i], end=' ')
```

## [Counting Sort 2](https://www.hackerrank.com/challenges/countingsort2)

```
from collections import Counter

N = int(input().strip())

arr = [int(i) for i in input().strip().split()]
c = Counter(arr)
for k,v in c.items():
    for i in range(v):
        print(k,end=' ')
```

## [Counting Sort 3](https://www.hackerrank.com/challenges/countingsort3)

```
T = int(input().strip())

arr = [0]*100
for _ in range(T):
    num = int(input().strip().split()[0])
    for i in range(num,100):
        arr[i]+=1

print(' '.join([str(i) for i in arr]))
```

## [Full Counting Sort](https://www.hackerrank.com/challenges/countingsort4)

```
from collections import defaultdict
from math import ceil


T = int(input().strip())

c = defaultdict(list)
for i in range(T):
    j,s = input().strip().split()
    if i < ceil(T/2):
        c[int(j)].append('-')
    else:
        c[int(j)].append(s)

for k,v in c.items():
    for l in v:
        print(l,end=' ')
```

## [Closest Numbers](https://www.hackerrank.com/challenges/closest-numbers)

```
N = int(input().strip())

arr = [int(i) for i in input().strip().split()]

arr = sorted(arr)

max_d = 1000000000000000
pairs = []
for i in range(1,len(arr)):
    if abs(arr[i]-arr[i-1])<max_d:
        pairs = []
        pairs.append([arr[i-1],arr[i]])
        max_d = abs(arr[i]-arr[i-1])
    elif abs(arr[i]-arr[i-1])==max_d:
        pairs.append([arr[i-1],arr[i]])
    else:
        continue

for i in pairs:
    print(' '.join([str(x) for x in i]), end=' ')
```

## [Find the Median](https://www.hackerrank.com/challenges/find-median)

```
N = int(input().strip())

arr = sorted([int(i) for i in input().strip().split()])

print(arr[N//2])
```

## [Sherlock and Watson](https://www.hackerrank.com/challenges/sherlock-and-watson)

```
N,K,Q = [int(i) for i in input().strip().split()]

arr = [int(i) for i in input().strip().split()]

for i in range(K):
    arr.insert(0,arr.pop())

for _ in range(Q):
    num = int(input().strip())
    print(arr[num])
```

## [Almost Sorted](https://www.hackerrank.com/challenges/almost-sorted)

```
N = int(input().strip())

arr = [int(i) for i in input().strip().split()]

is_sorted = True
can_be_sorted = True

arr.insert(0,-1)
arr.append(10000001)

hills = 0
h = []
dips = 0
d = []
for i in range(1,N+1):
    if arr[i-1] > arr[i] < arr[i+1]:
        d.append(i)
        dips += 1
    elif arr[i-1] < arr[i] > arr[i+1]:
        h.append(i)
        hills += 1

if hills == dips == 0:
    print('yes')
elif hills == dips == 2:
    if h[0]!=d[0]-1 or h[1]!=d[1]-1:
        print('no')
    else:
        l = h[0]
        r = d[1]
        arr[l],arr[r] = arr[r],arr[l]
        if arr[l+1]>arr[l]>arr[l-1] and arr[r-1]<arr[r]<arr[r+1]:
            print('yes')
            print('swap',l,r)
elif hills == dips == 1:
    l = h[0]
    r = d[0]
    if r == l+1:
        if arr[r]<arr[l-1] or arr[l]>arr[r+1]:
            print('no')  
        else:
            print('yes')
            print('swap',l,r)
    elif arr[l+1]>arr[r]>arr[l-1] and arr[r-1]<arr[l]<arr[r+1]:
        print('yes')
        print('reverse',l,r)
else:
    print('no')
```

## [Sherlock and Pairs](https://www.hackerrank.com/challenges/sherlock-and-pairs)

```
#P = n!/(n-k)!

from math import factorial
from collections import Counter

def f(n):
    return factorial(n)

def nPr(n,r):
    return int(f(n)/f(n-r))

T = int(input().strip())

for _ in range(T):
    N = int(input().strip())
    arr = [int(i) for i in input().strip().split()]
    c = Counter(arr)
    total = 0
    for k,v in c.items():
        if v >= 2:
            total+=nPr(v,2)

    print(total)
```

## [Insertion Sort Advanced Analysis](https://www.hackerrank.com/challenges/insertion-sort)

[Helpful link](https://sadakurapati.wordpress.com/2013/10/11/insertion-sort-counting-element-swaps/) (see approach 3)
```

```
