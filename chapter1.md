
---

# Array-easy

---

561 Array Parition

1.题目

2.解法

这个题让我们把变量两两组合，取其中的最小值求和，我们的目标应该是让组合中的值尽可能接近（因为是取最小值），所以我们可以对其进行排序后进行间隔求和.

```
class solution:
    def pairSum(self,num):
        """
        :type nums: List[int]
        :rtype: int
        """
        return sum(sorted(num)[::2]
```

---

566 Reshape the matrix

1.题目

2.解法

1. 通过np.reshape

```
import numpy as np
    class solution:
        def matrixReshape(self,nums,r,c):
        """
        :type nums: List[List[int]]
        :type r: int
        :type c: int
        :rtype: List[List[int]]
        """
        try:
            return np.reshape(nums,(r,c)).tolist()
        except:
            return nums
```

2.收集A中的数据，在将其放进r\*c的矩阵中

```
       def matrixResahpe(self,nums,r,c)：
           if len(nums)*len(nums[0])!= r*c: 
               return nums

           vals=(val for row in nums for val in row) 
           return [[vals.next() for xc in xrange(c)] for xr in xrange(r)]     #Python 3.X版本xrange取消，range代替xrange
```

---

485 Max Consecutive One

1.题目

2.解法

自己第一思路是用list保存连续1的值，最后选出最大值，但实际上这样效率差，更简便方法

```
class Solution:
    def findMaxConsecutiveOnes(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        con=0
        ans=0
        for num in nums:
            if num==1:
                con+=1
                ans=max(con,ans) #这一步实际上保存了每次连续的最大值
            else: 
                con=0
        return ans
```

---

695 Max area of Island

1.题目

2.解法

递归的方法

```
class Solution:
    def maxAreaOfIsland(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m,n = len(grid),len(grid[0])  #grid表示有多少行，grid[0]表示有多少列
        def dfs(i,j):
            if 0<=i<m and 0<=j<n and grid[i][j]: 
                grid[i][j]=0  #探索过的地区设置为0 
                return 1 + dfs[i-1,j] + dfs[i+1,j] + dfs[i,j-1] + dfs[i,j+1] #搜寻四个方位
            return 0 

        areas=[dfs(i,j) for i in range(m) for j in range(n) if grid[i][j]]
        return max(areas) if areas else 0
```

---

448 Find All Numbers Disappeared in an Array

1.题目

2.解法

错误答案，这实际上是O\(n^2）时间复杂度

```
class Solution:
    def findDisappearedNumbers(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """

        return [i for i in range(1,len(nums)+1) if i not in nums]
```

正解： set差集时间复杂度为O（len\(s\)\)

```
    def findDisappearedNumbers(self, nums):
         """
         :type nums: List[int]
         :rtype: List[int]
         """

         return list(set(range(1,len(nums)+1))-set(nums))
```

---

283 Mover Zeroes

1.题目

2.解法

```
class Solution:
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        zero = 0  #记录0的位置
        for i in range(len(nums)):
            if nums[i] != 0：
                nums[i],nums[zero] = nums[zero], nums[i] #交换i，j的位置，即把非零元素排到前面，原位置变成0
                zero += 1
```

---

717 1-bit and 2-bit Characters

1.题目

2.解法

```
class Solution:
    def isOneBitCharacter(self, bits):
        """
        :type bits: List[int]
        :rtype: bool
        """
        if not bits: return False #bits 为空
        
        n=len(bits)
        index=0
        while index<n:
            if index==n-1: return True #最后只剩一个0的时候一定是1 bit
            if bits[index] = 1：
                index += 2
            else:
                index += 1
        return False
```

   

---

169 Majority Element

1.题目

2.解法

2.1

```
class Solution:
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n=len(nums)
        nums_set = set(nums)  #找出不重复元素
        
        for num in nums_set:
            if nums.count(num)>n/2: 
                return num
                break
```

2.2

O\(nlogn\)

```
return sorted(num)[len(num)/2]

#NOTICE that the majority element always exist in the array,so that the middle always is the answer
```

2.3

使用字典

```
def majorityElement(self, nums):
    dic={}
    for num in nums:
        dic[num]=dic.get(num,0)+1 #使用字典count
    for num in nums:
        if dic[num]>n/2:
            return num
    
```



