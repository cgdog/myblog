---
title: 'leetcode: Valid Number'
id: 307
categories:
  - algorithm
date: 2016-07-13 20:10:08
tags:
  - leetcode
---

Validate if a given string is numeric.

Some examples:
```
"0" => true

" 0.1 " => true

"abc" => false

"1 a" => false

"2e10" => true
```
Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

各种坑。。。



``` cpp
class Solution {
public:
    bool isNumber(string s) {
        while(s[0]==' ') {
            s=s.substr(1);
        }
        while(s[s.size()-1]==' ') {
            s=s.substr(0,s.size()-1);
        }

        if (s[0]=='+' || s[0]=='-') {
            s=s.substr(1);
        }

        if (s.compare("")==0 || s.compare(".")==0 || s.compare("e")==0 || s.compare("E")==0 || s.compare(".E")==0 || s.compare(".e")==0 || s.compare("e.")==0||s.compare("E.")==0) {
            return false;
        }

        bool isDotCurred = false;
        bool isECurred = false;
        for (int i = 0; i < s.size(); i++) {
            if (s[i]=='.') {
                if (isECurred==true) {
                    return false;
                }
                if (isDotCurred== false) {
                    isDotCurred = true;
                } else {
                    return false;
                }
            } else if (s[i] == 'e' || s[i] == 'E') {
                if (isECurred == false && i!=0 && i!= (s.size()-1)) {
                    if ((i==1 && s[i-1]=='.')||(i==(s.size()-2) && s[i+1]=='.')) {
                        return false;
                    }
                    isECurred = true;
                } else {
                    return false;
                }
            } else if (i>0 && (s[i-1]=='e' || s[i-1]=='E')) {
                if (s[i]=='-' || s[i]=='+') {
                    if (i==s.size()-1) {
                        return false;
                    }
                    continue;
                } else if (!(s[i]>='0' && s[i]<='9')) {
                        return false;
                }
            } else if (!(s[i]>='0' && s[i]<='9')) {
                return false;
            }
        }
        return true;
    }
};
```