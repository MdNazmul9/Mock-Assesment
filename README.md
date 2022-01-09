# Mock-Assesment
### Q1
```
Given two arrays arr1 and arr2, the elements of arr2 are distinct, and all elements in arr2 are also in arr1.

Sort the elements of arr1 such that the relative ordering of items in arr1 are the same as in arr2. Elements that do not appear in arr2 should be placed at the end of arr1 in ascending order.

 

Example 1:

Input: arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
Output: [2,2,2,1,4,3,3,9,6,7,19]
Example 2:

Input: arr1 = [28,6,22,8,44,17], arr2 = [22,28,8,6]
Output: [22,28,8,6,17,44]
 

Constraints:

1 <= arr1.length, arr2.length <= 1000
0 <= arr1[i], arr2[i] <= 1000
All the elements of arr2 are distinct.
Each arr2[i] is in arr1.

```
#### Sol 1:
```
# count frequencey of arr1
# append element from arr2 x how many times x occur in arr1
# apped other elements from arr1 which are not exist in arr2 in sorted list


from collections import Counter

def relativeSortArray(arr1, arr2):
    res = []
    
    fq = Counter(arr1)
    for i in arr2:
        res.extend([i]*fq[i])
        fq[i]=0
    ren=list(sorted(filter(lambda x: fq[x] != 0, fq.keys())))
    for i in ren:
        res.extend([i]*fq[i])
    return res
    
print(relativeSortArray(arr1 = [28,6,22,8,44,17], arr2 = [22,28,8,6]))
```

### Q2
```
You have n dice and each die has k faces numbered from 1 to k.

Given three integers n, k, and target, return the number of possible ways (out of the kn total ways) to roll the dice so the sum of the face-up numbers equals target. Since the answer may be too large, return it modulo 109 + 7.

 

Example 1:

Input: n = 1, k = 6, target = 3
Output: 1
Explanation: You throw one die with 6 faces.
There is only one way to get a sum of 3.

Example 2:

Input: n = 2, k = 6, target = 7
Output: 6
Explanation: You throw two dice, each with 6 faces.
There are 6 ways to get a sum of 7: 1+6, 2+5, 3+4, 4+3, 5+2, 6+1.

Example 3:

Input: n = 30, k = 30, target = 500
Output: 222616187
Explanation: The answer must be returned modulo 109 + 7.

 

Constraints:

    1 <= n, k <= 30
    1 <= target <= 1000

```

#### Sol2:
```
def numRollsToTarget(n,k,target):        
        modulo = 10**9 + 7
        cache = {}
        
        def numRollsToTargetHelper(dd, tt):
            if cache.get((dd,tt)) != None:
                return cache[(dd,tt)]
            nonlocal k
            if dd == 1:
                if tt <= k:
                    return 1
                else:
                    return 0
            
            ret = 0
            for i in range(1, k+1):
                if tt - i > 0:
                    ret += numRollsToTargetHelper(dd-1, tt-i)
            cache[(dd,tt)] = ret
            return ret
        
        ret = numRollsToTargetHelper(n, target)
        return ret % modulo
    
    
print(numRollsToTarget(2,6,7))
```
