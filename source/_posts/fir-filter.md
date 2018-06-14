---
title: FIR filter 有限冲激响应
id: 158
categories:
  - signal processing
date: 2016-05-22 15:11:13
tags:
---

### Finite impulse response

In signal processing, a finite impulse response (FIR) filter is a filter whose impulse response (or response to any finite length input) is of finite duration, because it settles to zero in finite time. This is in contrast to infinite impulse response (IIR) filters, which may have internal feedback and may continue to respond indefinitely (usually decaying).

The impulse response (that is, the output in response to a Kronecker delta input) of an Nth-order discrete-time FIR filter lasts exactly N + 1 samples (from first nonzero element through last nonzero element) before it then settles to zero.

FIR filters can be discrete-time or continuous-time, and digital or analog.

> Reference:[https://en.wikipedia.org/wiki/Finite_impulse_response](https://en.wikipedia.org/wiki/Finite_impulse_response)

**有限冲激响应（Finite impulse response，缩写 FIR）**滤波器是数字滤波器的一种，简称FIR数字滤波器。这类滤波器对于脉冲输入信号的响应最终趋向于0，因此是有限的，而得名。它是相对于无限冲激响应（IIR）滤波器而言。由于无限冲激响应滤波器中存在反馈回路，因此对于脉冲输入信号的响应是无限延续的。

### 特性

有限冲激响应滤波器（FIR filter）的优点：

*   冲激响应（impulse response）为有限长：造成当输入数字信号为有限长的时候，输出数字信号也为有限长。
*   比无限冲激响应滤波器（IIR filter）较容易最佳化（optimize）。
*   线性相位（linear phase）：造成h(n)\,是偶对称（even）或奇对称（odd）且有限长。
*   一定是稳定的（stable）：因为Z变换（Z transform）后所有的极点（pole）都在单位圆内。

有限冲激响应滤波器（FIR filter）的缺点：

*   设计方式较无限冲激响应滤波器（IIR filter）不容易。

> 参考：[https://zh.wikipedia.org/wiki/%E6%9C%89%E9%99%90%E5%86%B2%E6%BF%80%E5%93%8D%E5%BA%94](https://zh.wikipedia.org/wiki/%E6%9C%89%E9%99%90%E5%86%B2%E6%BF%80%E5%93%8D%E5%BA%94)

Introduction to FIR filter

<iframe width="640" height="360" src="https://www.youtube.com/embed/NvRKtdrssFA" frameborder="0" allowfullscreen></iframe>

> https://www.youtube.com/watch?v=NvRKtdrssFA