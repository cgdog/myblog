---
title: leetCode Sudoku Solver
id: 405
categories:
  - algorithm
  - leetcode
date: 2016-09-20 23:19:44
tags:
---

[Sudoku Solver](https://leetcode.com/problems/sudoku-solver/)

Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character '.'.

You may assume that there will be only one unique solution.

![](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

A sudoku puzzle...

![](http://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)

...and its solution numbers marked in red.



``` cpp
class Solution {
public:

    bool isValid(vector<vector<char>>& board, int i, int j, char c) {
        for (int col = 0; col < 9; col++) {
            if (board[i][col] == c || board[col][j] == c) {
                return false;
            }
        }
        for (int row = ( i / 3)*3; row < (i / 3 + 1)*3; row++) {
            for (int col = (j / 3)*3; col < (j / 3 + 1)*3; col++) {
                if (board[row][col] == c) {
                    return false;
                }
            }
        }
        return true;
    }

    bool solve(vector<vector<char>>& board) {
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] ==  '.') {
                    for (char c = '1'; c <= '9'; c++) {
                        if (isValid(board, i, j, c)) {
                            board[i][j] = c;
                            if (solve(board)) {
                                return true;
                            } else {
                                board[i][j] = '.';
                            }
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
    void solveSudoku(vector<vector<char>>& board) {
        solve(board);
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/11327/straight-forward-java-solution-using-backtracking](https://discuss.leetcode.com/topic/11327/straight-forward-java-solution-using-backtracking)