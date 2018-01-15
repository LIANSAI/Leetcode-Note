# Array-easy

---

561. Array Parition

1.题目

2.思路

这个题让我们把变量两两组合，取其中的最小值求和，我们的目标应该是让组合中的值尽可能接近（因为是取最小值），所以我们可以对其进行排序后进行间隔求和.

3.代码

```
class solution:
    def pairSum(self,num):
        """
        :type nums: List[int]
        :rtype: int
        """
        return sum(sorted(num)[::2]
```







