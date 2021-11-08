# Sass 总结

# 一、什么是 Sass?

Sass 是一种 CSS 开发工具，提供了非常多便利的写法，节省了 CSS 开发的时间

以剪发为例，剪发分为洗头发、做造型、出头发。随着工作细化，发型师不会一人包揽所有流程，否则会忙不过来。于是，每个流程有专门的人执行。

而，编写网页 css，类似于做造型。它还有前后 2 个过程，分别是 pre processor 和 post css，小型项目这 2 个部分纯手写还行，但是项目稍微大一点编写及维护就非常痛苦，于是这 2 个过程就有了各种工具来处理。

pre processor：less、sass(scss)、stylus

post css：-moz、-webkit、-o、-ms 这些一般都不会再自己手写，而是配合使用 auto-prefixer

# 二、安装

Sass 是由 Ruby 实现的，需要先安装 Ruby

再输入 `gem install sass` 安装 Sass

或者，通过 npm、yarn 等包管理工具安装

# 三、Sass v.s. Scss

Sass：

```sass
nav
	float: left
	a
		display: inline-block
```

Scss：即 sassy css，完全兼容 css，形式上更像是在写 css

```scss
nav {
	float: left;
	a {
		display: inline-block;
	}
}
```

# 四、编译

在屏幕上显示 test.scss 编译后的 css 代码：

```bash
sass test.scss
```

将编译后的 css 代码保存为一个 .css 文件：

```bash
sass test.scss test.css
```

让 Sass 监听某个文件或目录，一旦源文件变动自动生成编译后的版本：

```bash
# watch a file
sass --watch input.scss:output.css
# watch a directory
sass --watch app/scss:public/stylesheets
```

Sass 提供了 4 种编译风格：

- nested：嵌套缩进的css代码，它是默认值
- expanded：没有缩进的、扩展的css代码
- compact：简洁格式的css代码
- compressed：压缩后的css代码

生产环境中，一般使用最后一个选项：

```bash
sass --style compressed test.scss test.css
```

# 五、软件与配置

1. 环境、软件、插件：Node、VSCode、Live Server、Live Sass Compiler
2. 软件设置：

![Untitled](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378034845-7fdb33fb-ca44-43cf-b4b9-8bb6a4bc39c1.png)

![Untitled](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378024863-7f407341-6299-4735-bf32-ec867cce16c3.png)

autoprefix 做了 post css 的最为人乐道的功能

浏览器市占率大于 1% 的都加上 -moz 这些前缀

支持那些浏览器的最新 2 个版本

另外，通过配置，liveSassCompiler 会编译出一个 css 正常的文件到根目录下的 style 目录中，会编译出一个压缩的 css 文件到根目录下的 dist 目录中的 style 目录中

# 六、基本用法

## 1. 变量

所有变量以 $ 开头

Scss 中写 css：

```scss
// scss
width: calc(100%/6);

// css
width: calc(100%/6); // 性能、兼容都差一点
```

Scss 使用变量：

```scss
//scss
$width: 100%;
$buttonNumber: 6;
width: $width / $buttonNumber;

//css
width: 16.66667%;
```

如果变量需要镶嵌在字符串中，就必须写在 `#{}` 中

```scss
// scss
$side: left;
$name: mail;
.rounded {
	border-#{$side}-radius: 4px;
}
.icon-#{$name} {
  background-image: url("/icons/#{$name}.svg")
}

// css
.rounded {
  border-left-radius: 4px;
}
.icon-mail {
  background-image: url("/icons/mail.svg");
}
```

## 2. 计算

可以使用算式

```scss
body {
	margin: (10px/2);
	top: 40px + 120px;
	right: $width * 10%;
}
```

## 3. 嵌套

可以使用选择器嵌套

```scss
// scss
div {
	hi {
		color: red;
	}
}

// css
div h1 {
	color: red;
}
```

属性也可以嵌套（注意，font、border 后面的 `:` 必须写）

```scss
// scss
div {
  height: 100px;
  font: {
    family: 'fangsong';
    size: 20px;
    weight: 700;
  }
  border: 1px solid red {
   left: 0;
   top: 0;
  }
}

// css
div {
  height: 100px;
  font-family: "fangsong";
  font-size: 20px;
  font-weight: 700;
  border: 1px solid red;
  border-left: 0;
  border-top: 0;
}
```

在嵌套的代码块内：

- 可以使用 & 引用父类
- 可以使用符号 `>` 创建子类选择器：匹配一个直接子元素
- 可以使用符号 `+` 或 `~` 创建同级选择器：匹配下一个相邻的同级元素或以下所有同级元素

```scss
// scss
article a {
  color: blue;
  &:hover { color: red }
}

// css
article a { color: blue }
article a:hover { color: red }
```

```scss
// scss
article {
  ~ article { border-top: 1px solid #ddd }
  > section { background: #ccc }
  dl > {
    dt { color: #666 }
    dd { color: #333 }
  }
  nav + & { margin-top: 0 }
}

// css
article ~ article {
  border-top: 1px solid #ddd;
}
article > section {
  background: #ccc;
}
article dl > dt {
  color: #666;
}
article dl > dd {
  color: #333;
}
nav + article {
  margin-top: 0;
}
```

## 4. 注释

标准的 CSS 注释 `/* comment */` ，会保留到编译后的文件，跟一个 ! 表示重要注释，即使压缩模式编译也会保留，通常用于声明版权信息

```scss
/*!
	重要注释！
*/
```

单行注释 `// comment`，只保留在 Scss 源文件中，编译后被省略

