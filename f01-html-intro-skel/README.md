# 1. HTML 骨架

## 大纲

* 什么是超文本
* HTML 基础结构
    - 标签
    - Doctype
    - 字符集
    - 页面骨架


## 讲义

我们通常讲的 "做网页", 其实就是想办法让 **浏览器** 这个软件, 按照我们的意愿, 去显示一些内容, 去实现一些交互动作. 那么我们做网页也要按照浏览器世界的基本法, 遵循标准去撰写我们的内容. 这些标准中, 我们首先要掌握的, 就是网页所使用的语言, **HTML** (Hypertext Markup Language, 超文本标记语言). 这就像你和中国人说话会用汉语, 和美国人说话会用英语一样, HTML 作为定义页面结构, 提供页面内容的语言, 自然要首先了解.

首先我们碰到一个术语, "超文本". 什么叫超文本? 通俗一点讲, 就是用文本自身来描述文本, 在文本内部构造出高于其自身的结构. 比如 `<em>这段话被强调</em>`, 里面的尖括号括起来的标签对本身也是文本, 却描述了其内含文本的额外信息. 这就是我们使用标记语言, 以单一文本的形式撰写丰富多彩的网页内容的哲学基础.

于是我们可以开始涉及基本的 HTML 结构了. 首先, 请在脑内形成一个人的形象.

好的, 我们观察这个人的形象, ta 有脑袋有身子 (显然), 这和 HTML 页面的基础结构非常类似. 实际上一个 HTML 页面的基本结构就是:

```html
<html>
  <head>
    <title>标题</title>
  </head>

  <body>
    <!-- 内容 -->
  </body>
<html>
```

如上的代码并不是一个严谨的 HTML 骨架, 但这并不妨碍我们观察得出一些关于 HTML 的重要感性认识:

* `<!-- ... -->` 是注释, 内容会被忽略 (内容不能出现两个连续的 `-` 字符, 这里略过)
* 标签一般是成对出现的 (有例外, 之后会涉及)
* 可以嵌套, 方式就是直接嵌入

关于嵌套, 有必要多说两句, 这里的嵌套要求开/闭标签严格对应. 形如

```html
<!--
  注意: 一般不推荐直接使用 <b> <i> 等标签指定样式, 这是上世纪的过时做法.
  当代 Web 开发一般通过指定语义 (如 <em> <strong> 分别表示 "强调" "重要")
  并为相应元素赋予样式的方法做内容设计.
  此处使用 <b> <i> 标签只是为了说明方便, 而且此处的字体风格并不承载更多语义.
-->
<b>粗体<i>粗斜体</b>斜体</i>
```

的代码虽然能在浏览器中正常显示 (术语: **渲染**), 但这是浏览器为了不至于 break the web 而做出的妥协, 或者叫容错处理. 浏览器看到这样的代码, 处理流程实际上是类似于下面这样:

```html
<b>粗体<i>粗斜体
<!-- </b>... 诶, 为什么没有闭合 <i> 就先闭合 <b> 了? 我就脑补 -->
</i>
<!-- 脑补结束 -->
</b>
<!-- 刚才是不是有个 <i>... 按照作者的意思, ta 应该还不希望 <i> 闭合吧 -->
<i>
<!-- 脑补又结束 -->
斜体</i>
```

实际上被渲染的内容是

```html
<b>粗体<i>粗斜体</i></b><i>斜体</i>
```

这样的正确嵌套方式.

(插曲: 我们在之后的前端学习中, 会碰到无数次 "兼容" "妥协" 之类的思维方式. 要知道整个互联网上的页面里 99% 都是不规范的; 在 HTML 的范畴里, 如果浏览器拒绝渲染不规范的页面, 那几乎没有页面会被正常显示. 而造成的结果呢? 人们会淡定地换用能够正常显示页面的浏览器; 原因就是 "-- XXX 软件的 YYY 功能不好用!  -- 那就换个软件吧!" 的小白思路.)

回到主题, 我们通过设想一个有脑袋有身子的人, 来类比地认识 HTML 页面的骨架. 这样一个人有 head, 有 body, 你把这些特征描述出来: "这个物体啊, 是个 html, 有 head, 有 body, head 里头有 title, ...", 但是这样就有一个问题 -- 你就确定对面知道你说的是人吗? 有 head 有 body 的东西多了去了. 实际上, 回到 HTML 的话题, 就算是 HTML 标准, 前前后后也出了很多版本, 不说清楚的话是会出问题的. 比方说:

