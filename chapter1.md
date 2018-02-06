
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

---

1 Two Sum

1.题目

2.解法

Hash Table

```
class Solution:
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        d={}

        for i, n in enumerate(numbers):
            m=target-n
            if m in d:  # in 找的是key值在不在这个字典中
                return [d[m],i] 
            else:
                d[n] = i  # n是key， i是value
```

---

26 Remove Duplicates from Sorted Array

1.题目

2.解法

Two points 相当于是把不一样的元素置换到前面，length后面的元素可以忽略。

```
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0

        newtail=0

        for i in range(1,len(nums)):
            if nums[i]!=nums[newtail]:
                newtail+=1
                nums[newtail]=nums[i]
        return newtail+1
```

---

27 Remove Element

1.题目

2.解法

Two points O\(n\) 和上一题类似，相当于把不等于val的数字置换到前面，以newtail修改前面的数字，这里的循环是从0开始而不是上一题的1，所以return的是newtail而不是newtail+1

```
class Solution:
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        if not nums:
            return 0

        newtail=0
        for i in range(0,len(nums)):
            if nums[i] != val:
                nums[newtail]=nums[i]
                newtail+=1
        return newtail
```

---

35 Search insert Position

1.题目

2.解法

```
class Solution:
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        for i in range(0,len(nums)):
            if nums[i] == target or nums[i]>target:

                return i

        return i+1
```

---

53 Maximum subarray

1.题目

2.解法

动态规划

```
class Solution:
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0

        cursum=maxsum=nums[0]

        for num in nums[1:]:
            cursum=max(cursum+num,num)
            maxsum=max(maxsum, cursum)

        return maxsum
```

---

118 Pascal's Triangle

1.题目

2.解法

2.1

```
class Solution:
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """


        res = [[1]]
        for i in range(1, numRows):
            res.append([map(lambda x, y: x+y, res[-1] + [0], [0] + res[-1])])
        return res if numRows else[]
```

2.2 leetcode 出现 map not implented

```
class Solution:
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """


        res = [[1]]
        for i in range(1, numRows):
            res.append([map(lambda x, y: x+y, res[-1] + [0], [0] + res[-1])])
        return res if numRows else[]
```

---

119 Pascal's Tringle II

1.题目

2解法

```
class Solution:
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        row=[1]  #注意这里只有一重list
        
        for i in range(rowIndex):
            row = [x+y for x,y in zip([0]+row, row+[0])]  #避免使用map
        return row
```

---

121 Best time to sell and buy

1.题目

2.解法

动态规划  和maxsubarray类似，求一段子序列的最大值（时间变化相当于股票价格波动，反映在盈亏中），若收益变为负，则从0重新开始（相当于以新的时间点买入）

```
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices:
            return 0
        maxpro=curpro=0
        
        for i in range(len(prices)-1):
            dif = prices[i+1]-prices[i]
            curpro = max(dif+curpro,0)
            maxpro = max(curpro, maxpro)
        
        return maxpro
```

---

122 Best time to sell and buy II

1.题目

2.解法

贪心算法  低买高卖

```
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        
        return sum(max(prices[i + 1] - prices[i], 0) for i in range(len(prices)-1))
```

---

