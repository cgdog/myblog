---
title: leetCode Repeated DNA Sequences
tags:
  - Bit manipulation
  - leetcode
id: 437
categories:
  - algorithm
date: 2016-09-25 16:54:51
---

[Repeated DNA Sequences](https://leetcode.com/problems/repeated-dna-sequences/)

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

For example,

```
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
```



``` cpp
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        vector<int> m(26, 0);
        m['C'-'A'] = 1;
        m['G'-'A'] = 2;
        m['T'-'A'] = 3;
        set<int> words;
        set<string> res;
        int n = s.size();
        for (int i = 0; i < n-9; i++) {
            int val = 0;
            for (int j = i; j < i+10; j++) {
                val <<= 2;
                val |= m[s[j]-'A'];
            }
            if (words.count(val) == 0) {
                words.insert(val);
            } else {
                res.insert(s.substr(i,10));
            }
        }
        return res.empty()? vector<string>() : vector<string>(res.begin(), res.end());
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/8894/clean-java-solution-hashmap-bits-manipulation](https://discuss.leetcode.com/topic/8894/clean-java-solution-hashmap-bits-manipulation)

**Other helpful links:**

[https://discuss.leetcode.com/topic/27517/7-lines-simple-java-o-n](https://discuss.leetcode.com/topic/27517/7-lines-simple-java-o-n)

[https://discuss.leetcode.com/topic/51018/concise-and-simple-c-code](https://discuss.leetcode.com/topic/51018/concise-and-simple-c-code)

[https://discuss.leetcode.com/topic/18263/10-lines-c-code-8-ms-passed](https://discuss.leetcode.com/topic/18263/10-lines-c-code-8-ms-passed)

[https://discuss.leetcode.com/topic/8487/i-did-it-in-10-lines-of-c](https://discuss.leetcode.com/topic/8487/i-did-it-in-10-lines-of-c)