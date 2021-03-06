---
layout: post
section-type: post
title: Set Matrix Zeroes
category: leetcode
tags: [ 'array' ]
---

### Set Matrix Zeroes

Given a <i>m</i> x <i>n</i> matrix, if an element is 0, set its entire row and column to 0. Do it in place.<br>
<b>Follow up:</b>
Did you use extra space?<br>
A straight forward solution using O(<i>m</i><i>n</i>) space is probably a bad idea.<br>
A simple improvement uses O(<i>m</i> + <i>n</i>) space, but still not the best solution.<br>
Could you devise a constant space solution?   


这道题中说的空间复杂度为O(mn)的解法是直接新建一个和matrix等大小的矩阵，然后一行一行的扫，只要有0，就将新建的矩阵的对应行全赋0，行扫完再扫列，然后把更新完的矩阵赋给matrix即可，这个算法的空间复杂度太高。将其优化到O(m+n)的方法是，用一个长度为m的一维数组记录各行中是否有0，用一个长度为n的一维数组记录各列中是否有0，最后直接更新matrix数组即可。这道题的要求是用O(1)的空间，那么我们就不能新建数组，我们考虑就用原数组的第一行第一列来记录各行各列是否有0.  
- 先扫描第一行第一列，如果有0，则将各自的flag设置为true    
- 然后扫描除去第一行第一列的整个数组，如果有0，则将对应的第一行和第一列的数字赋0    
- 再次遍历除去第一行第一列的整个数组，如果对应的第一行和第一列的数字有一个为0，则将当前值赋0    
- 最后根据第一行第一列的flag来更新第一行第一列  
代码如下：  


```cpp  
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        const size_t m=matrix.size();
        const size_t n=matrix[0].size();
        bool row_has_zero=false,col_has_zero=false;
        for(size_t i=0;i<m;++i)
        {
            if(matrix[i][0]==0) 
            {
                row_has_zero=true;
                break;
            }
        }
        for(size_t j=0;j<n;++j)
        {
            if(matrix[0][j]==0) 
            {
                col_has_zero=true;
                break;
            }
        }
        for(size_t i=1;i<m;++i)
            for(size_t j=1;j<n;++j)
            {
                if(matrix[i][j]==0)
                    matrix[i][0]=matrix[0][j]=0;
            }
        for(size_t i=1;i<m;++i)
            for(size_t j=1;j<n;++j)
            {
                if(matrix[i][0]==0||matrix[0][j]==0)
                    matrix[i][j]=0;
            }
        if(row_has_zero)
             for(size_t i=0;i<m;++i)
                matrix[i][0]=0;
        if(col_has_zero)
             for(size_t j=0;j<n;++j)
                matrix[0][j]=0;
    }
};
```  



