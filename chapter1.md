
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

189 Rotate array

1.题目

2.解法

```
class Solution:
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """

        n=len(nums)
        nums[:]=nums[n-k:]+nums[:n-k]

        这里不能写成 nums = nums[n-k:] + nums[:n-k] 
        因为 The previous one can truly change the value of old nums, but the following one just changes its reference to a new nums not the value of old nums.
```

---

217 Contains Duplicate

1.题目

2.解法

```
class Solution:
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        res=set(nums)

        return False if len(res) == len(nums) else True
```

```
class Solution(object):
def containsDuplicate(self, nums):
    """
    :type nums: List[int]
    :rtype: bool
    """
    return len(nums) != len(set(nums))
```

---

219 Contains Duplicate II

1.题目

2.解法

哈希表

```
class Solution:
    def containsNearbyDuplicate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        d={}

        for i, v in enumerate(nums):
            if v in d and i-d[v] <= k:  #如果字典中已经有了v且key值差不超过k
                return True

            d[v] = i

        return False
```

---

268 Missing number

1.题目

2.解法

sum方法 差额即为缺少的数

```
class Solution:
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return int((len(nums))/2*(len(nums)+1)-sum(nums))
```

---

414 Third Maximum Number

1.题目

2.解法

set找出非重复元素，之后逐一移除 第一大和第二大元素

```
    def thirdMax(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        res=set(nums)
        if len(res)<3:
            return max(res)
        else:
            for i in range(0,2):   #移除第1大和第2大元素
                res.remove(max(res))

        return max(res)
```

```
class Solution(object):
    def thirdMax(self, nums):
        v = [float('-inf'), float('-inf'), float('-inf')]
        for num in nums:
            if num not in v:
                if num > v[0]:   v = [num, v[0], v[1]]
                elif num > v[1]: v = [v[0], num, v[1]]
                elif num > v[2]: v = [v[0], v[1], num]
        return max(nums) if float('-inf') in v else v[2]
```

---

581 Shortest Unsorted Continuous Subarray

1.题目

2.解法

```
class Solution(object):
    def findUnsortedSubarray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        start, end = 0, len(nums) - 1
        while start < len(nums) - 1 and nums[start] <= nums[start + 1]:
            start += 1

        if start == len(nums) - 1:
            return 0

        while end > 0 and nums[end] >= nums[end - 1]:
            end -= 1


        vmin = min(nums[start:(end + 1)])
        vmax = max(nums[start:(end + 1)])

        while start >= 0 and nums[start] > vmin:
            start -= 1
        while end <= len(nums) - 1 and nums[end] < vmax:
            end += 1
        return end - start - 1
```

---

628 Maximum Product of Three numbers

1.题目

2.解法

注意有负值存在，最大值有两种可能，一种是三个最大的正数，第二种是二个最小的负数加上一个最大的正数

```
class Solution:
    def maximumProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums.sort()

        return max(nums[0]*nums[1]*nums[-1], nums[-1]*nums[-2]*nums[-3])
```

---

643 Maximum Average Subarray

1.题目

2.解法

初步思路为遍历，如果每一子序列用sum求解 时间复杂度为0\(n2\),所以我们采取另外一种方法：去掉最前段的数加上新进来的数

```
class Solution:
    def findMaxAverage(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: float
        """

        curave=maxave=sum(nums[:k])

        for i in range(len(nums)-k):  #如果k=len(nums)就会出现range（0）这时候for循环就不会执行，这是前面设置maxave的原因
            curave = curave-nums[i]+nums[i+k]  逐步去掉最开始的加上新进来的 不用sum 降低时间复杂度 
            maxave = max(maxave,curave)

        return maxave/k
```

---

661 Image Smoother

1.题目

2.解法

```
from copy import deepcopy as copy

class Solution:
    def imageSmoother(self, M):
        """
        :type M: List[List[int]]
        :rtype: List[List[int]]
        """

        x_len=len(M)
        y_len=len(M[0]) if x_len else 0 

        res=copy(M)

        for x in range(x_len):
            for y in range(y_len):
                neighbors=[
                    M[_x][_y]
                    for _x in (x-1,x,x+1)
                    for _y in (y-1,y,y+1)
                    if 0<= _x < x_len and 0<=_y<y_len
                ]

                res[x][y] = sum(neighbors)//len(neighbors)

        return res
```

---

665 Non decreasing array

1.题目

2.解法

First, find a pair where the order is wrong. Then there are two possibilities, either the first in the pair can be modified or the second can be modified to create a valid sequence. We simply modify both of them and check for validity of the modified arrays by comparing with the array after sorting.

I find this approach the easiest to reason about and understand.

```
class Solution(object):
    def checkPossibility(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        one, two = nums[:], nums[:]
        for i in range(len(nums) - 1):
            if nums[i] > nums[i + 1]:
                one[i] = nums[i + 1]
                two[i + 1] = nums[i]
                break
        return one == sorted(one) or two == sorted(two)
```

---

674 Longest Continuous Increasing array

1.题目

2.解法

```
class Solution:
    def findLengthOfLCIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0

        _max=0
        _cur=0

        for i in range(len(nums)-1):
            if nums[i+1]>nums[i]:
                _cur+=1
                _max=max(_max,_cur)

            else:
                _cur=0

        return _max+1
```

---

697  Degree of  An Array

1.题目

2.解法

python collections 高效计数模块

```
import collections

class Solution:
    def findShortestSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        c=collections.Counter(nums)

        first,last = {},{}
        for i,v in enumerate(nums):
            first.setdefault(v,i) #只保存第一次出现的值
            last[v]=i 

        degree=max(c.values())

        return min(last[v]-first[v]+1 for v in c if c[v]==degree)
```

---

724 Find Pivot Index

1.题目

2.解法

观察数组，发现left的会每次加上当前索引的上一个数，而right会减掉当前索引数

```
class Solution:
    def pivotIndex(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return -1

        sum_left=0
        sum_right=sum(nums[1:])
        if sum_left==sum_right:
            return 0


        for i in range(1,len(nums)):

            sum_left +=nums[i-1] 
            sum_right-=nums[i]

            if sum_left==sum_right:

                return i
                break

        return -1
```

```
class Solution(object):
    def pivotIndex(self, nums):
        # Time: O(n)
        # Space: O(1)
        left, right = 0, sum(nums)
        for index, num in enumerate(nums):
            right -= num
            if left == right:
                return index  
            left += num         #left和num  在 判断语句一前一后巧妙表达了 上面的思想
        return -1
```

---

746  Min Cost Climbing Stairs

1.题目

2.解法

动态规划

---

747 Largest Number at Least Twice of Others

```
class Solution:
    def dominantIndex(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        one=[0, 0]  #储存最大值和其index
        two=[0, 0]  #储存第二大值和其index

        for index, num in enumerate(nums):
            if num>one[0]:
                two=[one[0],one[1]]         #这里注意必须先更新two ，如果先更one，那one two 的值就都一样了


                one=[num,index]

            elif num>two[0]:
                two=[num,index]

        return one[1] if one[0]>=2*two[0] else -1
```

---

766 Toeplite Matrix

思路为每条对角线上元素都应该是x+1, j+1。这里巧妙在我们不需要一次 把一整个对角列遍历完，而每一次只需要和其下一个数对比，只要有一个不相等，就可以 返回False

```
class Solution:
    def isToeplitzMatrix(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: bool
        """

        for x in range(len(matrix)-1):
            for y in range(len(matrix[0])-1):
                if matrix[x][y] != matrix[x+1][y+1]:
                    return False

        return True
```



