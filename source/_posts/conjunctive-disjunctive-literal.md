---
title: 合取(conjunctive) 析取(disjunctive) 合取范式(CNF) 析取范式(DNF) 文字(literal) 原子公式
id: 239
categories:
  - math
date: 2016-06-04 16:54:30
tags:
---

### 合取范式

在布尔逻辑中，一个公式是合取范式(CNF)的，如果它是子句的合取。

和析取范式(DNF)中一样，在 CNF 公式中可以包含的命题连结词是与、或和非。非算子只能用做文字的一部分，这意味着它只能在命题变量前出现。

例如，下列所有公式都是 CNF: $$ {\displaystyle A\wedge B} {\displaystyle \neg A\wedge (B\vee C)} {\displaystyle (A\vee B)\wedge (\neg B\vee C\vee \neg D)\wedge (D\vee \neg E)} {\displaystyle (\neg B\vee C)}$$ 而下列不是:

$${\displaystyle \neg (B\vee C)} {\displaystyle (A\wedge B)\vee C} {\displaystyle A\wedge (B\vee (D\wedge E))}$$ 上述三个公式分别等价于合取范式的下列三个公式:

$${\displaystyle \neg B\wedge \neg C} {\displaystyle (A\vee C)\wedge (B\vee C)} {\displaystyle A\wedge (B\vee D)\wedge (B\vee E)}$$ 所有命题公式都可以转换成 CNF 的等价公式。这种变换基于了关于逻辑等价的规则: 双重否定律、德·摩根定律和分配律。

> 参考：[维基百科合取范式](https://zh.wikipedia.org/wiki/%E5%90%88%E5%8F%96%E8%8C%83%E5%BC%8F)

### 子句

在逻辑中，子句是文字的析取，在命题逻辑中，子句通常写做如下，这里的符号 {\displaystyle l_{i}} 是文字:

${\displaystyle l_{1}\vee \cdots \vee l_{n}}$ 在某些情况下，子句被写为文字的集合，所以上述子句将被写为 ${\displaystyle {l_{1},\ldots ,l_{n}}}$ 。从上下文中得到提示把这个集合解释为它的元素的析取。子句可以为空；在这种情况下，它是文字的空集。空字句被指示为各种符号比如 ${\displaystyle \emptyset }$ 、 ${\displaystyle \bot }$ 或 ${\displaystyle \Box }$ 。空字句的真值求值总是 ${\displaystyle false}$。

> 参考：[维基百科子句](https://zh.wikipedia.org/wiki/%E5%AD%90%E5%8F%A5_(%E9%80%BB%E8%BE%91))

### 文字 (数理逻辑)

在数理逻辑中，文字(literal)是一个原子公式(atom)或它的否定。文字可以分为两种类型:

肯定文字就是一个原子。 否定文字是一个原子的否定。 纯文字是其变量(在某个公式内)的所有出现都有相同符号的文字。

### 析取

逻辑或（logic or）又称逻辑**析取**（logic disjunction）、逻辑选言，是逻辑和数学概念中的一个二元逻辑算符。其运算方法是：如果其两个变量中有一个真值为“真”，其结果为“真”，两个变量同时为假，其结果为“假”。

> 参考：[维基百科](https://zh.wikipedia.org/wiki/%E9%80%BB%E8%BE%91%E6%88%96)

### 合取

基本符号： ${\displaystyle \land }$ 英文名：logical conjunction 中文名：逻辑与，**合取**，交集，按位与，逻辑乘，与门，... 命题逻辑中的二元连接词合取，是一个两元算子，集合论中的交集算子，二进制中的逻辑乘算子，按位与（Bitwise AND），逻辑门中的“与”门（AND gate），编程语言中的&amp;或and运算符等等。

> 参考：[维基百科](https://zh.wikipedia.org/wiki/%E9%80%BB%E8%BE%91%E4%B8%8E)

### 原子公式

在数理逻辑中， 原子公式或原子是没有子公式的公式。把什么公式当作原子依赖于所使用的逻辑。例如在命题逻辑中，唯一的原子公式是命题变量。

原子是在逻辑系统中"最小"的公式。在逻辑系统中的合式公式通常通过识别所有有效的原子公式，和给出从两个原子公式建立公式的规则而递归的定义。从原子公式制作的公式是复合公式。

例如，在命题逻辑中你有如下的公式构造规则:

任何命题变量 p 是合式原子公式。 给定任何公式 A，否定 ¬A ("非 A") 是合式公式。 给定任何两个公式 A 和 B，合取 A ∧ B ("A 与 B") 是合式公式。 给定任何两个公式 A 和 B，析取 A ∨ B ("A 或 B") 是合式公式。 给定任何两个公式 A 和 B，蕴涵 A ⇒ B ("A 蕴涵 B ") 是合式公式。 所以，我们可以建造任意的复杂的复合公式，比如，从简单的原子公式p、q 和 r 和我们的构造规则构造出 ((p ∧ ¬(q ⇒ r)) ∨ ¬p)。

> 参考：[维基百科](https://zh.wikipedia.org/wiki/%E5%8E%9F%E5%AD%90%E5%85%AC%E5%BC%8F)

### 析取范式

在布尔逻辑中，析取范式(DNF)是逻辑公式的标准化（或规范化），它是**合取子句(和“子句不一样？？”)**的析取。

一个逻辑公式被认为是 DNF 的，当且仅当它是一个或多个文字的一个或多个合取的析取。同合取范式（CNF）一样，在 DNF 中的命题算子是与、或和非。非算子只能用做文字的一部分，这意味着它只能领先于命题变量。例如，下列公式都是 DNF:

$${\displaystyle A\lor B} {\displaystyle A!} {\displaystyle (A\land B)\lor C} {\displaystyle (A\land \neg B\land \neg C)\lor (\neg D\land E\land F)}$$ 但如下公式不是 DNF:

${\displaystyle \neg (A\lor B)}$ NOT 是最外层的算子 ${\displaystyle A\lor (B\land (C\lor D))}$ 一个 OR 嵌套在一个 AND 中 把公式转换成 DNF 要使用逻辑等价，比如双重否定除去、德·摩根定律和分配律。注意所有逻辑公式都可以转换成析取范式。但是，在某些情况下转换成 DNF 可能导致公式的指数性爆涨。例如，在 DNF 形式下，如下逻辑公式有 2n 个项：

$${\displaystyle (X_{1}\lor Y_{1})\land (X_{2}\lor Y_{2})\land \dots \land (X_{n}\lor Y_{n})}$$