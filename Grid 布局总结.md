# 一、基本概念


Grid 布局比 Flex 布局更强大，Flex 布局是通过指定子项针对轴线的位置，是一种一维布局，Grid 布局是通过划分行与列，指定子项所在的单元格，是一种二维布局


## 1. 容器与子项


给 `<div>` 这类块级元素设置了 `display: grid;` 或者给 `<span>` 这类內联元素设置了 `display: inline-grid;`，就创建了 Grid 布局


`<div>`、`<span>` 这样采用 Grid 布局的区域，称为「容器」


容器内部的直接子元素，称为「子项」


```html
<div>
  <div><p>1</p></div>
  <div><p>2</p></div>
  <div><p>3</p></div>
</div>
```


上面代码中，`<div>` 就是容器，内部的 3 个 `<div>` 就是子项


3 个 `<p>` 并不是子项，而 Grid 布局只对子项生效


## 2. 行与列


容器内部，水平区域称为「行」，垂直区域称为「列」


![11.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378574827-dab403eb-6148-498f-9b1e-d409083a3a9b.png#clientId=udd7f076c-01d6-4&from=paste&height=454&id=u441860ed&margin=%5Bobject%20Object%5D&name=11.png&originHeight=454&originWidth=661&originalType=binary&ratio=1&size=14454&status=done&style=none&taskId=u62c5ef67-0af9-44fc-9fa9-2bf26881b1b&width=661)


## 3. 单元格


行与列交叉的矩形区域，称为「单元格」


一般来说，n 行和 m 列会产生 n x m 个单元格


## 4. 网格线


划分网格的线，称为「网格线」，水平网格线划分出行，竖直网格线划分出列


一般来说，n 行有 n+1 根水平网格线，m 列有 m+1 根竖直网格线


注意，我们在定义网格时，一般定义的都是网格轨道，或者说行与列，而不是网格线


![1.jpg](https://cdn.nlark.com/yuque/0/2021/jpeg/385743/1636378586783-4ed5799b-4ebe-4d91-a6fc-b741c37a29f5.jpeg#clientId=udd7f076c-01d6-4&from=paste&height=438&id=u9cfad14b&margin=%5Bobject%20Object%5D&name=1.jpg&originHeight=438&originWidth=781&originalType=binary&ratio=1&size=49630&status=done&style=none&taskId=ua68485a1-0868-4f90-be39-0ed4f9ec8d0&width=781)


# 二、Grid 布局 CSS 属性概览


## grid 容器属性


- grid-template-columns
- grid-template-rows
- grid-template-areas
- grid-template
- grid-column-gap
- grid-row-gap
- grid-gap
- justify-items
- align-items
- place-items
- justify-content
- align-content
- place-content
- grid-auto-columns
- grid-auto-rows
- grid-auto-flow
- grid



## grid 子项属性


- grid-column-start
- grid-column-end
- grid-row-start
- grid-row-end
- grid-column
- grid-row
- grid-area
- justify-self
- align-self
- place-self



# 三、容器属性


## 1. display


```css
div { display: grid; }
```


即创建 grid 布局


![Unititled 1.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378633684-e42fa9af-55b6-4ac9-8469-8b75895a8275.png#clientId=udd7f076c-01d6-4&from=paste&height=357&id=u061fab0d&margin=%5Bobject%20Object%5D&name=Unititled%201.png&originHeight=357&originWidth=349&originalType=binary&ratio=1&size=12372&status=done&style=none&taskId=ue9a5b4de-575e-43c3-b44a-429c83ac009&width=349)


默认，容器都是块级元素，但是也可以设置成內联元素


```css
div { display: inline-grid; }
```


![Untitled 2.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378674269-4d7b0fe4-d6e2-453f-9103-66815546011b.png#clientId=udd7f076c-01d6-4&from=paste&height=335&id=u6f51fb79&margin=%5Bobject%20Object%5D&name=Untitled%202.png&originHeight=335&originWidth=405&originalType=binary&ratio=1&size=13014&status=done&style=none&taskId=ue6b6bc1d-1a02-4016-8778-a5d5f00fee5&width=405)


`grid` 和 `inline-grid` 区别在于：


`inline-grid` 容器为 `inline` 特性，因此可以和图片文字一行显示


grid 容器保持块状特性，宽度默认 100%，不和内联元素一行显示


注意：设为网格布局以后，「子项」的 `float`、`display: inline-block`、`display: table-cell`、`vertical-align` 和 `column-*` 等设置都将失效


## 2. grid-template-columns、grid-template-rows


创建网格布局之后，开始划分行和列


`grid-template-columns` 定义每一列的列宽


`grid-template-rows` 定义每一行的行高


语法：


```css
.container {
	grid-template-columns: <track-size> ... | <line-name> <track-size> ...;
	grid-template-rows: <track-size> ... | <line-name> <track-size> ...;
}
/*
	<track-size>：列宽或行高，可以是长度值、百分比以及 fr
	<line-name>：网格线名称，可以任意命名
*/
```


例子：


```css
.container {
	grid-template-columns: 40px auto 100px;
  grid-template-rows: 25% 150px auto 80px;
}
```


上面的代码，指定了一个 4 行 3 列的网格


3 列的宽度分别为 40px、auto、100px


4 行的高度分别是 25%、150px、auto、80px


![Untitled 3.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378686610-f8a92625-4d05-4a12-90f9-c4a1a4f6573a.png#clientId=udd7f076c-01d6-4&from=paste&height=371&id=ufe875127&margin=%5Bobject%20Object%5D&name=Untitled%203.png&originHeight=371&originWidth=397&originalType=binary&ratio=1&size=11458&status=done&style=none&taskId=u727ecd51-6405-403c-b5f7-c8e6e6b3576&width=397)


我们还可以给每条网格线使用 `[]` 进行包裹命名：


```css
.container {
	grid-template-columns: [c1]40px [c2]auto [c3]100px;
  grid-template-rows: [r1]25% [r2]150px [r3]auto [r4]80px;
}
```


网格线允许同一根线有多个名字，比如 `[r2 second-line 第2根横线]`


给网格线命名，是为了更好地对区域进行描述，就好比以 2 条公路联合命名的公交站一样


当然，如果没有描述某片区域的需求，自然也不需要命名了


### 2.1 repeat()


对重复写同样的值进行简化


参数 1：重复次数；参数 2：重复的值


```css
.container {
	display: grid;
	gird-template-columns: repeat(3, 50px);
	grid-template-rows: repeat(4, 80px);
}
// 等价于
.container {
	display: grid;
	grid-template-columns: 50px 50px 50px;
	grid-template-rows: 80px 80px 80px 80px;
}
```


`repeat` 可以重复某种模式


```css
grid-template-columns: repeat(2, 100px 20px 50px);
```


第 1、4 列宽 100px，第 2、5 列宽 20px，第 3、6 列宽 50px


### 2.2 auto-fill 关键字


表示自动填充，让每一行或每一列尽可能容纳更多的单元格


有时，我们希望单元格大小是固定的，但是容器的大小不是固定的或不确定


然后希望每行或每列可以容纳尽可能多的单元格，有一种响应式的效果


可以使用 `auto-fill` 作为 `repeat` 第一个表示重复次数的参数


```css
.container {
	display: grid;
	grid-template-columns: repeat(auto-fill, 100px);
}
```


随着容器的宽度变大变小，一行中的列数会增多减少，但每列的宽度都是 100px


### 2.3 fr 关键字


`fr`，即 fraction（片段），表示容器可用空间的拆分的份数


```css
.container {
	display: grid;
	grid-template-columns: 1fr 2fr 1fr;
}
```


容器被分成 3 列，分别为 1 份、2 份、1 份的宽度


-  当有固定尺寸，则划分剩余空间大小，很常用很方便 
![Untitled 4.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378698361-a9796912-97e1-4518-8a82-380a3a549d10.png#clientId=udd7f076c-01d6-4&from=paste&height=413&id=uec88b432&margin=%5Bobject%20Object%5D&name=Untitled%204.png&originHeight=413&originWidth=875&originalType=binary&ratio=1&size=19062&status=done&style=none&taskId=u9e7f9f24-cce0-4071-8dad-499985d873a&width=875)
后 2 列宽度是 grid 容器宽度减去 200 像素后的 1/3、2/3 大小 
```css
.container {
	display: grid;
	grid-template-columns: 200px 1fr 2fr;
	grid-template-rows: repeat(4, 100px);
}
```

-  与 `auto` 混用 
![Untitled 5.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378705597-faa229df-4fe3-4839-91d5-4d9b132cd126.png#clientId=udd7f076c-01d6-4&from=paste&height=415&id=u6a3c3373&margin=%5Bobject%20Object%5D&name=Untitled%205.png&originHeight=415&originWidth=575&originalType=binary&ratio=1&size=14696&status=done&style=none&taskId=u798c1a9b-a422-4b40-b7cd-e3f10180eee&width=575)
当有设置 `fr` 尺寸的时候，`auto` 的尺寸表现为“包裹”，即为内容宽度
如果没有设置 `fr` 尺寸的网格，则表现为拉伸 
```css
.container {
	display: grid;
	grid-template-columns: auto 1fr 1fr;
	gird-template-rows: repeat(4, 100px);
}
```

-  fr 之和小于 1 
![Untitled 6.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378714237-aa30a15a-c265-4e06-9cd3-1fbd6718cf35.png#clientId=udd7f076c-01d6-4&from=paste&height=308&id=uc33d59ee&margin=%5Bobject%20Object%5D&name=Untitled%206.png&originHeight=308&originWidth=499&originalType=binary&ratio=1&size=12251&status=done&style=none&taskId=u9156c284-f2d3-47ff-9de4-ac6f872d5c1&width=499)
由于第 1 列的宽度是 `auto`，所以剩下的容器宽度为：容器宽度-"第1列数字字符的宽度"
于是，剩下 3 列宽度都是 （容器宽度 - "第一列数字字符宽度"）* 0.25
这 3 列宽度确定，容器剩下的宽度就是第 1 列的宽度 
```css
.container {
	display: grid;
	grid-template-columns: auto 0.25fr 0.25fr 0.25fr;
	grid-template-rows: repeat(3, 100px);
}
```


### 2.4 minmax()


该函数产生一个长度范围，表示长度就在这个范围内，接收 2 个参数，分别是最小值和最大值


```css
.container {
	display: grid;
	grid-template-columns: 1fr 1fr minmax(80px 1fr);
	grid-template-rows: repeat(4, 100px);
}
```


![Untitled 7.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378723656-7abdd7c4-ad26-477d-b42a-f0ee05cf7a81.png#clientId=udd7f076c-01d6-4&from=paste&height=413&id=u61a8d97c&margin=%5Bobject%20Object%5D&name=Untitled%207.png&originHeight=413&originWidth=560&originalType=binary&ratio=1&size=15342&status=done&style=none&taskId=u75bd7fd8-1d6f-4826-a1f1-6d312203feb&width=560)


`minmax(80px, 1fr)` 表示第 3 列宽度不小于 80px，不大于 `1fr`


### 2.5 auto 关键字


表示由浏览器自己决定长度


```css
grid-template-columns: 200px auto 100px;
```


除非，第二列单元格「内容」设置了 `min-width`，并且这个值大于最大宽度


否则，第二列的宽度基本等于该列单元格的最大宽度


### 2.6 方便的布局


两栏布局：


```css
.container {
	display: grid;
	gird-template-columns: 70% 30%;
}
```


十二网格布局：


```css
.container {
	display: grid;
	grid-template-columns: repeat(12, 1fr);
}
```


## 3. grid-template-areas、子项属性（grid-area）


`grid-template-areas` 属性，就是给网格划分区域的，一个区域可以由「一个或多个」单元格组成


这个属性一般结合 grid 子项的 `grid-area` 一起使用


`grid-area` 属性，指定 grid 子项隶属于那个区域


语法：


```css
.container {
	grid-template-areas: "<grid-area-name> | . | none | ...";
}
/*
	grid-area-name：网格区域名称
	.：空的网格单元，表示没有用到该单元格，或者该单元格不属于任何网格区域
	none：没有定义网格区域
*/
```


例子：


```css
.container {
	display: grid;
	grid-template-columns: repeat(3, 150px);
	grid-template-rows: repeat(3, 150px);
	grid-template-areas: 
		"header header ."
		"sidebar content content"
		"footer footer footer";
}
.header {
	grid-area: header;
}
.sidebar {
	grid-area: sidebar;
}
.content {
	grid-area: content;
}
.footer {
	grid-area: footer;
}
```


9 个格子，4 片区域，因此，我们的 grid 子项只需要 4 个元素即可


```html
<div class="container">
  <div class="header">header</div>
  <div class="sidebar">sidebar</div>
  <div class="content">content</div>
  <div class="footer">footer</div>
</div>
```


![Untitled 8.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378735942-5dee37f4-dc70-4caf-8e05-b418e679a44e.png#clientId=udd7f076c-01d6-4&from=paste&height=460&id=ua38277d2&margin=%5Bobject%20Object%5D&name=Untitled%208.png&originHeight=460&originWidth=460&originalType=binary&ratio=1&size=14839&status=done&style=none&taskId=u64f8d82e-8067-464f-aa01-74babaa79a1&width=460)


注意：


网格区域命名会影响到网格线，自动根据网格区域名生成网格线名


规则就是，在网格区域名后面加上 -start 与 -end


比如，某个网格区域名为 content，则该区域左、上的 column、row 线叫做「content-start」，该区域右、下的 column、row 线叫做「content-end」


另外：网格区域应该是矩形区域，不规则区域是无效属性值


## 4. grid-template


是 `grid-template-rows`、`grid-template-columns`、`gird-template-areas` 这 3 个属性的合并简写形式


比如，上面的例子可以简写为：


```css
.container {
	display: grid;
	grid-template: 
		"header header ." 150px
		"sidebar content content" 150px
		"footer footer footer" 150px
		/150px 150px 150px;
}
```


也可以省略 `grid-template-areas`：


```css
.container {
	display: grid;
	grid-template: repeat(3, 1fr) / repeat(3, 1fr);
}
```


## 5. row-gap、column-gap、gap


`gird-row-gap` 属性，设置行与行之间的间距


`grid-column-gap` 属性，设置列与列之间的间距


`grid-gap` 属性，是 `grid-row-gap`、`grid-column-gap` 的合并简写形式


```css
.container {
	display: grid;
	grid-row-gap: <line-size>;
	grid-column-gap: <line-size>;
	/* grid-gap: <grid-row-gap> <grid-column-gap>; */
}
```


根据最新标准：上面 3 个属性的 grid- 前缀已删除，推荐使用 `row-gap`、`column-gap`、`gap`


```css
.container {
	display: grid;
	row-gap: 10px;
	column-gap: 10px;
	/* gap: 10px 10px; */
}
```


## 6. justify-items、align-items、place-items


`justify-items` 属性，整体指定单元格内容的水平呈现方式，是水平拉伸，还是左中右水平对齐


`aling-items` 属性，整体指定单元格内容的垂直呈现方式，是垂直拉伸，还是垂直上中下对齐


`place-items` 属性，是 `align-items`、`justify-items` 的合并简写形式，要注意顺序，如果省略第 2 个值，则浏览器会认为与第 1 个值相等


```css
.container {
	justify-items: legacy | stretch | start | end | center;
	align-items: stretch | start | end | center;
	/* place-items: <align-items> <justify-items>?; */
}
```


### 6.1 justify-items 取值


- legacy：默认值，拉伸，水平填充
- stretch：拉伸，水平填充
- start：网格水平尺寸收缩为内容大小，同时沿网格线左侧对齐显示
- end：网格水平尺寸收缩为内容大小，同时沿网格线右侧对齐显示
- center：网格水平尺寸收缩为内容大小，同时在当前网格区域内水平居中对齐显示



```css
.container {
	justify-items: start;
}
```


![Untitled 9.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378749526-036347d0-1a01-4734-80e2-565a50e1d3eb.png#clientId=udd7f076c-01d6-4&from=paste&height=502&id=u0a2ba39b&margin=%5Bobject%20Object%5D&name=Untitled%209.png&originHeight=502&originWidth=502&originalType=binary&ratio=1&size=16656&status=done&style=none&taskId=u5edebc2b-086c-4307-995b-a59770f9cf1&width=502)


### 6.2 align-items 取值


- stretch：默认值，拉伸，垂直填充
- start：网格垂直尺寸收缩为内容大小，同时沿着上网格线对齐显示
- end：网格垂直尺寸收缩为内容大小，同时沿着下网格线对齐显示
- center：网格尺寸收缩为内容大小，同时在当前网格区域内部垂直居中对齐显示



```css
.container {
	align-items: start;
}
```


![Untitled 10.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378757315-bc9e3134-c437-42fa-86ec-36e6bcda5d1b.png#clientId=udd7f076c-01d6-4&from=paste&height=501&id=u12f7608e&margin=%5Bobject%20Object%5D&name=Untitled%2010.png&originHeight=501&originWidth=501&originalType=binary&ratio=1&size=12127&status=done&style=none&taskId=u861a38b9-7088-4187-b088-5d863bf2139&width=501)


### 6.3 place-items 取值


```css
.container {
	place-items: center;
}
```


![Untitled 11.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378764301-00407741-8881-469d-8317-829fd45d9481.png#clientId=udd7f076c-01d6-4&from=paste&height=502&id=u616dc0f3&margin=%5Bobject%20Object%5D&name=Untitled%2011.png&originHeight=502&originWidth=502&originalType=binary&ratio=1&size=13320&status=done&style=none&taskId=uafafe69c-9383-4f63-a9c0-ed25cdf60a7&width=502)


## 7. justify-content、align-content、place-content


`justify-content` 属性，指定整个内容区域（每一列）在容器里面的水平分布方式


`align-content` 属性，指定整个内容区域（每一行）在容器里面的水平分布方式


`place-content` 属性，是 `align-content`、`justify-content` 的合并简写形式，省略第 2 个值浏览器会认为与第 1 个值相等


```css
.container {
	justify-content: stretch | start | end | center | space-between | space-around | space-evenly;
	align-content: stretch | start | end | center | space-between | space-around | space-evenly;
	/* place-content: <align-content> <justify-content>?; */
}
```


### 7.1 使用前提


上述属性，仅在网格总宽度、高度小于 grid 容器宽度、高度时候有效果，比如，网格设定了固定宽度，容器有剩余空间


```css
.container {
	display: grid;
	width: 400px;
	grid-template: 100px 100px 100px/100px 100px 100px;
}
```


### 7.2 justify-content、align-content 取值


- stretch：默认值，等比例拉伸，宽度/高度填满 grid 容器 
   - 需要在网格目标尺寸设置为 auto 时才有效，如果定死长度，则无法拉伸
   - 比如 `grid-template: repeat(3, 100px) / repeat(3, 100px);` 就无法拉伸，当然，其它取值还是有效果的
- start：对齐容器的起始边框
- end：对齐容器的结束边框
- center：容器内部居中
- space-between：子项与子项的间距相等，子项与容器边框之间没有间距
- space-around：子项之间的间隔比子项与容器边框的间距大一倍
- space-evenly：子项之间的间距相等，子项与容器边框之间也是同样长度的间距



```css
.container {
	display: grid;
	grid-template: repeat(3, 100px) / repeat(3, 100px);
	justify-content: center;
	align-content: space-between;
	/* place-content: space-between start; */
}
```


![Untitled 12.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378775978-66bac747-5a72-4742-9026-6ae410b37a39.png#clientId=udd7f076c-01d6-4&from=paste&height=402&id=u6215ea7c&margin=%5Bobject%20Object%5D&name=Untitled%2012.png&originHeight=402&originWidth=402&originalType=binary&ratio=1&size=12493&status=done&style=none&taskId=u6979995c-5065-4f1e-9401-c66c31327e9&width=402)


## 8. grid-auto-columns、grid-auto-rows


### 8.1 显式网格、隐式网格


显式网格：包含了使用 `grid-template-columns`、`grid-template-rows`定义的行与列


隐式网格：当你在定义的网格之外又放了一些东西（比如网格只有 3 列却指定某个子项在第 5 列），或者因为内容的数量需要更多的网格轨道，浏览器会自动生成多余的网格以放置子项


多余网格的列宽、行高由这 2 个属性设置


值的设置与 `grid-template-colums`、`grid-template-rows` 一样


如果不设置这 2 个属性，浏览器完全根据单元格内容的尺寸，决定新增网格的列宽和行高


```css
.container {
  display: grid;
  grid-template-columns: 80px 50px;
  grid-template-rows: 50px 50px;
  grid-auto-rows: 100px;
}
```


![Untitled 13.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378786622-e782f690-6395-427d-89a3-77bc1afb001c.png#clientId=udd7f076c-01d6-4&from=paste&height=424&id=u339de3b5&margin=%5Bobject%20Object%5D&name=Untitled%2013.png&originHeight=424&originWidth=405&originalType=binary&ratio=1&size=12553&status=done&style=none&taskId=uc0bcf939-9c31-4c46-94b3-95ca64fb54e&width=405)


## 9. grid-auto-flow


划分网格之后，容器的子项会按照顺序，自动放置在每一个网格中


该属性，用来控制没有明确指定位置的子项的放置方式


语法：


```css
.container {
	grid-auto-flow: row | column | row dense | column dense;
}
```


取值：


- row：默认值，即先行后列。先填满第一行，再放入第二行，以此类推
- column：先列后行。先填满第一列，再放入第二列，以此类推
- dense：稠密，设置了之后表示自动排列启用「稠密打包算法」 
   - 在自动排列顺序的规则下，使网格尽可能稠密
   - 主要用于某些项目指定位置以后，剩下的项目怎么自动放置
   - 这个属性值仅仅改变视觉顺序，并不改变 DOM 属性，可能会导致疑惑，谨慎使用



```css
.container {
	display: grid;
	grid-template: repeat(3, 1fr) / repeat(3, 1fr);
	grid-auto-flow: column;
}
```


![Untitled 14.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378795721-8f18eeed-a074-4dcd-a48e-32ad30727e1f.png#clientId=udd7f076c-01d6-4&from=paste&height=402&id=u2fa8f90a&margin=%5Bobject%20Object%5D&name=Untitled%2014.png&originHeight=402&originWidth=402&originalType=binary&ratio=1&size=11139&status=done&style=none&taskId=ud3d41f41-0558-4dc5-8cd2-bf9a5b8fb58&width=402)


当 item-1 后面空间无法放下 item-2 时，会出现以下情况：


![Untitled 15.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378801996-3df7a490-327d-41b6-a367-283e81548f0f.png#clientId=udd7f076c-01d6-4&from=paste&height=418&id=uf4bc44e5&margin=%5Bobject%20Object%5D&name=Untitled%2015.png&originHeight=418&originWidth=403&originalType=binary&ratio=1&size=12719&status=done&style=none&taskId=u7dbbd39b-0534-45ac-af90-c5830e4918b&width=403)


```css
.container {
	display: grid;
	grid-auto-flow: row dense;
}
```


![Untitled 16.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378808113-e8d74ad2-2222-4883-8760-01fc4f23b00b.png#clientId=udd7f076c-01d6-4&from=paste&height=417&id=ud27fd835&margin=%5Bobject%20Object%5D&name=Untitled%2016.png&originHeight=417&originWidth=402&originalType=binary&ratio=1&size=12782&status=done&style=none&taskId=u77501f6f-d24d-4080-ba97-b783c6694ce&width=402)


```css
.container {
	display: grid;
	grid-auto-flow: column dense;
}
```


![Untitled 17.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378816598-0645bec5-a871-493b-8248-2d27322f6b26.png#clientId=udd7f076c-01d6-4&from=paste&height=417&id=u4bda2ddf&margin=%5Bobject%20Object%5D&name=Untitled%2017.png&originHeight=417&originWidth=402&originalType=binary&ratio=1&size=11793&status=done&style=none&taskId=ud4a8367f-304e-4814-8560-e4cca0c98be&width=402)


## 10. grid


`grid` 属性，是 `grid-template-rows`、`grid-template-columns`、`grid-template-areas`、`grid-auto-rows`、`grid-auto-columns`、`grid-auto-flow` 这 6 个属性的合并简写形式


语法:


```css
.container {
	grid: none;
	grid: <grid-template>;
	grid: <grid-template-rows> / [auto-flow && dense?] <grid-auto-columns>?;
	grid: [auto-flow && dense?] <grid-auto-rows> / <grid-template-columns>;
}
```


具体解释：


```css
.container {
	grid: none;
}
/* 表示设置所有的子属性为初始值 */
```


```css
.container {
	grid: 100px 300px / 3fr 1fr;
}
/* 等价于 */
.container {
	grid-template-rows: 100px 300px;
	grid-template-columns: 3fr 1fr;
}
```


```css
.container {
	grid: 100px 300px / auto-flow 200px;
}
/* 等价于 */
.container {
	grid-template-rows: 100px 300px;
	grid-auto-flow: column;
	grid-auto-columns: 200px;
}
```


```css
.container {
  grid: auto-flow dense 100px / 1fr 2fr;
}
/* 等价于 */
.container {
  grid-auto-flow: row dense;
  grid-auto-rows: 100px;
  grid-template-columns: 1fr 2fr;
}
```


如果没有哪个单元格跑到 grid 容器外面，那么就是用 `grid-template` 属性


后面 2 个语法是使用在当 grid 容器外有单元格的时候，要么是 `grid-template/auto-flow`，要么是 `auto-flow/grid-tempalte`


# 四、子项属性


## 1. grid-column-start、grid-column-end、grid-row-start、grid-row-end


我们可以指定子项所在的 4 个边框分别定位在哪根网格线，从而指定子项的位置


使用这 4 个属性，如果产生了子项的重叠，则使用 `z-index` 属性指定子项的重叠顺序


语法：


```css
.item {
    grid-column-start: <number> | <name> | span <number> | span <name> | auto
    grid-column-end: <number> | <name> | span <number> | span <name> | auto
    grid-row-start: <number> | <name> | span <number> | span <name> | auto
    grid-row-end: <number> | <name> | span <number> | span <name> | auto
}
```


- ：第几条网格线（从 1 开始）
- ：自定义的网格线名
- span ：表示当前子项会跨越多少个单元格
- auto：全自动，包括定位、跨度



```css
.item-1 {
	grid-column-start: 2;
	grid-column-end: 4;
}
.item-2 {
	grid-row-start: 2;
	grid-column-end: 4;
}
/* 等价于 */
.container {
  display: grid;
  grid-template: [r1]100px [r2]100px [r3]100px [r4] / [c1]100px [c2]100px [c3]100px [c4];
}
.item-1 {
	grid-column-start: c2;
	grid-column-end: c4;
}
.item-2 {
	grid-row-start: span 2;
}
```


![Untitled 18.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378828785-a496962a-4e32-4122-9dc6-62f45494654e.png#clientId=udd7f076c-01d6-4&from=paste&height=417&id=u39e0dfc3&margin=%5Bobject%20Object%5D&name=Untitled%2018.png&originHeight=417&originWidth=312&originalType=binary&ratio=1&size=9874&status=done&style=none&taskId=u38acc1ce-5017-4d34-8d8f-24681d71317&width=312)


## 2. grid-column、grid-row


`grid-column` 属性，是 `grid-column-start`、`grid-column-end` 的合并简写形式


`grid-row` 属性，是 `grid-row-start`、`grid-row-end` 的合并简写形式


语法：


```css
.item {
    grid-column: <start-line> / <end-line> | <start-line> / span <value> | <start-line>;
    grid-row: <start-line> / <end-line> | <start-line> / span <value> | <start-line>;
}
```


```css
.container {
	display: grid;
  grid-template: [r1]100px [r2]100px [r3]100px [r4]/[c1]100px [c2]100px [c3]100px [c4];
}
.item-1 {
	grid-column: 2/4;
}
.item-2 {
	grid-row: 2/4;
}
/* 等价于 */
.item-1 {
	grid-column: 2 / span 2;
}
.item-2 {
	grid-row: r2 / span r4;
}
```


![Untitled 18.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378935348-49e0d279-774f-443b-b77d-066b548e2c28.png#clientId=udd7f076c-01d6-4&from=paste&height=417&id=uded66afd&margin=%5Bobject%20Object%5D&name=Untitled%2018.png&originHeight=417&originWidth=312&originalType=binary&ratio=1&size=9874&status=done&style=none&taskId=u084c7f85-956f-40d2-b199-bd5570abbd0&width=312)


`/` 以及后面的部分可以省略，即从起始网格线开始默认跨越一个单元格


## 3. grid-area


`grid-area` 属性，指定该子项放在哪个区域，在容器属性 `grid-template-areas` 中说过，不再赘述


除了支持 `grid-template-areas` 使用外，该属性其实是 `grid-row-start`、`grid-column-start`、`grid-row-end`、`grid-column-end` 的合并简写形式


语法：


```css
.item {
    grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
}
```


```css
.item-1 {
	grid-area: 1/2/3/4;
}
```


![Untitled 19.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378915293-9ad137b8-4055-4024-bc27-cbaaff294409.png#clientId=udd7f076c-01d6-4&from=paste&height=417&id=u3c64ea2b&margin=%5Bobject%20Object%5D&name=Untitled%2019.png&originHeight=417&originWidth=312&originalType=binary&ratio=1&size=9654&status=done&style=none&taskId=u9e0fe344-39f2-451c-b2db-78ae074364d&width=312)


## 4. justify-self、align-self、place-self


`justify-self` 属性，与 `justify-items` 属性用法完全相同，只作用于单个子项，设置单元格内容的水平对齐方式


`align-self` 属性，与 `align-items` 属性用法完全相同，只作用于单个子项，设置单元格内容的垂直对齐方式


`place-self` 属性，是 `justify-self`、`align-self` 的合并简写形式


语法：


```css
.item {
  justify-self: stretch | start | end | center;
	align-self: stretch | start | end | center;
	place-self: <align-self> <justify-self>?;
}
```


```css
.item-1 {
	justify-self: start;
}
.item-2 {
	align-self: end;
}
.item-3 {
	place-self: center center;
}
```


![Untitled 20.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636378891806-790e35ab-a06f-447c-9e05-c6932764ab61.png#clientId=udd7f076c-01d6-4&from=paste&height=312&id=uaf29082d&margin=%5Bobject%20Object%5D&name=Untitled%2020.png&originHeight=312&originWidth=312&originalType=binary&ratio=1&size=8423&status=done&style=none&taskId=u66aeda57-3e3b-4b34-b3bf-5bda5147f65&width=312)


# 五、参考资料


- [MDN Grid](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid)
- [CSS Grid 网格布局教程](https://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)
- [写给自己看的display: grid布局教程](https://www.zhangxinxu.com/wordpress/2018/11/display-grid-css-css3/)
