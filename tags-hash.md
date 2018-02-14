# Tags Hash

---

136 Single Number

```
class Solution:
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        dic={}

        for num in nums:
            dic[num]=dic.get(num,0)+1

        for key,value in dic.items():
            if value==1:
                return key
```

---

202 Happy Number

```
class Solution:
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """

        mem=set()

        while n!= 1:
            n=sum([int(i)**2 for i in str(n)])  #str化数字n让我们可以遍历n中的每一个数字

            if n in mem:
                return False
            else:
                mem.add(n)
        else:
            return True
```

---

204 Count Primes

```
class Solution:
    def countPrimes(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n<3:     #质数大于等于2
            return 0

        primes=[True]*n  #True代表是质数

        primes[0]=primes[1]=False

        for i in range(2,int(n**0.5)+1): #每一个循环数i代表能否被i整除
            if primes[i]:  
                primes[i*i:n:i]=[False]* len(primes[i*i:n:i]) 
                #从i开始间隔为i的数列，代表肯定能被i整除
        return sum(primes)
```

---

205 Isomorphic Strings

这个题的隐藏含义是说 这两个string的字母必须是一一对应的映射关系，下面解法如果只保留len\(set\(zip\(s, t\)\)\) == len\(set\(s\)\)，在"ab","aa"的case中， 第2个string的a会对应两个字母，那么对其取set后，其长度必不和zip后的set长度一致

```
class Solution:
    def isIsomorphic(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        return len(set(zip(s, t))) == len(set(s)) and len(set(zip(t, s))) == len(set(t))
```

---

242 Valid Anagram

两个string元素出现的次数必须一样

```
class Solution:
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        ds={}
        dt={}

        for _s in s:
            ds[_s]=ds.get(_s,0)+1
        for _t in t:
            dt[_t]=dt.get(_t,0)+1

        return ds == dt
```

---

290 Word Pattern

这个题和205题类似，但是除了要一一对应之外，还要求其本来长度一致，因为zip\(set\(\)\)只会以较短的一项产生映射，而且这个题目里面没有两个输入长度相等的条件

```
class Solution:
    def wordPattern(self, pattern, str_):
        """
        :type pattern: str
        :type str: str
        :rtype: bool
        """
        str_ = str_.split()

        return len(set(zip(pattern,str_))) == len(set(pattern)) and len(set(zip(pattern,str_))) == len(set(str_)) and len(pattern)==len(str_)
```

---

349 Intersection of Two Arrays

```
class Solution(object):
def intersection(self, nums1, nums2):
    """
    :type nums1: List[int]
    :type nums2: List[int]
    :rtype: List[int]
    """
    return list(set(nums1) & set(nums2))
```

use dict/hashmap to record all nums appeared in the first list, and then check if there are nums in the second list have appeared in the map.

```
class Solution:
    def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        res=[]
        dic={}

        for num1 in nums1:
            dic[num1]=dic.get(num1,0)+1

        for num2 in nums2:
            if num2 in dic and dic[num2]>0:
                res.append(num2)
                dic[num2]=0

        return res
```

---

349 Intersection of Two Arrays II

```
class Solution:
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        res=[]
        dic={}

        for num1 in nums1:
            dic[num1]=dic.get(num1,0)+1

        for num2 in nums2: 
            if num2 in dic and dic[num2]>0:  # 只能append两个list中元素出现较小的次数
                res.append(num2)
                dic[num2]-=1


        return res
```

---

387 First  Unique Character in a String

基本思路 先用字典统计出只出现一次的元素，再遍历string求第一个不重复元素

```
class Solution:
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        """
        dic={}

        for _s in s:
            dic[_s]=dic.get(_s,0)+1

        if 1 not in dic.values():
            return -1
        else:
            for i in range(len(s)):
                if dic[s[i]] == 1:
                    return i
                    break
```

更快的思路 60ms

```
class Solution:
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        """

        letters='abcdefghijklmnopqrstuvwxyz'

        index = [s.index(l) for l in letters if s.count(l) ==1]  # s.index(l)只返回第一个字母出现的位置 

        return min(index) if len(index)>0 else -1
```

---

389 Find the difference

Bit Manipulation

```
class Solution:
    def findTheDifference(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        dic={}


        for _s in s:
            dic[_s]=dic.get(_s,0)+1
        for _t in t:
            dic[_t] = dic[_t]-1 if _t in dic and dic[_t]>0 else 1 #大于0是因为如果添加s中有的元素，就会减到0

        return min([k for k,v in dic.items() if v ==1])
```

下面这个方法和上面思路是一样的，两字典相减，最后随机添加的元素在字典中的value一定是1（其他是0），以更高效的collection实现

```
import collections

class Solution:
    def findTheDifference(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        return list((collections.Counter(t)-collections.Counter(s)))[0] #[0]和上面min的作用一样，把list元素转为string
```

---

_**409 Longest  Palindrome**_

回文的思路是  对于奇数元素，我们只能用其n-1的数量，除了1个奇数元素可以放到中间，所以解法为：

```
import collections

class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: int
        """
        odds = sum(v&1 for v in collections.Counter(s).values()) #v&1是一种判断奇数偶数的方法 偶数得0 奇数得1 牵扯到二进制计算

        return len(s)-odds+bool(odds) #这里不能直接加1因为可能没有奇数
```

---

438 Find All Anagrams in String

```
from collections import Counter

class Solution:
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        sCounter = Counter(s[:len(p)-1])
        pCounter = Counter(p)
        res=[]

        for i in range(len(p)-1,len(s)):    
            sCounter[s[i]] += 1                 #通过去掉头部加上尾部的数据 避免重复生成字典，减小时间复杂度
            if sCounter == pCounter:  
                res.append(i-len(p)+1)

            sCounter[s[i-len(p)+1]] -=1
            if sCounter[s[i-len(p)+1]] == 0:
                del sCounter[s[i-len(p)+1]]

        return res
```

---

447 Number of Boomerangs

```
class Solution:
    def numberOfBoomerangs(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        res=0

        for p in points:
            camp={}
            for q in points:
                f=p[0]-q[0]
                s=p[1]-q[1]

                camp[f*f+s*s] = camp.get(f*f+s*s,0)+1

            for c in camp:
                res += camp[c]*(camp[c]-1)

        return res
```

---

463 Island Perimeter

Since there are no lakes, every pair of neighbour cells with different values is part of the perimeter \(more precisely, the edge between them is\). So just count the differing pairs, both horizontally and vertically \(for the latter I simply transpose the grid\).

对于operator.ne的解释：

\[0\] + \[1,2,3,4,5,6,7,8\] = \[0,1,2,3,4,5,6,7,8\]

\[1,2,3,4,5,6,7,8\] + \[0\] = \[1,2,3,4,5,6,7,8,0\]

basically, operator.ne compares 1 with 0 and 2, and compares 2 with 1 and 3… It compares every element with its two neighbors.

```
class Solution:
    def islandPerimeter(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        
        return sum(sum(map(operator.ne, [0] + row, row + [0]))
               for row in grid + map(list, zip(*grid)))
                    
```

---

573 Distribute Candies

让妹妹先拿糖果，每种拿一个

```
class Solution:
    def distributeCandies(self, candies):
        """
        :type candies: List[int]
        :rtype: int
        """
        
        kind=len(set(candies))
        num= len(candies)/2
        
        return int(min(kind,num))
```



