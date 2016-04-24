# Strings

## Pangrams

```
from collections import defaultdict

counter = defaultdict(int)

s = input().strip().replace(' ','').lower()
#print(s)

for i in s:
    counter[i] += 1

pangram = True
for i in 'abcdefghijklmnopqrstuvwxyz':
    if counter[i] == 0:
        pangram = False

if pangram:
    print('pangram')
else:
    print('not pangram')
```

## Alternating Characters

All test cases passed in < 0.4 seconds. Save time by not actually removing from string/list
```
T = int(input().strip())

for _ in range(T):
    s = list(input().strip())
    length_s = len(s)
    i = 1
    deletions = 0
    last_letter = s[i-1]
    while i < length_s:
        if s[i] == last_letter:
            i+=1
            deletions += 1
        else:
            last_letter = s[i]
            i+=1

    print(deletions)
```

## The Love-Letter Mystery

The idea behind this is to take the absolute difference between symmetric opposites in the string and sum each of them. This is because the absolute difference is the amount a letter has to be lowered to reach the other.
```
import string
from collections import defaultdict

abc_dict = defaultdict(int)
abc = string.ascii_lowercase
for i,a in enumerate(abc):
    abc_dict[a] = i


T = int(input().strip())

for _ in range(T):
    s = list(input().strip())

    count = 0
    for i in range(len(s)//2):
        count += abs(abc_dict[s[i]]-abc_dict[s[-i-1]])
    print(count)
```

## Gemstones

```
from functools import reduce


T = int(input().strip())

rocks = []
for _ in range(T):
    rocks.append(set(input().strip()))

print(len(reduce(set.intersection,rocks)))
```

## Funny String

```

```

##