# 七、代码重用

## 1. 继承

允许一个选择器，继承另一个选择器的全部样式

```scss
// scss
.a {
  color: #000;
}
.a x {
  font-size: 10px;
}
.b {
  @extend .a;
  background-color: #fff;
}

// css
.a, .b {
	color: #000;
}
.a x, .b x {
	font-size: 10px;
}
.b {
	background-color: #fff;
}
```

有的时候我们不需要继承的父类也生成代码，因此可以使用 placeholder 来声明

```scss
// scss
%a {
  color: #000;
}
%a x {
  font-size: 10px;
}
.b {
  @extend %a;
  background-color: #fff;
}

// css
.b {
  color: #000;
}
.b x {
  font-size: 10px;
}
.b {
  background-color: #fff;
}
```

## 2. 混入

功能最强大，可以定义一个重用的代码块，并使用

```scss
// scss
@mixin line {
	text-decoration: none;
	display: block;
}
div {
	@include line;
}
.a {
	@include line;
}

// css
div {
  text-decoration: none;
  display: block;
}
.a {
  text-decoration: none;
  display: block;
}
```

mixin 的强大之处，在于可以指定参数和默认值

```scss
// scss
@mixin line($display, $decoration: none) {
   display: $display;
   li {
     display: $display;
     text-decoration: $decoration;
   }
}
div {
  @include line(inline-block, none);  
}
.x {
	@include line(block, underline)
}
.y {
  @include line(inline)
}

// css
div {
  display: inline-block;
}
div li {
  display: inline-block;
  text-decoration: none;
}
.x {
  display: block;
}
.x li {
  display: block;
  text-decoration: underline;
}
.y {
  display: inline;
}
.y li {
  display: inline;
  text-decoration: none;
}
```

## 3. 模块化系统

CSS 的 `@import` 非常难用，需要执行到它时才能触发浏览器去下载它所 `import` 来的 css 文件，导致页面加载起来特别慢

Sass 扩展了 CSS 的 `@import` 功能，默认情况下，它会寻找 Sass 文件并直接引入，所有引入的 Scss 和 Sass 文件都会被合并并输出一个单一的 CSS 文件，被导入的文件中所定义的变量或 `mixins` 都可以在主文件中使用

```scss
@import 'path/filename.scss'
#app {
	@import url('path/filename.scss')
}
```

# 八、高级用法

## 1. 条件语句

```scss
p {
　@if 1 + 1 == 2 { border: 1px solid; }
	@if 5 < 3 { border: 2px dotted; }
}

@if lightness($color) > 30% {
　background-color: #000;
} @else {
　background-color: #fff;
}
```

## 2. 循环语句

through 结束值执行，to 结束值不执行

```scss
// scss
@for $i from 1 through 3 {
  .div#{$i}{
     height: $i * 20px;
  }
}
@for $i from 1 to 3 {
  .span#{$i}{
     height: $i * 20px;
  }
}

// css
.div1 {
  height: 20px;
}
.div2 {
  height: 40px;
}
.div3 {
  height: 60px;
}
.span1 {
  height: 20px;
}
.span2 {
  height: 40px;
}
```

有判断条件的 while 循环

```scss
// scss
$i: 5;
@while $i > 0 {
    .item-#{$i} {
        width: 2px * $i;
    }
    $i: $i - 1;
}

// css
.item-5 {
  width: 10px;
}
.item-4 {
  width: 8px;
}
.item-3 {
  width: 6px;
}
.item-2 {
  width: 4px;
}
.item-1 {
  width: 2px;
}
```

## 3. 列表循环

```scss
// scss
$list: a,b,c,d; 
@each $member in $list {
    .#{$member} {
        background-image: url("/image/#{$member}.jpg");
    }
}

// css
.a {
  background-image: url("/image/a.jpg");
}
.b {
  background-image: url("/image/b.jpg");
}
.c {
  background-image: url("/image/c.jpg");
}
.d {
  background-image: url("/image/d.jpg");
}
```

## 4. 字符串函数

```scss
// scss
.span1 {
	content: to-upper-case('hello world')
}
.span2 {
	content: to-lower-case('HELLO WORLD')
}

// css 
.span1 {
  content: "HELLO WORLD";
}
.span2 {
  content: "hello world";
}
```

## 5. 数字函数

```scss
// scss
.div1 {
  width: round(16.6px);
}
.div2 {
  width: ceil(16.5px);
}
.div3 {
  width: floor(16.4px);
}
.div4 {
  width: abs(-16.3px);
}
.div5 {
  width: min(30, 290, 10%, 33, 80%);
}
.div6 {
  width: max(23, 11, 20, 29%, 199);
}
.div7 {
  width: random() + '%';
}

// css
.div1 {
  width: 17px;
}
.div2 {
  width: 17px;
}
.div3 {
  width: 16px;
}
.div4 {
  width: 16.3px;
}
.div5 {
  width: 10%;
}
.div6 {
  width: 199;
}
.div7 {
  width: "0.98725%";
}
```

## 6. 颜色函数

Sass 提供了一些内置的颜色函数，可以生成系列颜色

```scss
// scss
body {
	lighten(#cc3, 10%) // #d6d65c
	darken(#cc3, 10%) // #a3a329
	grayscale(#cc3) // #808080
}
```

## 7. 自定义函数

计算出一个结果

```scss
// scss
@function line($count: 1, $baseLineHeight: 10px){
	@return $baseLineHeight * $count
}
.aa {
	padding: line(2, 12px)
}

// css
.aa {
  padding: 24px;
}
```