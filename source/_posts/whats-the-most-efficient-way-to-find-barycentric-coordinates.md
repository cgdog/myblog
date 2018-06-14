---
title: What's the most efficient way to find barycentric coordinates?
id: 772
categories:
  - algorithm
date: 2016-12-29 22:53:31
tags:
  - CG
  - math
  - 计算几何
---

[http://gamedev.stackexchange.com/questions/23743/whats-the-most-efficient-way-to-find-barycentric-coordinates](http://gamedev.stackexchange.com/questions/23743/whats-the-most-efficient-way-to-find-barycentric-coordinates)

[https://en.wikipedia.org/wiki/Barycentric_coordinate_system](https://en.wikipedia.org/wiki/Barycentric_coordinate_system)

Transcribed from Christer Ericson's Real-Time Collision Detection (which, incidentally, is an excellent book):



``` cpp
// Compute barycentric coordinates (u, v, w) for
// point p with respect to triangle (a, b, c)
void Barycentric(Point p, Point a, Point b, Point c, float &u, float &v, float &w)
{
    Vector v0 = b - a, v1 = c - a, v2 = p - a;
    float d00 = Dot(v0, v0);
    float d01 = Dot(v0, v1);
    float d11 = Dot(v1, v1);
    float d20 = Dot(v2, v0);
    float d21 = Dot(v2, v1);
    float denom = d00 * d11 - d01 * d01;
    v = (d11 * d20 - d01 * d21) / denom;
    w = (d00 * d21 - d01 * d20) / denom;
    u = 1.0f - v - w;
}
```

This is effectively Cramer's rule for solving a linear system. You will not get much more efficient than this—if this is still a bottleneck (and it might be: it doesn't look like it's much different computation-wise than your current algorithm), you'll probably need to find some other place to gain a speedup.

Note that a decent number of values here are independent of p—they can be cached with the triangle if necessary.