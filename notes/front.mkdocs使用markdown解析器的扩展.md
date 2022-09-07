---
id: r4584xu4ztgz95ebxfvwu6f
title: Mkdocs使用markdown解析器的扩展
desc: ''
updated: 1662565912901
created: 1662565912901
isDir: false
---
默认情况下，mkdocs没有配置使用它的解析器python-markdown的扩展的。但其实它可以使用扩展来增加表现力和功能。

其中一个需要就是在markdown文档中添加一些html标签，比如需要把一个层级内的所有元素都包在一个标签内。原生的markdown没有提供这种语法。

```
<div>
# this head1
</div>
```
输入的效果是标签内的内容不解析

根据文档，可以在mkdocs的yml文件中配置使用扩展，其中一个扩展就是md_in_html。这个就可以解析标签内的md。

mkdocs.yml
```
markdown_extensions:
    - 'md_in_html' #注意要加引号
```

然后在md中使用如下语法，就可以为md文档加上结构了。


```
<div markdown='1'> # 注意官方文档推荐使用1这个参数。
# this head1
</div>
```

https://python-markdown.github.io/extensions/md_in_html/

https://www.mkdocs.org/user-guide/configuration/