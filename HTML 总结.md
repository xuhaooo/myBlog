# HTML 总结

# 一、HTML 是什么

## 1. 什么是 HTML

HTML 全名叫做“超文本标记语言”（HyperText Markup Language），是由 Tim Berners-Lee 发明的一种网页标记语言，用于定义网页的结构和内容。我们使用浏览器访问网站，就是从服务器下载 HTML 代码，然后渲染出页面，HTML 最大的特点就是支持超链接，可以点击跳转到其他网页，而因为这个特点产生了如今的互联网。

一个简单的 HTML 源码如下：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
	<meta charset="utf-8">
	<title>网页标题</title>
</head>
<body>
	<p>Hello World</p>
</body>
</html>
```

## 2. 网页的基本概念

### 2.1 标签的功能、构成与分类

```html
<title>网页标题</title>
```

功能

网页的 HTML 代码是由许多不同的标签构成，学习 HTML 就是学习各种标签的用法

标签用来告诉浏览器，如何处理这段 HTML 代码；标签的内容就是浏览器所渲染展示到页面上的内容

构成

标签一般是由一个开始标签和一个结束标签构成，加 / 表示结束标签；但是也有一些标签是单独出现的，如

```html
<meta charset="utf-8">
```

这种单独使用的标签，通常是因为标签本身就可以完成功能，不需要标签之间的内容，实际应用中，它们主要用来提示浏览器做一些特别处理

标签是可以嵌套的，但是注意不能跨层嵌套同时也要注意成对标签的闭合

标签名大小写不敏感，但一般使用小写

### 2.2 元素与标签

浏览器渲染网页时，会把 HTML 源码解析成一个标签树，每个标签都是树的一个节点（node），这种节点称为网页元素（element）。因此“标签”与“元素”是同义词，只不过使用场合不一样：标签是从源码角度来看，元素是从变成角度来看，比如 `<p>` 标签对应就是网页的 `p` 元素

标签的嵌套构成了网页的层级关系，比如下面代码中，p 元素就是其“父元素” div 元素的”子元素“

```html
<div><p>Hello World</p><div>
```

### 2.3 块级元素、行内元素

所有元素可以分为 2 大类：块级元素（block）、行内元素（inline）

块级元素，默认占据独立一行，在网页中显示会自动另起一行，占据 100% 宽度

行内元素与其他元素显示在同一行，不换行

```html
<p>Hello</p>
<p>World</p>

<span>Hello</span>
<span>World</span>
```

### 2.4 属性名大小写

属性是标签的额外信息，使用空格与标签名和其他属性分隔，使用等号指定属性值，HTML 提供大量的属性，用来定制标签的行为

注意，属性名是大小写不敏感的，`onclick` 和 `onClick` 是同一个属性

```html
<img src="demo.jpg" width="300">
```

## 3. 网页的基本标签

### 3.1 <!DOCTYPE>

通常是网页的第一个标签，表示文档的类型，告诉浏览器如何解析网页

如今我们一般直接声明文档类型为 `html`，浏览器会按照 HTML5 的规则处理网页

```html
<!DOCTYPE html>
```

### 3.2 <html>

`<html>` 是网页的顶层容器，即标签树结构的顶层节点，也称为根元素，其他元素都是它的子元素，一个网页只能有一个 `<html>` 标签

该标签的 `lang` 属性，表示网页内容默认的语言；下面代码表示网页是中文内容，将 `zh-CN` 改为 `en` 表示网页是英文内容

```html
<html lang="zh-CN">
</html>
```

### 3.3 <head>

`<head>` 标签是一个容器标签，用于防止网页的元信息，它的内容不会出现在网页上，而是为网页渲染提供额外信息。它是 `<html>` 的第一个子元素，如果没写，浏览器会自动创建一个

`<head>` 的子元素一般有下面 7 个：

- `<meta>`：设置网页的元数据
- `<link>`：连接外部样式表
- `<title>`：设置网页标题
- `<style>`：设置内嵌的样式表
- `<script>`：引入脚本
- `<noscript>`：浏览器不支持脚本时，所要显示的内容
- `<base>`：设置网页内部相对 URL 的计算基准

### 3.4 <meta>

`<meta>` 标签用于设置或说明网页的元数据，必须放在 `<head>` 中，一个该标签就是一项元数据，网页可以有多个 `<meta>`

所有的网页，一般都可以写下面 2 个 `<meta>`，第一个表示网页字符采用 UTF-8 格式编码，第二个表示网页在手机端可以自动缩放

```html
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Page Title</title>
</head>
```

`<meta>` 有 5 个属性：

charset

用于指定网页的编码方式

注意声明的编码格式应该与网页文件保存的编码格式相同，否则可能会乱码

name、content

`name` 属性表示元数据的名称，`content` 属性表示元数据的值，结合使用就可以为网页指定一个元数据

```html
<head>
  <meta name="description" content="HTML 语言入门">
  <meta name="keywords" content="HTML,教程">
  <meta name="author" content="张三">
