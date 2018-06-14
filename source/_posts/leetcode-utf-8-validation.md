---
title: leetCode UTF-8 Validation
tags:
  - Bit manipulation
  - leetcode
id: 430
categories:
  - algorithm
date: 2016-09-24 21:00:03
---

[UTF-8 Validation](https://discuss.leetcode.com/category/516/utf-8-validation) A character in UTF8 can be from 1 to 4 bytes long, subjected to the following rules:

> For 1-byte character, the first bit is a 0, followed by its unicode code.
> 
> For n-bytes character, the first n-bits are all one's, the n+1 bit is 0, followed by n-1 bytes with most significant 2 bits being 10.

This is how the UTF-8 encoding would work:

<pre>Char. number range  |        UTF-8 octet sequence
      (hexadecimal)    |              (binary)
   --------------------+---------------------------------------------
   0000 0000-0000 007F | 0xxxxxxx
   0000 0080-0000 07FF | 110xxxxx 10xxxxxx
   0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx
   0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
</pre>

Given an array of integers representing the data, return whether it is a valid utf-8 encoding.

Note:

The input is an array of integers. Only the least significant 8 bits of each integer is used to store the data. This means each integer represents only 1 byte of data.

Example 1:

<pre>data = [197, 130, 1], which represents the octet sequence: 11000101 10000010 00000001.
Return true.
It is a valid utf-8 encoding for a 2-bytes character followed by a 1-byte character.
</pre>

Example 2:

<pre>data = [235, 140, 4], which represented the octet sequence: 11101011 10001100 00000100.
Return false.
The first 3 bits are all one's and the 4th bit is 0 means it is a 3-bytes character.
The next byte is a continuation byte which starts with 10 and that's correct.
But the second continuation byte does not start with 10, so it is invalid.
</pre>



``` cpp
class Solution {
public:
    bool validUtf8(vector<int>& data) {
        int count = 0;
        int n = data.size();
        while (count < n)
        {
            int pre_count = count;
            if (count + 1 <= n && (data[count] & 0x00000080) == 0) {
                count++;
            }
            else if (count + 2 <= n && ((data[count] & 0x000000E0) >> 5 == 6) && (((data[count+1] & 0x000000C0) >> 6) == 2)) {
                count += 2;
            }
            else if (count + 3 <= n && ((data[count] & 0x000000F0) >> 4 == 14) && (((data[count+1] & 0x000000C0) >> 6) == 2 && ((data[count+2] & 0x000000C0) >> 6) == 2)) {
                count += 3;
            }
            else if (count+4 <= n && ((data[count] & 0x000000F8) >> 3 == 30) && (((data[count+1] & 0x000000C0) >> 6) == 2 && ((data[count+2] & 0x000000C0) >> 6) == 2 && ((data[count+3] & 0x000000C0) >> 6) == 2)) {
                count+=4;
                continue;
            }
            if (pre_count == count) {
                return false;
            }
        }

        return true;
    }
};
```

实际上, 0x00000080 == 0x080，所以上述代码data[count] & 0x00000080) == 0，可以写成data[count] & 0x080) == 0;其它类似修改。

> Reference:[https://discuss.leetcode.com/topic/60274/c-a-accepted-naive-algorithm](https://discuss.leetcode.com/topic/60274/c-a-accepted-naive-algorithm)

上述解法，是我自己想出的,比较naive，beats 82.55% 。

另一个非常简洁的解法见如下：



``` cpp
class Solution {
public:
    bool validUtf8(vector<int>& data) {
        int count = 0;
        for (auto c : data) {
            if (count == 0) {
                if ((c >> 5) == 0b110) count = 1;
                else if ((c >> 4) == 0b1110) count = 2;
                else if ((c >> 3) == 0b11110) count = 3;
                else if ((c >> 7)) return false;
            } else {
                if ((c >> 6) != 0b10) return false;
                count--;
            }
        }
        return count == 0;
    }
};
```

> Reference:<[https://discuss.leetcode.com/topic/57195/concise-c-implementation](https://discuss.leetcode.com/topic/57195/concise-c-implementation)>