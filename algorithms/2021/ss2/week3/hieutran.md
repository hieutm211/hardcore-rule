# Problem 1: Merge Sorted Array
https://leetcode.com/problems/merge-sorted-array/

```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: None Do not return anything, modify nums1 in-place instead.
        """
        iNums1 = m-1
        iNums2 = n-1
        for i in reversed(range(n+m)):
            if (iNums2 < 0 or (iNums1 >= 0 and nums1[iNums1] >= nums2[iNums2])):
                nums1[i] = nums1[iNums1]
                iNums1 -= 1
            else:
                nums1[i] = nums2[iNums2]
                iNums2 -= 1
```
