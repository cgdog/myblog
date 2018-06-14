---
title: leetCode 207. Course Schedule
id: 682
categories:
  - algorithm
date: 2016-11-09 10:26:13
tags:
  - BFS
  - C++
  - DFS
  - graph theory
  - leetcode
---

[207\. Course Schedule](https://leetcode.com/problems/course-schedule/)

There are a total of n courses you have to take, labeled from `0` to `n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

**For example:**

    2, [[1,0]]
    

    There are a total of 2 courses to take. To take course 1 you should have finished course 0\. So it is possible.

    `2, [[1,0],[0,1]]`

    There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1\. So it is impossible.

    **Note:**
    The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.

    **Hints:**

    This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.

    [Topological Sort via DFS](https://class.coursera.org/algo-003/lecture/52) - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.
    Topological sort could also be done via [BFS](http://en.wikipedia.org/wiki/Topological_sorting#Algorithms).

    ### BFS topological sort:



``` cpp
    class Solution {

    <pre>`public:
        bool canFinish(int numCourses, vector&lt;pair&lt;int, int&gt;&gt;&amp; prerequisites) {
            vector&lt;unordered_set&lt;int&gt;&gt; graph(numCourses);
            vector&lt;int&gt; indegree(numCourses, 0);
            for (int i = 0; i &lt; prerequisites.size(); i++) {
                graph[prerequisites[i].second].insert(prerequisites[i].first);
            }
            for (int i = 0; i &lt; numCourses; i ++) {
                for (int neighbor : graph[i]) {
                    indegree[neighbor]++;
                }
            }
            for (int i = 0; i &lt; numCourses; i++) {
                int j = 0;
                for (; j &lt; numCourses; j++) {
                    if (!indegree[j]) break;
                }
                if (j == numCourses) return false;
                indegree[j] = -1;
                for (int neighbor : graph[j]) {
                    indegree[neighbor]--;
                }
            }
            return true;
        }
    };
```

    ### DFS detect cycle. faster.



``` cpp
class Solution {
    public:

        bool DFS_dect_cycle(vector&lt;unordered_set&lt;int&gt;&gt; &amp;graph, int i, vector&lt;bool&gt; &amp;visited, vector&lt;bool&gt; &amp;curPath) {
            if (visited[i]) return false;
            curPath[i] = visited[i] = true;
            for (int neighbor : graph[i]) {
                if (curPath[neighbor] || DFS_dect_cycle(graph, neighbor, visited, curPath))
                    return true;
            }
            return curPath[i] = false;
        }

        bool canFinish(int numCourses, vector&lt;pair&lt;int, int&gt;&gt;&amp; prerequisites) {
            vector&lt;unordered_set&lt;int&gt;&gt; graph(numCourses);
            vector&lt;bool&gt; visited(numCourses, false), curPath(numCourses, false);

            for (int i = 0; i &lt; prerequisites.size(); i++) {
                graph[prerequisites[i].second].insert(prerequisites[i].first);
            }
            for (int i = 0; i &lt; numCourses; i ++) {
                if (!visited[i] &amp;&amp; DFS_dect_cycle(graph, i, visited, curPath))
                    return false;
            }

            return true;
        }
    };
```
> Reference:[https://discuss.leetcode.com/topic/17273/18-22-lines-c-bfs-dfs-solutions](https://discuss.leetcode.com/topic/17273/18-22-lines-c-bfs-dfs-solutions)