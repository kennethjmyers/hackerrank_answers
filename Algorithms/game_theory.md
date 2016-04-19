# Game Theory

## Permutation Game

```
from copy import deepcopy
from collections import defaultdict


memo = defaultdict(str)
sort_memo = defaultdict(bool)

#used to determine if a sublist is sorted and cache result
def check_list(lst):
    global sort_memo

    list_is_sorted = True
    #if one element return True
    if len(lst) == 1:
        sort_memo[tuple(lst)] = True
        return True

    for i in range(1,len(lst)):
        #if previous element is greater return not sorted
        if lst[i-1] > lst[i]:
            sort_memo[tuple(lst)] = False
            return not list_is_sorted

    #else return sorted
    sort_memo[tuple(lst)] = True
    return list_is_sorted

def recursive_func(lst, turn='A',top_level=True):
    global memo
    global sort_memo
    #reinitialize these for each test case
    if top_level:
        memo = defaultdict(str)
        sort_memo = defaultdict(bool)

    #each sublist has only one result so if its
    #already cached then return it
    if tuple(lst) in memo:
        return memo[tuple(lst)]

    #we dont need to check if a list is sorted each
    #time if it is already chached so chache that too
    if tuple(lst) in sort_memo:
        check = sort_memo[tuple(lst)]
    else:
        check = check_list(lst)

    #if list is sorted return the result of the person who made that turn
    if check:
        if turn is 'B':
            result = 'A'
        else:
            result = 'B'
        memo[tuple(lst)] =  result
        return 'A' if turn is 'B' else 'B'

    #loop over the list and create a sublist and recursively check each sublist
    for i in range(len(lst)):
        new_lst = deepcopy(lst)
        new_lst.pop(i)
        if turn == 'A':
            res = recursive_func(new_lst,turn='B',top_level=False)
        else:
            res = recursive_func(new_lst,turn='A',top_level=False)

        #this represents a win for this persons turn
        #if at least one win, then optimal move is to win
        if res == turn:
            memo[tuple(lst)] = turn
            return turn

    #this represents all losses were returned for this persons turn
    # so return the opponent
    if turn is 'B':
        result = 'A'
    else:
        result = 'B'
    memo[tuple(lst)] =  result
    return 'A' if turn is 'B' else 'B'


T = int(input().strip())

for _ in range(T):
    N = int(input().strip())
    perm = list(map(int,input().strip().split()))
    result = recursive_func(perm)
    if result == 'A':
        print('Alice')
    else:
        print('Bob')
```

## Chocolate in the Box

```

```
