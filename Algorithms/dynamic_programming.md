# Dynamic Programming Exercises (python3)

## Fibonacci Modified

```
arr = input().split()
a,b,n = [int(i) for i in arr]

for _ in range(n-2):
    a,b = b,a+b**2

print(b)
```

## The Maximum Subarray

```
t = int(input().strip())
for a0 in range(t):
    T = int(input().strip())
    arr = input().strip().split()
    arr = [int(i) for i in arr]

    if arr[0] >= 0:
        max_non_cont = arr[0]
    else:
        max_non_cont = 0
    max_ending_here = max_so_far = max_arr = arr[0]
    for x in arr[1:]:
        max_ending_here = max(x, max_ending_here+x)
        max_so_far = max(max_so_far,max_ending_here)
        if x >= 0:
            max_non_cont += x
        if x > max_arr:
            max_arr = x

    #check for an array with all negative values
    if max_arr < 0:
        max_non_cont = max_arr

    print(str(max_so_far)+' '+str(max_non_cont))
```

## The coin change problem

First attempt (bad for large amounts of coins)
```
n,m = input().strip().split()
n,m = int(n),int(m)
C = input().strip().split()
C = sorted([int(i) for i in C])

count = 0
options = [[0]*n]
for c in C:
    new_options = []
    for option in options:
        last = option
        while last[:c] == [0]*c:
            last = last[c:]+[c]
            if last[0] != 0:
                count +=1
            new_options.append(last)
    options.extend(new_options)

print(count)
```

Second attempt:
```
n,m = input().strip().split()
n,m = int(n),int(m)
C = input().strip().split()
C = sorted([int(i) for i in C])

def get_count(total,coins):
    total_combinations = [1]+[0]*total
    for coin in coins:
        for i in range(coin,total+1):
            total_combinations[i] += total_combinations[i-coin]
    return total_combinations[total]

print(get_count(n,C))
```

## Candies

```
n = int(input().strip())
arr = []
for _ in range(n):
    arr.append(int(input().strip()))

candies = [1]*n
desc = 0 #this is a counter for the number of consecutive descending elements
for i in range(1,n):
    if arr[i] >= arr[i-1]:
        desc = 0 # reset the descender if same value or increasing
    #increment by previous persons candies if this persons score is greater
    if arr[i] > arr[i-1]:
        candies[i] += candies[i-1]

    #if the array starts descending then you have to go back and
    #increment all of the previous descending elements
    #sorry this section is so illegible, I kept running into
    #different cases where things would fail (ie 1,2,3,4,3,2,1 vs 1,2,3,4,4,3,2,1)
    elif arr[i] < arr[i-1]:
        desc+=1
        #increment the previous if both values are equal
        if desc == 1 and candies[i] == candies[i-1]:
            candies[i-1] += 1
        #do nothing if first descent and not equal
        elif desc == 1:
            pass
        else:
            #work backwards in a subset of however many elements descended
            for j in range(i,i-1-desc,-1):
                #if difference in candies is greater than 1 or
                #the previous candy has a lower value than the current candy or
                #the previous students score is less than or equal to the current student
                #then break the loop over subset
                if candies[j-1]-candies[j] > 1 or candies[j-1]<candies[j] or arr[j-1]<=arr[j]:
                    break
                #if previous students candies equals currents students then add
                #one to the previous student and continue
                if candies[j] == candies[j-1]:
                    candies[j-1]+=1
                    continue
                #if you have something like 4,5,4 then continue, dont want to end up with 4,6,4
                if candies[j-1] > candies[j-2] and candies[j-1] > candies[j]:
                    continue
                #otherwise add 1 to the previous persons candies
                else:
                    candies[j-1] += 1

print(sum(candies))
```

## [Stock Maximize](https://www.hackerrank.com/challenges/stockmax)

