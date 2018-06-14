---
title: JPinyin一个汉字转拼音的Java开源类库
id: 175
categories:
  - java
date: 2016-05-28 14:42:00
tags:
---

做工程，有一个需求：把汉字或汉字字母的混合，转化成拼音。

有一个开源Java库可以满足要求:JPinyin

### Maven


``` html
<dependency>
       <groupId>com.github.stuxuhai</groupId>
       <artifactId>jpinyin</artifactId>
       <version>1.1.5</version>
</dependency>
```

### Usage


``` java
	String str = "你好世界";
    PinyinHelper.convertToPinyinString(str, ",", PinyinFormat.WITH_TONE_MARK); // nǐ,hǎo,shì,jiè
    PinyinHelper.convertToPinyinString(str, ",", PinyinFormat.WITH_TONE_NUMBER); // ni3,hao3,shi4,jie4
    PinyinHelper.convertToPinyinString(str, ",", PinyinFormat.WITHOUT_TONE); // ni,hao,shi,jie
    PinyinHelper.getShortPinyin(str); // nhsj
```

> 参考：[https://github.com/stuxuhai/jpinyin](https://github.com/stuxuhai/jpinyin)