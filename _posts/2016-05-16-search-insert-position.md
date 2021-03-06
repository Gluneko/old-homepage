---
layout: post
section-type: post
title: Search Insert Position
category: leetcode
tags: [ 'array','Binary Search' ]
---

### Search Insert Position

<p>Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.</p>

<p>You may assume no duplicates in the array.</p>

<p>
Here are few examples.<br>
<code>[1,3,5,6]</code>, 5 → 2<br>
<code>[1,3,5,6]</code>, 2 → 1<br>
<code>[1,3,5,6]</code>, 7 → 4<br>
<code>[1,3,5,6]</code>, 0 → 0
</p>  


二分搜索法，可直接照搬Search for a Range的代码：  

```cpp  
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int l = 0, r = nums.size(), mid;
    while (l < r) {
        mid = (l + r) / 2;
        if (nums[mid] >= target)
            r = mid;
        else
            l = mid + 1;
    }
    return l;
    }
};
```  