This is not DP but it will pass all test cases. The idea is to find all of the maxima of the array, then buy up all stocks before that point and sell them on that maxima day. Then repeat this for all the stocks after that maxima (find maxima, buy before, sell on day, repeat for days after...). Worst case (stock prices are all decreasing) this method is O(N^2) ([see this page for why](http://www.leda-tutorial.org/en/official/ch02s02s03.html)) and space used only decreases over time since each array is replaced by a smaller one. [Here is a better solution that uses a similar concept but is O(N)](https://www.hackerrank.com/challenges/stockmax/forum/comments/126930).
```
def arg_max(arr):
    max_v = -999999999
    for i,x in enumerate(arr):
        if x > max_v:
            max_v = x
            max_i = i

    return max_i

T = int(input().strip())
for _ in range(T):
    N = int(input().strip())
    arr = [int(i) for i in input().strip().split()]

    profit = 0
    while arr:
        max_i = arg_max(arr)
        bought = sum(arr[:max_i])
        amt_bought = len(arr[:max_i])
        profit -= bought
        profit += amt_bought*arr[max_i]
        arr = arr[max_i+1:]
    print(profit)
```

## [Red John is Back](https://www.hackerrank.com/challenges/red-john-is-back)

```
from collections import defaultdict

## Memoization for the ways to order bricks
brick_memo = defaultdict(int)
for i in range(1,4):
    brick_memo[i] = 1 # only one way to arrange 4x1,2,3
brick_memo[4] = 2 # two ways to arrange 4x4

## Basically place either 4 1x4s or 1 4x1 and get
## the count of remaining n spots and add to # of ways
## recursively call the function for smaller N values
def get_combinations(N):
    '''
    >>> get_combinations(7)
    5
    '''
    if N in brick_memo:
        return brick_memo[N]
    ways = 0
    if N > 4:
        ways += get_combinations(N-4)
    ways += get_combinations(N-1)
    brick_memo[N] = ways
    return ways

## Memoization for whether or not something is prime
primes = {}
def isPrime(n):
    '''
    >>> isPrime(5)
    True
    >>> isPrime(100)
    False
    '''
    if n in primes:
        return primes[n]
    n2 = n
    i = 2
    while i*i<=n:
        if n%i == 0:
            n//=i
        else:
            i+=1
    if n2 == n:
        primes[n2] = True
        return True
    else:
        primes[n2] = False
        return False

## Memoization for the number of primes up to and including a number
primes_up_to = {1:0,2:1,3:2,4:2,5:3}
def prime_count(N):
    '''
    >>> prime_count(11)
    5
    '''
    if N in primes_up_to:
        return primes_up_to[N]
    max_so_far = max(primes_up_to.keys())
    primes_so_far = primes_up_to[max_so_far]
    for i in range(max_so_far+1,N+1):
        if isPrime(i):
            primes_so_far+=1
        primes_up_to[i] = primes_so_far
    return primes_up_to[N]


if __name__ == "__main__":
    import doctest
    doctest.testmod()

    T = int(input().strip())
    for _ in range(T):
        N = int(input().strip())

        combinations = get_combinations(N)
        print(prime_count(combinations))
```

## [Grid Walking](https://www.hackerrank.com/challenges/grid-walking/submissions/code/22250452)

The general consensus on this problem is that it is much more difficult than it is labeled (should be difficult or advanced instead of moderate). I came up with this solution which works for smaller testcases/dimensions but times out on larger problems. The true solution involves something with combinations and [may involve this](https://barkingbogart.wordpress.com/2013/02/21/cnk-mod-1000000007/) according to one user (I expect its so you only have to calculate for a fraction of the positions instead of all of them). I may return to this problem one day but for now this is my solution.
```
from collections import defaultdict
from copy import deepcopy

# outer memo dictionary stores remaining moves
# inner dictionary stores the possible answers from there
memo = defaultdict(lambda:defaultdict(int))

b = 1000000007

def rec_paths(pos, limits, M):
    tuple_pos = tuple(pos)
    if tuple_pos in memo[M]:
        return memo[M][tuple_pos]
    if M == 0:
        return 1
    ways = 0
    for i,x in enumerate(pos):
        if x+1 <= limits[i]:
            new_pos = deepcopy(pos)
            new_pos[i]+=1
            ways = (ways%b + rec_paths(new_pos,limits,M-1)%b)%b
        if x-1 > 0:
            new_pos = deepcopy(pos)
            new_pos[i]-=1
            ways = (ways%b + rec_paths(new_pos,limits,M-1)%b)%b
    memo[M][tuple_pos] = ways
    return ways

T = int(input().strip())
for _ in range(T):
    memo = defaultdict(lambda:defaultdict(int))
    N,M = [int(i) for i in input().strip().split()]
    start = [int(i) for i in input().strip().split()]
    d_limits = [int(i) for i in input().strip().split()]

    print(rec_paths(start, d_limits, M))
```
