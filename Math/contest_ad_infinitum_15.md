# Ad infinitum 15

Contest.

## K-element Sequences


Language:Python3
```
from functools import reduce

b = 1000000007
facts = {0:1,1:1}

for i in range(2,2*10**6+1):
    facts[i] = ((i)*(facts[i-1]))%b

def nCr(n,r):
    try:
        num = facts[n]
        den = pow(facts[r],b-2,b)
        den2 = pow(facts[n-r],b-2,b)
        return reduce(lambda x,y: (((x)%b)*(y%b))%b, [num,den,den2])
    except:
        return 1

t = int(input().strip())
for _ in range(t):
    n,k = input().strip().split()
    n,k = int(n),int(k)
    #print(nCr(n-1,k-1))
    print(nCr(n-1,k-1)%b)
```

## Angles in Space

Language: python3
```
from math import sqrt,acos
from itertools import permutations

n = int(input().strip())
points = []
for _ in range(n):
    p = input().strip().split()
    p = [int(i) for i in p]
    points.append(p)

def get_angle(p1,p2,p3):
    v1 = [p1[0]-p2[0],p1[1]-p2[1],p1[2]-p2[2]]
    v2 = [p3[0]-p2[0],p3[1]-p2[1],p3[2]-p2[2]]
    v1mag = sqrt(v1[0]**2+v1[1]**2+v1[2]**2)
    v1norm = [v1[0]/v1mag,v1[1]/v1mag,v1[2]/v1mag]
    v2mag = sqrt(v2[0]**2+v2[1]**2+v2[2]**2)
    v2norm = [v2[0]/v2mag,v2[1]/v2mag,v2[2]/v2mag]
    res = v1norm[0] * v2norm[0] + v1norm[1] * v2norm[1] + v1norm[2] * v2norm[2]
    angle = acos(res)
    return angle

angles = []
indices = list(range(len(points)))
s = set(permutations(indices,3))
new_s = set()
for i in s:
    if tuple(list(i)[::-1]) not in new_s and i[0]<i[1]<i[2]:
        new_s.add(i)

for p_set in new_s:
    a = get_angle(points[p_set[0]],points[p_set[1]],points[p_set[2]])
    if a:
        angles.append(a)

#print(new_s,angles)
print(sum(angles)/len(angles))
```

## Multipoint evaluation

Language: python3
This solution was way to slow to pass the test cases
```
from functools import reduce

arr = input().strip().split()
n,b,c,d,e = [int(i) for i in arr]

mo = 1000003

c_cache = {0:1}
for i in range(1, 10**6+1):
    c_cache[i] = (c*c_cache[i-1])%mo

a_arr = input().strip().split()
a_arr = [int(i) for i in a_arr]

x_k = [((((b)*(pow(c_cache[k],4,mo)))%mo)+(((d)*(pow(c_cache[k],2,mo)))%mo)+e)%mo for k in a_arr]

for i in range(len(a_arr)):
    num = a_arr[0]*1
    rec = (((x_k[i])*(a_arr[-1]))%mo)
    for j in range(n-2):
        rec = ((x_k[i]) * ((a_arr[-2-j] + rec)%mo)%mo)%mo
    print(num+rec)
    #val = [((a2%mo)*(x_k[i]**j)%mo)%mo for j,a2 in enumerate(a_arr)]
    #print(reduce(lambda x,y:((x%mo)+(y%mo))%mo,val ))
```
