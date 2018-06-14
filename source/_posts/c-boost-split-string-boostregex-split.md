---
title: 'c++ boost split string  boost::regex split'
tags:
  - boost
  - c++
  - string
id: 694
categories:
  - programming
date: 2016-11-15 15:10:43
---

Split string using boost::split.

```
string line("test\ttest2\ttest3");
vector<string> strs;
boost::split(strs,line,boost::is_any_of("\t"));

cout << "* size of the vector: " << strs.size() << endl;    
for (size_t i = 0; i < strs.size(); i++)
    cout << strs[i] << endl;
```

The output:

```
* size of the vector: 3
test
test2
test3
```

> Referece:[http://stackoverflow.com/questions/5734304/c-boost-split-string](http://stackoverflow.com/questions/5734304/c-boost-split-string)

Split string using boost::regex.

```
#include <iostream>
#include <boost/regex.hpp>

using namespace std;

int main(int argc)
{
   string s;
   do{
      if(argc == 1)
      {
         cout << "Enter text to split (or \"quit\" to exit): ";
         getline(cin, s);
         if(s == "quit") break;
      }
      else
         s = "This is a string of tokens";

      boost::regex re("\\s+");
      boost::sregex_token_iterator i(s.begin(), s.end(), re, -1);
      boost::sregex_token_iterator j;

      unsigned count = 0;
      while(i != j)
      {
         cout << *i++ << endl;
         count++;
      }
      cout << "There were " << count << " tokens found." << endl;

   }while(argc == 1);
   return 0;
}
```

> Reference:[http://www.boost.org/doc/libs/1_39_0/libs/regex/doc/html/boost_regex/ref/regex_token_iterator.html#boost_regex.ref.regex_token_iterator.examples](http://www.boost.org/doc/libs/1_39_0/libs/regex/doc/html/boost_regex/ref/regex_token_iterator.html#boost_regex.ref.regex_token_iterator.examples)