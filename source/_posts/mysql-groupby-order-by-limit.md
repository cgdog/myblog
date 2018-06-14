---
title: mysql中where group by limit和order by的顺序
id: 246
categories:
  - 数据库
date: 2016-06-08 17:20:21
tags:
  - mysql
---

在mysql中同时使用limit关键字和order by关键字时，二者的顺序时先用order by,然后用limit。否则报语法错误。



``` sql
FROM
        table_t
WHERE XXX
GROUP BY 
        XX
HAVING xxx
ORDERBY XXX
LIMIT m,n;
```