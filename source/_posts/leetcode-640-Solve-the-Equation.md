---
title: leetcode 640. Solve the Equation
categories:
  - algorithm
date: 2017-07-10 21:44:10
tags:
  - C++
  - leetcode
---

[640. Solve the Equation](https://leetcode.com/contest/leetcode-weekly-contest-40/problems/solve-the-equation/)

Solve a given equation and return the value of `x` in the form of string "x=#value". The equation contains only '+', '-' operation, the variable x and its coefficient.

If there is no solution for the equation, return "No solution".

If there are infinite solutions for the equation, return "Infinite solutions".

If there is exactly one solution for the equation, we ensure that the value of `x` is an integer.



**Example 1:**
```
Input: "x+5-3+x=6+x-2"
Output: "x=2"
```

**Example 2:**
```
Input: "x=x"
Output: "Infinite solutions"
```

**Example 3:**
```
Input: "2x=x"
Output: "x=0"
```

**Example 4:**

```
Input: "2x+3x-6x=x+2"
Output: "x=-1"
```

**Example 5:**
```
Input: "x=x+2"
Output: "No solution"
```


``` cpp
class Solution {
public:
	string solveEquation(string equation) {
		size_t equalPos = string::npos;
		equalPos = equation.find('=');
		if (equalPos == string::npos) {
			return "No solution";
		}

		int xnum = 0;

		size_t xpos = equation.rfind('x');
		while (xpos < equation.size()) {
			int i = xpos - 1;
			while (i >= 0 && equation[i] >= '0' && equation[i] <= '9') {
				--i;
			}
			string strcoefficient = equation.substr(i + 1, xpos - 1 - i);

			if (i == xpos - 1) {
				strcoefficient = "1";
			}

			if (i + 1 == 0 || equation[i] == '+' || equation[i] == '=') {
				if (xpos < equalPos) {
					xnum += stoi(strcoefficient);
				}
				else {
					xnum -= stoi(strcoefficient);
				}

			}
			else {
				if (xpos < equalPos) {
					xnum -= stoi(strcoefficient);
				}
				else {
					xnum += stoi(strcoefficient);
				}
			}

			if (i + 1 == 0 || equation[i] == '=') {
				i += 1;
			}
			equation.erase(i, xpos - i + 1);

			xpos = equation.rfind('x', xpos + 1);
		}

		equalPos = equation.find('=');
		int sum = 0;
		bool plus = false;
		int pos = 0;
		while (pos < equation.size()) {
			if (equation[pos] == '+') {
				if (pos < equalPos)
					plus = false;
				else
					plus = true;
				++pos;
			}
			else if (equation[pos] == '-') {
				if (pos < equalPos)
					plus = true;
				else
					plus = false;
				++pos;
			}
			else if (equation[pos] == '=') {
				++pos;
				if (equation[pos] == '+' || equation[pos] == '-') continue;
				if (pos >= equation.size()) break;
				plus = true;
			}

			int i = pos;
			while (i < equation.size() && equation[i] >= '0' && equation[i] <= '9') {
				++i;
			}
			int num = stoi(equation.substr(pos, i - pos));
			if (plus) {
				sum += num;
			}
			else {
				sum -= num;
			}

			pos = i;
		}

		if (xnum == 0 && sum == 0) {
			return "Infinite solutions";
		}
		else if (xnum == 0 && sum != 0) {
			return "No solution";
		}
		else {
			return "x=" + to_string(sum / xnum);
		}
	}
};
```