</head>
<!-- description 是网页内容的描述，keywords 是网页内容的关键词，author 是网页作者 -->
```

http-equiv、content

`http-equiv` 属性用来覆盖 HTTP 响应头信息字段，`content` 属性是对应字段内容

### 3.5 <title>

`<title>` 标签用于指定网页的标题，会显示在浏览器窗口的标题栏

### 3.6 <body>

`<body>` 标签是一个容器标签，用于放置网页的主体内容，浏览器显示的页面内容都是放置在其内部

## 4. HTML 的空格处理规则

HTML 有自己的空格处理规则，标签内容的头部、尾部空格一律忽略不计，标签内容中的多个连续空格（包括制表符 `\\t`）会被浏览器合成一个空格，浏览器还会将文本中的换行符（`\\n`）和回车符（`\\r`）替换成空格

## 5. 注释

HTML 代码的注释以 `<!--` 开头，以 `—->` 结尾，支持多行注释

```html
<!-- 这是一个注释 -->
<!--
	这是一个多行注释
	<p>111</p>
	<p>222</p>
-->
```

# 二、URL

## 1. URL 是什么

URL 全称为“统一资源定位符”（Uniform Resource Locator），又称作网址，表示各种资源的互联网位置，比如：`https://www.example.com/path/index.html` 

资源，即各种可以通过互联网访问的文件，如网页、图像、音视频、JS 脚本等，只有知道了它们的 URL，才能在互联网上获取它们

一个 URL对应一个资源，但一个资源可以对应多个 URL

URL 是互联网的基础，之所以可以“互联”，是因为网页可以通过“链接”包含其他 URL，用户点击就可以通过一个 URL跳转到其他 URL，获取不同资源或者前往不同网站

## 2. 网址的组成部分

URL 由多个部分组成，比如下面就是一个较复杂的 URL

```html
https://www.example.com:80/path/to/index.html?key1=value1&key2=value2#anchor
```

### 2.1 协议

协议，是浏览器请求服务器资源的方法，上面的 `https://` 就表示使用了 HTTPS 协议

浏览器默认使用的时候 HTTP 协议，HTTPS 是 HTTP 的加密版本

后面的 `://` 不是所有的协议都是如此，比如邮件地址协议是 `mailto:xxx@yyy.com`

### 2.2 主机

主机，是资源所在的网站名或服务器的名字，又称域名，比如上面的 `[www.example.com](http://www.example.com)` ，有些主机没有域名，只有 IP 地址如 `192.168.2.23` ，这种情况常出现在局域网

### 2.3 端口

同一个域名下面可能包含多个网站，它们通过“端口”区分，端口是一个整数，可以理解成访问者告诉服务器想要访问那个网站。浏览器默认端口是 `80`

### 2.4 路径

路径是资源在网站的位置，比如上面的 `/path/index.html`，就是指向网站的 `/path` 子目录下面的网页文件 `index.html` 

