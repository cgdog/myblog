---
title: mybatis foreach
tags:
  - mybatis
id: 253
categories:
  - 数据库
date: 2016-06-10 16:07:17
---

在mybatis中，foreach主要和IN一起使用，用户在SQL中遍历一个集合(List或Array)。

foreach元素的属性主要有 item，index，collection，open，separator，close。

item表示集合中每一个元素进行迭代时的别名，index指 定一个名字，用于表示在迭代过程中，每次迭代到的位置，open表示该语句以什么开始，separator表示在每次进行迭代之间以什么符号作为分隔 符，close表示以什么结束。

collection属性是必须指定的，但是在不同情况下，该属性的值是不一样的，主要有一下3种情况：

1 如果传入的是单参数且参数类型是一个List的时候，collection属性值为list

2 如果传入的是单参数且参数类型是一个array数组的时候，collection的属性值为array

3 如果传入的参数是多个的时候，我们就需要把它们封装成一个Map了，当然单参数也可以封装成map，实际上如果你在传入参数的时候，在breast里面也是会把它封装成一个Map的，map的key就是参数名，所以这个时候collection属性值就是传入的List或array对象在自己封装的map里面的key

> 以上参考自：[http://blog.sina.com.cn/s/blog_6a0cd5e501011snl.html](http://blog.sina.com.cn/s/blog_6a0cd5e501011snl.html)

然而，我在使用时，发现传入多个参数时，并不需要封装成Map（和上面条3条不太一样，可能是mybatis版本不同吧），直接把collection属性的值设值为集合变量的名称即可(我用的集合是List<Integer>)。

Mapper.xml中代代码如下：



``` sql
<select id="getCaseFileByCaseIds" resultMap="resourceMap">
        SELECT
            my_resources_vw.id,
            my_resources_vw.resource_library_id,
            my_resources_vw.physical_path,
            my_resources_vw.format,
            my_resources_vw.open_tools,
            my_resources_vw.outside_link,
            my_resources_vw.description,
            my_resources_vw.title,
            my_resources_vw.file_size
        FROM
            my_resources_vw
        LEFT JOIN
            my_product_case_vw
        ON
        (   my_product_case_vw.id IN 
        <foreach collection="caseIdList" index="index" item="item" open="(" separator="," close=")">
            #{item}
        </foreach>
        AND
            my_product_case_vw.resource_library_id=my_resources_vw.resource_library_id
        )           
 </select>
```

mapper.java文件中的接口代码如下：



``` java
public List<MyResource> loadCaseFileByCaseId(@Param("compId") int compId, 
            @Param("caseIdList") List<Integer> caseIdList, @Param("langId") String langId);
```

mybatis中foreach也可以和where标签加IN一起使用。如下代码：



``` sql
<where>
     my_product_model_tb.id 
     IN
    <foreach collection="prodIDsList" item="item" index="index" open="(" separator="," close=")">#{item}</foreach>
</where>
```