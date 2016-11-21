layout: atom
title: grammar更改笔记
date: 2016-11-20 13:18:57
tags:
---
# Atom中文件识别默认语法修改

* *需求*：公司使用自己开发的css预处理器mcss来进行web样式开发，这类文件的后缀为.mcss，在Atom中无法识别，因此每次打开这类文件，都需要ctrl+shift+L选择语言(grammar)版本，通常会选择scss或者less来代替一下。重复度比较大。
* *思路*：解决这个问题有2个办法：一个就是写个Atom插件，让Atom可以识别mcss语言；另一个就是将就策略，让Atom自动用scss或者less的语法来识别.mcss文件。考虑到办法一短时间无法实现（好吧，其实是因为菜），这里先用方法二处理下，后续有缘再进行插件的开发。

## Atom语法介绍

加载了一个文件以后，Atom会做一些事情来试图识别出文件的类型。大部分情况下，Atom 会通过文件的扩展名（.md 通常是一个 Markdown 文件，等等）来完成这项工作，但有时只通过扩展名难以判断，它会对文件内容进行一些检查来确定。

如果加载了一个 Atom 无法判断语法的文件，它会默认为是最简单的纯文本类型（Plain Text）。如果它把文件默认为纯文本，或者弄错了文件类型，再或者由于一些原因你想修改文件的当前作用语法，可以按下 ctrl-shift-L 调出语法选择器。

![](./images/Atom中文件识别默认语法修改/grammar.png)

一旦手动修改了一个文件的语法，Atom会记住它，除非你将语法设置回自动检测，或者手动选择一个不同的语法。

语法选择器的功能在 [atom/grammar-selector](https://github.com/atom/grammar-selector) 这个 package 里实现。

## 实现

在Atom的配置文件夹目录下有一个init.coffee的文件，用于做Atom初始化设置。

在其中添加代码

    # add ".mcss" to SCSS grammar:
    for grammar of atom.grammars.grammars
      if grammar.name is "Less"
        grammar.fileTypes.push('mcss')
    atom.grammars.onDidAddGrammar (grammar) ->
      if grammar.name is "Less"
        grammar.fileTypes.push('mcss')

表示在Less的语法中，添加识别文件类型mcss。从而使mcss文件能够被当做Less识别