路径可能只包含目录，不包含文件名，如 `/xxx/`，甚至尾部的 `/` 都可以省略。这时，服务器通常会默认跳转到该目录下的 `index.html` 文件（等同于请求 `/xxx/index.html`），当然也可能有其他的处理（如列出目录中的所有文件），取决于服务器的设置，一般来说访问 [`www.example.com`](http://www.example.com) 这个网址，很可能返回的是网页文件 `www.example.com/index.html`

### 2.5 查询参数

查询参数是提供给服务器的额外信息，参数的位置在路径后面，两者之间使用 `？`分隔

查询参数由一组或多组键值对构成，每组键值对同时具有键名和键值，使用 `=` 链接，多组参数间使用 `&` 连接，比如 `key1=value1&key2=value2`

### 2.6 锚点

锚点是网页内部的定位点，使用 # 加上锚点名称，位置位于网址最后，如 `#anchor`。浏览器加载页面后，会自动滚动到锚点所在的位置。锚点名称通过网页元素的 `id` 属性命名

## 3. URL 字符

URL 的各个部分只能使用字符：`a-z`、`A-Z`、`0-9`、`-`、`_`、`.` ，加上 18 个 URL 的保留字符，只能出现在给定位置上，比如 `?` 只能出现在查询参数的开头

如果想要在其他位置使用保留字、汉字怎么办？

那么如果网址的其他部分想要使用这些保留字符怎么办呢，必须使用他们的转译形式，转义方法是在这些字符的十六进制 ASCII 码前加上 `%`，比如 `xxx?index.html` 就需要写成 `xxx%3Findex.html` 。URL 合法字符如 `a-z` 也是可以使用转义写法的，但是不推荐，最后，空格的转义形式为 `%20` 

既不属于合法字符、也不属于保留字符的其他字符（如汉字），理论上不需要转义可以直接写在 URL 中，浏览器会自动将其转义发给服务器。转义方法是使用字符的十六进制 UTF-8 编码，2 位算一组，每组头部添加 `%` 

```html
<!-- www.expample.com/中国.html -->
www.example.com/%e4%b8%ad%e5%9b%bd.html
```

## 4. 绝对 URL 与相对 URL

URL 分两种：绝对 URL和相对 URL

绝对 URL，指的是只靠 URL 本身就能确定资源的位置，这就意味着 URL 必须带有资源的完整信息，包含协议、主机、路径等部分，前面的例子都是绝对 URL

相对 URL，指的是 URL 不包含资源位置的全部信息，必须结合当前网页的位置，才能定位资源。比如，当前网页 URL 为 `https://www.example.com/path/index.html`，网页上有个资源，URL 指向 `a.html`，这就是相对 URL，因为只知道 `a.html` 并不能定位资源，浏览器假定 `a.html` 与当前网页在同一个子目录下，从而得到绝对 URL `[https://www.example.com/path/a.html](https://www.example.com/path/a.html)` 

相对 URL 如果以 `/` 开头，就表示网站的根目录，否则必须以当前目录为起点推算资源位置

URL 还有 2 个特殊简写表示特定位置：

`.`：表示当前目录，如 `./a.html` 表示当前目录下的 `a.html` 文件

`..`：表示上级目录，如 `../a.html` 表示上级目录下的 `a.html` 文件，这种写法可以连用

## 5. <base>

`<base>` 标签指定网页内部的所有相对 URL 的计算基准，整个网页只能有一个 `<base>` 标签，且只能放在 `<head>` 中

```html
<head>
<base href="https://www.example.com/files/" target="_blank">
</head>
```

`href` 属性给出计算的基准网址，`target` 属性给出如何打开链接的说明，`<base>` 必须具备这 2 个属性中的一个

一旦设定对这个网页都有效，如果想要改变某个链接的行为只能使用绝对链接代替相对链接，注意，锚点也是针对 `<base>` 计算的而不是当前网页的 URL

# 三、网页元素的属性

## 1. 属性

网页元素的属性可以定制元素的行为，属性的写法是标签内部的键值对，比如 `<html lang="en">`

属性名与标签名一样，不区分大小写，`lang` 与 `LANG` 是同一个属性

有些属性是布尔属性（即属性值是布尔值），有和无两种状态，因此写了属性名即表示有该属性，不写就表示没有该属性，如 `<input type="text" required>`

## 2. 全局属性

所有的元素都可以使用，不过有些属性对某些元素可能不产生意义

### 2.1 id

`id` 属性是元素在网页中的唯一标识符，该属性的值必须是全局唯一的，即同一个页面不能有 2 个相同的 `id` 属性值，另外， `id` 属性值不能有空格

```html
<div id="div1"></div>
<div id="div2"></div>
<div id="div3"></div>
```

可以在 `id` 属性值之前加上 `#`，放到 URL 中作为锚点，定位到该元素在网页中的位置

### 2.2 class

`class` 属性用来对网页元素进行分类，如果不同元素的 `class` 属性值相同，则表示它们是一类的。一个元素可以同时具有多个 `class`，它们之间使用空格分隔

```html
<div class="div1 div2 div3"></div>
```

### 2.3 title

`title` 属性用来给元素添加附加说明，大多数浏览器中，鼠标悬浮在元素上，都会显示 `title` 属性值

```html
<img src="demo.jpg" title="一张图片">
```

### 2.4 style

`style` 属性用来指定当前元素的 CSS 样式

```html
<p style="color: red;">Hello World</p>
```

### 2.5 hidden

`hidden` 表示当前元素不再跟当前网页相关，因此浏览器就不会渲染这个元素，所以在网页中看不到该元素

注意，CSS 的可见性设置，优先级高于 `hidden` 属性，即如果使用 CSS 设置了元素可见那么 `hidden` 属性无效

### 2.6 lang，dir

`lang` 属性指定网页元素使用的语言，属性值如： `zh` 表示中文，`zh-Hans`表示简体中文，`en` 表示英语

`dir` 属性表示文字的阅读方向，属性值有：`ltr` 从左向右，`rtl` 丛右向左，`auto` 浏览器根据内容自行决定

### 2.7 contenteditable

HTML 网页内容默认是用户不能编辑的，`contenteditable` 属性允许用户修改内容，属性值有：`true` 或空字符串表示内容可编辑，`false` 表示不可编辑

```html
<p contenteditable="true">本段内容可以直接修改</p>
```

用户点击即可进行编辑，当然，除非提交到服务器，否则页面刷新还是显示原来的内容

### 2.8 data-

`data-` 属性用于给元素嵌入自定义属性或数据，通过 CSS 或 JS 进行使用

```html
<head>
	<style>
    #div1::before {
      content: attr(data-x);
    }
    div[data-xx="456"] {
      width: 100px;
      height: 100px;
      border: 1px solid red;
    }
  </style>
</head>
<body>
  <div
    id="div1"
    data-x="123"
    data-xx="456"
    data-xxx="789"
  >Hello World</div>
  <script>
    var div1 = document.querySelector('#div1')
    console.log(div1.dataset.xxx) // "789"
  </script>
</body>
```

### 2.9 事件处理属性

除了上述属性，全局属性还包括事件处理属性，用来响应用户的动作，这些属性的值都是 JS 代码，如 `onclick`、`onblur` 等等

# 四、HTML 字符编码

## 1. HTML 的字符编码

网页包含大量文字，浏览器必须知道这些文字的编码方法，才能把文字正确解析显示出来，一般情况下服务器向浏览器发送 HTML 网页文件时，会通过 HTTP 头声明网页的编码方式

```jsx
Content-Type: text/html; charset=UTF-8
```

HTTP 头信息的 `Content-Type` 字段先声明，服务器发送的数据类型是 `text/html` 即 HTML 网页，然后声明网页文字编码为 `UTF-8`

网页内部也会再用 `<meta>` 再次声明网页的编码

```html
<meta charset="UTF-8">
```

## 2. UTF-8

如今网页中最常用的编码为 UTF-8，UTF-8 编码是 Unicode 字符集的一种表达形式，这个字符集包含了世界上所有字符

每一个字符都有一个 Unicode 号码，称作码点，可以通过码点查到是什么字符，如 a 的码点是十进制 97（十六进制 61）

HTML 允许使用 Unicode 码点表示字符，浏览器会自动将码点转成对应字符，注意，HTML 标签本身不能使用码点表示

码点的表示法：`&#十进制码点`、`&#x十六进制码点`，如 a 可以写成 `&#97` 或 `&#x61`

## 3. 字符的实体表示

由于数字码点难以记忆，HTML 为一些特殊字符设置了容易记忆的名字，允许通过名字来表示这些字符

常用的字符写法有：

- `<`：`&lt;`
- `>`：`&gt;`
- `©`：`&copy;`
- 空格：`&nbsp;`

# 五、语义化

## 1. HTML 语义化

HTML 标签的一个重要作用，就是声明网页元素的性质，使得用户只看标签就能了解这个元素的意义，阅读源码就能了解网页的大致结构。语义良好的网页，天然具有良好的结构，对于开发者易读易写易维护，也能帮助计算机更好地处理网页内容

一个典型的语义结构的网页：

```html
<body>
	<header>页眉</header>
	<main>
	  <article>
	    <h1>文章标题</h1>
	    <p>文章内容</p>
	  </article>
	</main>
	<footer>页尾</footer>
</body>
```

## 2. 常用语义化标签

### 2.1 <header>

既可以表示整个网页的头部，也可以表示一篇文章或一个区块的头部

### 2.2 <footer>

表示网页、文章、章节的尾部，如果用于整个网页的尾部，称为“页尾”，通常包含版权信息或其他相关信息

### 2.3 <main>

表示页面的主体内容，一个页面只能有一个 `<main>`

`<main>` 是顶层标签，不能写在 `<header>`、`<footer>`、`<article>`、`<aside>`、`<nav>` 等标签中

另外，功能性区块如搜索栏不适合放入 `<main>`

### 2.4 <article>

表示页面中一段完整的内容，通常用来表示一篇文章或一个论坛的帖子，它可以有自己的标题

### 2.5 <aside>

用来放置与网页或文章主要内容间接相关的部分，网页级的 `<aside>` 可以用来放置侧边栏，文章级的 `<aside>` 可以用来放置评论或注释

### 2.6 <section>

表示含有主题的独立部分，通常用在文档中表示一个章节，比如 `<article>` 可以包含多个 `<section>`，当然，一个 `<section>` 中也可以有多个 `<article>` 这个取决于在当前页面的含义，另外，一般来说 `<section>` 都应该有标题

### 2.7 <nav>

用于放置页面或文档的导航信息，往往放置在 `<header>`中，当然，一个页面中可以有多个 `<nav>`，比如一个用于站点导航一个用于文章导航

### 2.8 <h1> - <h6>

表示文章的标题，浏览器默认粗体显示标题，同时字号逐级递减

### 2.9 <hgroup>

 如果主标题包含多级标题（比如带有副标题），可以使用 `<hgroup>` 将多级标题放置其中

注意，`<hgroup>` 只能包含 `<h1>`-`<h6>`

# 六、文本标签

## 1. <div>

`<div>` 是一个没有语义的通用标签，表示一个区块，如果网页需要一个块级元素容器且没有合适的标签，就可以使用它

早期通过层层包裹的 `<div>` 搭建页面结构，但是现在我们应该尽量使用 HTML5 的语义化块级标签

## 2. <p>

`<p>` 是一个代表文章段落的块级元素，当然不仅仅是文本，任何想要以段落显示的内容，如图片、表单项，都可以放入 `<p>`

## 3. <span>

`<span>` 是一个不带语义的通用行内标签，如果网页需要一个行内元素，就可以使用它，我们主要使用它包裹某些行内内容并指定样式

## 4. <br>，<wbr>

`<br>` 是一个让网页产生换行效果的单标签，但是，块级元素的间隔不要使用 `<br>` 来产生，而应该使用 CSS 指定

`<wbr>` 跟 `<br>` 很相似，表示一个可选的换行，即如果一行的宽度如果够就不换行，如果宽度不够就在 `<wbr>` 的位置换行

## 5. <hr>

`<hr>` 是一个表示水平线的单标签，一般用来在一篇文章中分隔两个不同的主题，不过，在主题之间分隔现在可以使用 `<section>`，如果想要水平线效果，可以使用 CSS

## 6. <pre>

`<pre>` 是一个块级元素，表示保留原来的格式，即浏览器会保留标签内部原始的换行和空格

注意，`<pre>` 中的 HTML 标签还是起作用的，它只是保留空格和换行，不会保留 HTML 标签，下面代码中 `<pre>` 标签内容会加粗显示

```html
<pre><strong>hello world</strong></pre>
```

## 7. <strong>，<b>

这两个标签都是行内标签，标签内容都会加粗显示，只不过前者表示语义上内容的重要性，后者没有，应该尽量使用 `<strong>`

## 8. <em>，<i>

这两个标签都是行内标签，表示强调，标签内容会以斜体显示，只不过前者表示语义上的强调，应该尽量使用 `<em>`，但是，更推荐使用 CSS 设置字体为斜体

## 9. <sub>，<sup>

`<sub>` 标签将内容变成下标，`<sup>` 将内容变成上标，它们都是行内元素，主要应用于数学公式、分子式等

## 10. <u>，<s>

`<u>` 是一个行内元素，为内容加上下划线，可以用来提示拼写错误。但是由于 `<a>` 也默认带有下划线，所以为了避免混淆，尽量使用 CSS 来设置下划线样式

`<s>` 是一个行内元素，为内容加上删除线

## 11. <blockquote>，<cite>

`<blockquote>` 是一个块级元素，表示引用别人的话，浏览器会在样式渲染上与正常文本区分。它有一个 `cite` 属性，值是一个 `url`，表示引言的来源，并不会显示在网页上

`<cite>` 表示引言出处或作者，浏览器默认使用斜体显示内容，这个标签可以单独使用，不一定跟 `<blockquote>` 一起使用

## 12. <code>

`<code>` 是一个行内元素，表示一行代码，默认以等宽字体显示，如果要显示多行代码，需要将多个 `<code>` 放在 `<pre>` 内部

## 13. <kbd>

`<kbd>` 是一个行内元素，原意是用户从键盘输入的内容，现在扩展到各种输入，包括语音输入，默认等宽字体显示标签内容，多个 `<kbd>` 之间可以嵌套

```html
<p>Windows 中可以通过 <kbd>Ctrl</kbd> + <kbd>C</kbd> 来复制内容</p>
```

## 14. <address>

`<address>` 是一个块级元素，表示联系方式，一般结合 `<p> <a>` 在 `<footer>` 中使用

## 15. <abbr>

`<abbr>` 是一个行内元素，表示标签内容是一个缩写，它的 `title` 属性给出缩写的完整形式或描述，鼠标悬浮 `title` 值就会显示

## 16. <ins>，<del>

两个都是行内元素，`<ins>` 表示原来文档添加的内容，标签内容会加上下划线；`<del>` 表示删除的内容，标签内容会加上删除线

这两元素都有 `cite` 和 `datetime` 属性，分别表示可以解释本次修改的 `url` 以及删改发生的时间

# 七、列表标签

## 1. <ol>

`<ol>` 是一个有序列表容器，会在内部列表项前面生成数字编号，`<ol>` 可以嵌套 `<ol>` 和 `<ul>`，这样就形成了多级列表

它有以下几个属性：

- `reversed`，产生倒序数字列表
- `start`，指定数字列表的起始编号，如 `<ol start="3">`
- `type`，指定数字编号的样式，支持 a、A、i、I、1，如 `<ol type="a">`

注意，即使编号为字母，`start` 属性依旧可以使用整数，比如 `<ol type="a" start="3">` 表示编号从 `c` 开始

## 2. <ul>

`<ul>` 是一个无序列表容器，会在内部列表项前面生成实心圆点作为列表符号，同样的，它内部也可以嵌套 `<ul>` 或 `<ol>` 形成多级列表

## 3. <li>

`<li>` 作为列表项使用在 `<ol>` 或 `<ul>` 中

在 `<ol>` 中 `<li>` 具有 value 属性，指定其与后面列表项的编号，比如下面的列表项编号分别为 1、3、4

```html
<ol>
	<li> 列表项 1 </li>
  <li value="3"> 列表项 2 </li>
	<li> 列表项 3 </li>
</ol>
```

## 4. <dl>，<dt>，<dd>

`<dl>` 是一个块级元素，表示一组术语列表，其中术语名使用 `<dt>` 定义，术语解释使用 `<dd>` 定义，`<dt>`、`<dd>` 都是块级元素

# 八、图像标签

## 1. <img>

`<img>` 标签用于插入图片，是一个单标签，它默认是一个行内元素，与前后的文字处于同一行

图像默认是以原始大小显示的，同时它还可以放在 `<a>` 中得到一个可点击的链接图片

## 2. 属性

src：指定图片的地址

alt：设置图片的文字说明（图片无法显示时）

width、height：一旦设置浏览器就预留这个空间，无论图片是否加载成功，所以不建议使用；如果使用的话，一般只设置其中一个，这样浏览器会根据图片的原始大小自动设置另外一个值；可以通过`img {max-width: 100%;}` 设置图片使用手机屏幕

# 九、链接标签

## 1. <a>

链接通过 `<a>` 表示，用户点击浏览器就会跳转到指定的网址

`<a>` 标签内部不仅可以放置文字，段落、图片、多媒体等都是可以的

属性：

### 1.1 href

该属性指定链接指向的网址，它的值可以是 URL 或锚点

### 1.2 title

该属性给出链接的说明信息，当鼠标在链接上悬浮时会把该值显示出来

### 1.3 target

该属性指定如何展示打开的链接，它的值可以是：

- `_self`：当前窗口打开（默认值）
- `_blank`：新窗口打开
- `_parent`：上层窗口打开，这是相对于父窗口中打开的子窗口或 `<iframe>` 中的链接来说的，如果当前窗口没有上层窗口，那么这个值相当于 `_self`
- `_top`：顶层窗口打开，同上

### 1.4 rel

该属性说明链接与当前页面的关系，它的值可以是：`alternate`（当前文档的另一种形式，如翻译）、`author`、`license` 等

## 2. 邮件链接

链接也可以指向一个邮件地址，使用 `mailto` 协议，用户点击后浏览器会打开本机默认邮件程序，让用户向指定地址发送邮件

```html
<a href="mailto:contact@example.com">联系我们</a>
```

## 3. 电话链接

如果是手机浏览的页面，可以使用 `tel` 协议创建电话链接，用户点击链接就会唤起电话，可以进行拨号

```html
<a href="tel:123131312">1232312312</a>
```

## 4. <link>

`<link>` 主要用于将当前网页与相关的外部资源联系起来，通常放在 `<head>` 中，最常见的用途就是加载 CSS 样式表

当然 `<link>` 还有其他功能如：加载替代样式表、加载网站的 favicon、提供不同分辨率的图标文件等

属性：

href：提供外部资源的网址

rel：跟 `<a>` 一样，表示外部资源与当前文档之间的关系，是 `<link>` 标签必须的属性，它的值可以是 `alternate`、`icon`、`author`、`license`、`stylesheet` 等

## 5. <script>

`<script>` 用于加载脚本代码，当然主要是加载 JavaScript 代码，可以直接嵌入代码或者加载外部代码

```html
<script> console.log('Hello World') </script>
<script type="text/javascript" src="example.js"><script>
```

`type` 属性给出脚本的类型，默认是 JavaScript 代码，所以可以省略

# 十、多媒体标签

## 1.<video>

<video> 用于放置视频，是一个块级元素。如果浏览器支持加载的视频格式，就会显示一个播放器，否则就显示 <video> 内部的子元素

```html
<video src="example.mp4" controls>
	<p>你的浏览器不支持 HTML5 视频，请下载<a href="example.mp4">视频文件</a></p>
</video>
```

属性

- src：视频文件地址
- controls：播放器是否显示控制栏，布尔值；如果不想用浏览器默认播放器，而想自定义播放器，则不要使用
- width/height：视频播放器宽高，单位像素
- autoplay：视频是否自动播放，布尔值
- loop：视频是否循环播放，布尔值
- muted：视频默认是否静音，布尔值
- poster：视频播放器的封面图片的 URL
- preload：视频播放前，是否有缓冲文件，仅适用于 autoplay 的情况；值：none（不缓冲）、metadata（仅仅缓冲视频文件的元数据）、auto（可以缓冲整个文件）
- playsinline：禁止 Safari 浏览器播放视频自动全屏，布尔值
- crossorigin：是否采用跨域方式加载视频；值：anonymous（跨域请求时，不发送用户凭证，主要是 Cookie），use-credentials（跨域时发送用户凭证）
- currentTime：指定当前播放位置（双精度浮点数，单位秒），如果还没播放，则从该位置开始播放
- duration：只读属性，指示时间轴上的持续播放时间（总长度），值是双精度浮点数，单位秒；如果是流媒体，没有已知结束事件，属性值是 +Infinity

```html
<video width="500" height="500" autoplay loop muted poster="poster.png">
	<source src="example.mp4" type="video/mp4">
	<source src="example.webm" type="video/webm">
	<p>你的浏览器不支持 HTML5 视频，请下载<a href="example.mp4">视频文件</a></p>
</video>
```

## 2.<audio>

`<audio>`用于放置音频，是一个块级元素，用法与 `<video>` 基本一致

```html
<audio controls>
  <source src="example.mp3" type="audio/mp3">
  <source src="example.ogg" type="audio/ogg">
  <p>你的浏览器不支持 HTML5 音频，请直接下载<a href="example.mp3">音频文件</a></p>
</audio>
```

属性

- src：音频文件地址
- autoplay：是否自动播放，布尔值
- controls：是否显示播放工具栏，布尔值，不设置浏览器就不显示播放界面，通常用于背景音乐
- crossorigin：是否使用跨域方式请求
- loop：是否循环播放，布尔值
- muted：是否静音，布尔值
- preload：音频文件缓冲设置

## 3.<track>

`<track>` 用于指定视频字幕，单标签，放在 `<video>` 内部

```html
<video src="example.mp4" controls>
  <track label="英文" kind="subtitles" src="subtitles_en.vtt" srclang="en">
  <track label="中文" kind="subtitles" src="subtitles_cn.vtt" srclang="cn">
</video>
```

属性

- src：.vtt 字幕文件的网址
- srclang：字幕的语言，必须是有效代码语言
- default：是否默认打开，布尔值
- label：播放器显示的字幕名称，供用户选择
- kind：字幕的类型，默认值 subtitles，表示将原始声音翻译成外国文字，如英文视频提供中文字幕；另一个常用值 captions，表示原始声音的文字描述，通常是视频原始使用的语言，如英文视频提供英文字幕

## 4.<source>

`<source>` 用在 `<picture>`、`<video>`、`<audio>` 的内部，指定一项外部资源，单标签

属性

- src：指定源文件，用于 `<video>`、`<audio>`
- type：指定外部资源的 MIME 类型
- srcset：指定不同条件下加载的图像文件，用于 `<picture>`
- media：指定媒体查询表达式，用于 `<picture>`
- sizes：指定不同设备显示大小，用于 `<picture>`，必须跟 `srcset` 搭配使用

# 十一、表格标签

## 1. <table>，<caption>

`<table>` 是一个容器标签，也是一个块级标签，所有的表格内容都要放在这个标签中

`<caption>` 作为 `<table>` 的第一个子元素，表示表格标题，可选

```html
<table>
	<caption>表格标题</caption>
</table>
```

## 2. <thead>、<tbody>、<tfoot>

这 3 个标签都是块级容器标签，且都是 `<table>` 的直接子元素，表示表头、表体和表尾

```html
<table>
	<thead></thead>
	<tbody></tbody>
	<tfoot></tfoot>
</table>
```

大型表格内可以使用多个 `<tbody>`，表示连续的多个部分

## 3. <tr>

`<tr>` 表示表格的一行

如果有 `<thead>`、`<tbody>`、`<tfoot>` 则放在这 3 个标签中

如果没有，则作为 `<table>` 的直接子元素

```html
<table>
	<tr>...</tr>
	<tr>...</tr>
</table>
```

## 4. <th>，<td>

`<th>`、`<td>` 都用来定义表格的单元格，`<th>` 是标题单元格，`<td>` 是数据单元格

```html
<table>
	<tr>
		<th>姓名</th><th>性别</th>
	</tr>
	<tr>
		<td>张三</td><td>男</td>
	</tr>
	<tr>
		<td>李四</td><td>男</td>
	</tr>
</table>
```

单元格可能会跨行或跨列，就需要通过这 2 个属性来设置，`colspan` 设置单元格跨列数，`rowspan` 设置单元格跨行数，默认值都是 1

```html
<table>
	<tr>
		<td rowspan="2">A</td>
		<td colspan="3">B</td>
		<!-- A 跨 2 行，B 跨 3 列 -->
	</tr>
	<tr>
		<td>C</td>
		<td>D</td>
		<td>E</td>
	</tr>
</table>
```

# 十二、表单标签

## 1. <form>

`<form>` 用来定义一个表单，所有表单内容放在这个容器元素中

```html
<form action="https://example.com/aip" method="post">
  <label>用户名：<input type="text" name="user"></label>
  <input type="submit" value="提交">
</form>
```

属性

- action：服务器接收数据的 URL
- method：提交数据的 HTTP 方法，如 `post`、`get`等
- name：表单的名称，应该是网页唯一的；如果表单中的一个控件没有设置 `name` 属性，则该控件的值不会作为键值对发送给服务器
- target：指定在哪个窗口展示服务器返回的数据，`_self`（当前窗口）、`_black`（新建窗口）、`_parent`（父窗口）、`_top`（顶层窗口）、`<iframe>` 标签的 `name` 属性（即表单返回结果展示在 `<iframe>` 窗口）

## 2. <fieldset>、<legend>

`<fieldset>` 是一个表示控件的集合的块级容器标签，用于将一组相关控件合成一组

<legend> 用来设置 <fieldset> 控件组的标题

```html
<form>
  <fieldset>
		<legend>学生登记情况</legend>
    <p>姓名：<input type="text" name="name"></p>
    <p>性别：<input type="text" name="gender"></p>
  </fieldset>
</form>
```

属性

- disabled：布尔值，一旦设置是的 <fieldset> 内的控件都不可用，显示灰色
- name：指定控件组的名称

## 3. <label>

`<label>` 是一个行内元素，提供控件的文字说明

一个控件可以有多个关联的 `<label>` 标签

```html
<label for="user">用户名：</label>
<input type="text" name="user" id="user" />
<!-- or -->
<label>
	用户名：<input type="text" name="user" />
</label>
```

属性

- for：关联控件的 `id` 属性
- form：关联表单的 `id` 属性

## 4. <input>

<input> 是一个行内元素，用来接收用户的输入，单标签

该标签拥有多个类型，取决于 type 的属性值，默认是 text，即一个输入框

属性

- autofocus：布尔值，是否在页面加载时自动获得焦点
- disabled：布尔值，是否禁用该控件，用户无法操作
- name：控件的名称，用于向服务器提交数据时，控件键值对的键名，只有设置了 `name` 属性的控件才会向服务器提交数据
- readonly：布尔值，是否只读
- required：布尔值，是否必填
- type：控件类型
- value：控件的值

类型

- text
    
    `type="text"` 是一个普通文本框，用来输入单行文本
    
    ```html
    <input type="text" name="name" required minlength="4" maxlength="8" size="10" placeholder="请输入姓名" />
    ```
    
    - placeholder：输入字段为空时，用于提示的值
    - maxlength：可以输入的最大字符数
    - minlength：可以输入的最小字符数
    - readonly：布尔值，只读
    - size：表示输入框的显示长度有多少个字符宽，默认是 20，超过必须移动光标才能看到
- search
    
    `type="search"` 是用于搜索的文本输入框，基本等同于 `type="text"` ，某些浏览器在输入时会在输入框尾部显示一个删除按钮
    
    ```html
    <input type="search" placeholder="请输入关键词" required />
    ```
    
- button
    
    `type="button"` 是没有默认行为的按钮
    
    尽量避免使用，而是使用 `<button>`，语义清晰同时 `<button>` 内可以插入图片或其他 HTML 代码
    
- submit
    
    `type="submit"` 是表单的提交按钮，用户点击就会把表单提交给服务器
    
    ```html
    <input type="submit" value="提交" />
    ```
    
- image
    
    `type="image"` 表示将一个图片文件作为提交按钮，与 `type="submit"` 用法行为一样
    
    ```html
    <input type="image" alt="登录" src="login-button.png" />
    ```
    
- reset
    
    `type="reset"` 是一个重置按钮，用户点击之后，所有表格空间重置为初始值
    
    ```html
    <input type="reset" value="重置" />
    ```
    
- checkbox
    
    `type="checkbox"` 是复选框，允许选择或取消选择选项，`checked` 属性表示选中
    
    提交时`name` 值决定键名，`value` 值决定键值
    
    ```html
    <input type="checkbox" name="interest" value="run" checked />跑步
    <input type="checkbox" name="interest" value="read">读书
    <input type="checkbox" name="interest" value="music"/>音乐
    ```
    
- radio
    
    `type="radio"` 是单选框，表示一组选择中只能选一个，所有的单选项的 `name` 值应该保持一致
    
    `checked` 表示默认选中，`value` 是提交的键值
    
    ```html
    <input type="radio" name="gender" value="male" />男
    <input type="radio" name="gender" value="female" />女
    ```
    
- email
    
    `type="email"` 是一个只能输入邮箱的文本输入框，提交前浏览器会自动检测是否符合邮箱格式
    
- password
    
    `type="password"` 是一个密码输入框，用户输入会被遮挡而显示 * 或 .
    
- file
    
    `type="file"` 是一个文件选择框，允许用户选择一个或多个文件，常用于上传功能，`accept` 定义允许选择的文件类型，`multiple` 允许用户选择多个文件
    
- number
    
    `type="number"` 是一个数字输入框，只能输入数字
    
- range
    
    `type="range"` 是一个滑块，用户拖动选择给定范围中的一个数值，拖动产生的值不是精确的
    
    ```html
    <input type="range" name="volume" min="0" max="11" />
    ```
    
- url
    
    `type="url"` 是一个只能输入网址的文本框，浏览器会自动检查，注意必须要带协议
    
- tel
    
    `type="tel"` 是一个只能输入电话号码的输入框
    
- color
    
    `type="color"` 是一个选择颜色的控件
    
- date
    
    `type="date"` 是一个只能输入日期的输入框，可以输入年月日，但是不能输入时分，`max` 设置最晚日期，`min` 设置最早日期
    
- time
    
    `type="time"` 是一个只能输入时间的输入框，可以输入时分秒，不能输入年月日
    

## 5. <button>

`<button>` 标签生成一个可以点击的按钮，没有默认行为

其中可以放置 `<img>`

`type` 属性可以有 `submit`、`reset`、`button` 这 3 个值

## 6. <select>

`<select>` 用于生成一个下拉菜单，菜单项使用 `<option>` 标签

```html
<select name="value">
	<option value="">--请选择一项--</option>
	<option value="first" selected>1</option>
	<option value="second">2</option>
	<option value="third">3</option>
<select>
```

## 7. <textarea>

`<textarea>` 是一个块级元素，用来生成多行文本框

通过 `rows` 和 `cols` 来设置文本框的行数和每行字符数

通过 `resize: none;` 来禁止用户缩放文本框