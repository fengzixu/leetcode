# 18 - 四数相加

## 题目描述
![problem](images/18.png)

我是怎么也想不出来时间复杂度小一点的方法，于是只好利用搜索引擎了。

cr: 
* [Quadratic algorithm for 4-SUM](https://stackoverflow.com/questions/14732277/quadratic-algorithm-for-4-sum)
* [zhuli19901106](https://github.com/zhuli19901106/leetcode-2/blob/master/4sum_1_AC.cpp)
* [leetcode：4Sums(四个数相加的和)](http://www.cnblogs.com/zhaolizhen/p/3378685.html)

## 解题思路
1. 升序排序；
2. 使用双层循环计算两数之和；
3. 两指针在剩余元素中相向移动；
4. 若四数之和等于target，加入结果序列；
5. 跳过重复值。

```python
class Solution:
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """

        nums = sorted(nums)
        l = len(nums)
        res = []

        # i1,i2,i3,i4为四个指针
        for i1 in range(0, l-3):
        	for i2 in range(i1 + 1, l-2):
        		i3 = i2 + 1
        		i4 = l - 1

        		# 循环结束条件为两指针相遇
        		while i3 < i4:
        			the_sum = nums[i1] + nums[i2] + nums[i3] + nums[i4]
        			if the_sum < target:
        				i3 += 1
        			elif the_sum > target:
        				i4 -= 1
        			else:
        				li = [ nums[i1], nums[i2], nums[i3], nums[i4] ] 
        				if li not in res:
        					res.append(li)
        				
        				i3 += 1

        return res
```

## debug
list赋值错误
![error](images/error.png)
li是空数组，使用li[0]=xx这样赋值当然越界了，改用append。