* 有些标签 (主要是一些历史上曾经辉煌一时的标签, 比如 `<frameset>` `<font>` 之类) 只在某几个 HTML 版本中支持;
* 不同 HTML 版本对语法的要求严格程度不一, 比如 XHTML 系列对语法的要求就比 HTML 严格得多 (因为 XHTML 是基于 XML 定义的).

于是为了开门见山地说清楚我们希望采用的 HTML 版本, 我们就使用 **DOCTYPE**, 文档类型, 来把这条信息传达给浏览器. 因为是初学, 我们只需要记住 HTML5 的 doctype:

```html
<!DOCTYPE html>
```

对 HTML5 而言, 大小写是无所谓的; 而像上面这样的大小写是标准的形式. (具体的内容参见 [HTML5 规范的有关章节][html5-syntax-doctype].) 因为是开门见山, 开宗明义, 所以 DOCTYPE 的位置是出现在 `<html>` 标签之前, 位于整个页面的开头.

[html5-syntax-doctype]: http://www.w3.org/TR/html5/syntax.html#the-doctype

好的, 解决了 DOCTYPE 的问题, 我们还有一个重要的属性, **编码** (charset 字符集; character/text encoding 字符/文本编码). 在互联网的洪荒时代, 计算机系统之间基本上没有大规模的互联, 常见的情景最多就是一座建筑里的机器互联. 于是, 当时的计算机系统一般而言并不需要处理多语言多文化的信息. 加上当年的机器内存外存容量与现在相比都很小, 一般的系统也没有能力支持多种语言多种文字. 因此早期的文字信息并没有采用 Unicode 编码, 而是以各个国家/地区专用的文字编码储存, 并用这种形式被处理. 可以想像, 如果不用某种手段声明一段字节流的编码, 那在理解上势必会出现各种问题, 比如经典的:

```
   汉字:    曹     操
Unicode:  U+66F9 U+64CD
   Big5:  b1 e4  be de

GB18030:  b1 e4  be de
Unicode:  U+53D8 U+5DE8
   汉字:    变     巨
```

Big5 是台湾地区的传统字符集, GB18030 是中国大陆的传统字符集 GB2312/80 的最新修订. 我们清楚地看到, 如果在字节流层面没有明确的编码声明的话, 我们便无法唯一地确定该字节流实际承载的文本. 这在理论上和实际上会造成一些后果:

* 页面无法正常加载 (最好的结果, 因为马上会被发现, 并被修复);
* 页面出现乱码 (相对而言算好的结果, 关键词 `锟斤拷` 可自行搜索);
* 造成不必要的网络请求, 增加网络流量, 延长页面加载时间 (不展开分析, 不过原理是页面上图片等资源的地址可能因为浏览器 **猜测** 的编码变化而变化);
* 造成安全漏洞 (最坏的结果, 关键词 `UTF-7`).

因此我们本着负责任的态度, 势必不能容忍不指定页面编码的行为. 现在使用最广泛的编码是 **UTF-8**, 支持多语言; 使用 UTF-8 编码的声明形式如下:

```html
<!-- 位于 <head> 标签内 -->
<meta charset="utf-8" />
```

从这里我们可以看到一些知识点:

* 描述页面信息的元数据用 `<meta>` (元) 标签, 这个标签只能出现在 `<head>` 中
* meta 属性 `charset` 用来声明该页面字节流的编码
* HTML 中大多数标签可以带属性, 语法就是 `name="value"` (最标准的形式; 其他形式以后会涉及). 标签和属性之间, 还有属性与属性之间, 使用空格分开.
* 有的标签不带内容 (tag body), 写法形如 `<tag attr1="val1" attr2="val2" />`, 这是所谓 self-enclosing tags. HTML5 中最后的 `/>` 可以省略斜杠.

于是我们得到一个比较严谨的 HTML 页面骨架:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title></title>
</head>
<body>
</body>
</html>
```

编码/字符集的声明放在页面标题之前, 这是前端开发最佳实践: 使浏览器尽早接收, 也就相当于明确下来, 接下来如何解码后续的内容 (字节流). 既然 charset 必须出现在 `<head>` 标签打开之后, 那么最为紧凑的 HTML 头部就必须撰写成如上的形式 (在省略了换行和允许省略的空格之后).


## 教学细节问题

*TODO*


<!-- vim:set ai et ts=4 sw=4 sts=4 fenc=utf-8: -->
