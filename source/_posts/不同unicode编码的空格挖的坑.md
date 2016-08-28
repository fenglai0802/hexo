---
title: 不同unicode编码的空格挖的坑
date: 2016-08-04 17:33:14
categories: JS
tags:
    - 空白字符
    - 编码
---
前段时间在做搜索的时候，遇到一个关于空格的小问题，总结一下。

有时在文本值中会插入一些空格字符 （Unicode 字符集值 32 和 160） ，比如说标题之类的。当你对包含空格的值进行**排序、 筛选或搜索**时，这些字符有时会导致意外的结果。本次就是因为把数据存放在dom节点上，取出来做搜索的时候，发现编码发现了改变（从32变成了160），导致无法正确匹配。

> The non-breaking space (U+00A0 Unicode, 160 decimal, &nbsp;) is not the same as the space character (U+0020 Unicode, 32 decimal). Well, both of them seems to be a "space", but they are absolutely different characters.

这里的解决方案是：采用正则替换成统一字符，如下

		var s = ' ' // 假设这里是一个160的空格。
		var reg = new RegExp(String.fromCharCode(160),"gm");
		var 32sp = String.fromCharCode(32)
		s = s.replace(reg, 32sp);

后来重构代码，直接废除了将数据存在dom上这种方案，就更好了。

除了空格字符，非打印字符在进行**排序、 筛选或搜索**操作时，也可能会遇到这类问题，[参考](https://support.office.com/zh-cn/article/%E5%88%A0%E9%99%A4%E6%96%87%E6%9C%AC%E4%B8%AD%E7%9A%84%E7%A9%BA%E6%A0%BC%E5%92%8C%E9%9D%9E%E6%89%93%E5%8D%B0%E5%AD%97%E7%AC%A6-023f3a08-3d56-49e4-bf0c-fe5303222c9d)。要注意~
