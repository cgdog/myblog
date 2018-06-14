---
title: Hello world C++ Policy-Based class Design
id: 648
categories:
  - programming
date: 2016-10-28 16:08:34
tags:
  - C++
---


``` cpp
template<
    typename output_policy,
    typename language_policy
>
class HelloWorld
  : public output_policy,
    public language_policy
{
    using output_policy::Print;
    using language_policy::Message;

public:

    //behaviour method
    void Run()
    {
        //two policy methods
        Print( Message() );
    }

};

#include &lt;iostream>

class HelloWorld_OutputPolicy_WriteToCout
{
protected:

    template&lt; typename message_type >
    void Print( message_type message )
    {
        std::cout &lt;&lt; message &lt;&lt; std::endl;
    }

};

#include &lt;string>

class HelloWorld_LanguagePolicy_English
{
protected:

    std::string Message()
    {
        return "Hello, World!";
    }

};

class HelloWorld_LanguagePolicy_German{
protected:

    std::string Message()
    {
        return "Hallo Welt!";
    }

};

int main()
{

/* example 1 */

    typedef
        HelloWorld&lt;
            HelloWorld_OutputPolicy_WriteToCout,
            HelloWorld_LanguagePolicy_English
        >
            my_hello_world_type;

    my_hello_world_type hello_world;
    hello_world.Run(); //returns Hello World!

/* example 2 
 * does the same but uses another policy, the language has changed
 */

    typedef
        HelloWorld&lt;
            HelloWorld_OutputPolicy_WriteToCout,
            HelloWorld_LanguagePolicy_German
        >
            my_other_hello_world_type;

    my_other_hello_world_type hello_world2;
    hello_world2.Run(); //returns Hallo Welt!
}
```

> Reference:[https://en.wikipedia.org/wiki/Policy-based_design](https://en.wikipedia.org/wiki/Policy-based_design)