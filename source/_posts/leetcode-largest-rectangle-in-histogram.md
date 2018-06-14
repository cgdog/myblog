---
title: leetCode Largest Rectangle in Histogram
id: 415
categories:
  - algorithm
date: 2016-09-21 15:28:24
tags:
  - leetcode
---

[Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](http://www.leetcode.com/wp-content/uploads/2012/04/histogram.png)

Above is a histogram where width of each bar is 1, given **height = [2,1,5,6,2,3]**.

![](http://www.leetcode.com/wp-content/uploads/2012/04/histogram_area.png)

The largest rectangle is shown in the shaded area, which has area = 10 unit.

For example,

Given **heights = [2,1,5,6,2,3]**,

return 10.



``` cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        if (heights.empty()) {
            return 0;
        }

        int area = 0;
        vector<int> st;
        int n = heights.size();
        for (int i = 0; i <= n; i++) {

            int h = i == n ? 0 : heights[i];
            if (st.empty() || h >= heights[st.back()]) {
                st.push_back(i);
            } else {
                int top = st.back();
                st.pop_back();
                int tmparea = (st.empty()?i:(i - 1 - st.back())) * heights[top];
                area = area > tmparea ? area : tmparea;
                i--;
            }

        }
        return area;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/7599/o-n-stack-based-java-solution/2](https://discuss.leetcode.com/topic/7599/o-n-stack-based-java-solution/2)