---
title: leetCode Maximal Rectangle
tags:
  - Dynamic Programming
  - leetcode
id: 411
categories:
  - algorithm
date: 2016-09-21 11:51:24
---

[Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/)

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

For example, given the following matrix:

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

Return 6.



``` cpp
// DP
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {

         int area = 0;
        if (matrix.empty()) {
            return area;
        }

        const int m = matrix.size();
        const int n = matrix[0].size();
        vector<int> left(n, 0), right(n, n), height(n, 0);

        for (int i = 0; i < m; i++) {
            int cur_left = 0, cur_right = n;
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '1') {
                    height[j]++;
                } else {
                    height[j] = 0;
                }
            }

            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '1') {
                    left[j] = max(left[j], cur_left);
                } else {
                    left[j] = 0;
                    cur_left = j+1;
                }
            }

            for (int j = n-1; j >= 0; j--) {
                if (matrix[i][j]=='1') {
                    right[j] = min(right[j], cur_right);
                } else {
                    right[j] = n;
                    cur_right = j;
                }
            }

            for (int j = 0; j < n; j++) {
                area = max(area, (right[j]-left[j])*height[j]);
            }
        }
        return area;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/6650/share-my-dp-solution](https://discuss.leetcode.com/topic/6650/share-my-dp-solution)

```
//
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {

        int area = 0;
        if (matrix.empty()) {
            return area;
        }

        const int m = matrix.size();
        const int n = matrix[0].size();
        vector<int> height(n+1, 0);
        vector<int> st;
        for (int i = 0; i < m; i++) {
            st.clear();
            for (int j = 0; j <= n; j++) {
                if (j < n) 
                    height[j] = matrix[i][j]=='1' ? (height[j]+1) : 0;

                if (st.empty() || height[j] >= height[st.back()]) {
                    st.push_back(j);
                    continue;
                }
                while (!st.empty() && height[j] <height[st.back()]) {
                    int top = st.back();
                    st.pop_back();
                    int begin = st.empty() ? 0 : st.back()+1;
                    int tmp = height[top] * (j - begin);
                    area = area > tmp ? area : tmp;
                }
                st.push_back(j);
            }
        }
        return area;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/1634/a-o-n-2-solution-based-on-largest-rectangle-in-histogram/13](https://discuss.leetcode.com/topic/1634/a-o-n-2-solution-based-on-largest-rectangle-in-histogram/13)