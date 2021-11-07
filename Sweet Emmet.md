# Sweet Emmet

## Child：>

```html
<!-- nav>ul>li -->
<nav>
  <ul>
    <li></li>
  </ul>
</nav>
```

## Sibling：+

```html
<!-- header+main+footer -->
<header></header>
<main></main>
<footer></footer>
```

## Climb-up：^

```html
<!-- div+div>p>span+em^bq -->
<div></div>
<div>
  <p><span></span><em></em></p>
  <blockquote></blockquote>
</div>

<!-- div+div>p>span+em^^bq -->
<div></div>
<div>
  <p><span></span><em></em></p>
</div>
<blockquote></blockquote>
```

## Grouping：()

```html
<!-- div>(header>ul>li>a)+footer>p -->
<div>
  <header>
    <ul>
      <li><a href=""></a></li>
    </ul>
  </header>
  <footer>
    <p></p>
  </footer>
</div>

<!-- (div>dl>(dt+dd))+footer>p -->
<div>
  <dl>
    <dt></dt>
    <dd></dd>
  </dl>
</div>
<footer>
  <p></p>
</footer>
```

## Multiplication：*

```html
<!-- ul>li*5 -->
<ul>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

## Text：{}

```html
<!-- a{Click me} -->
<a href="">Click me</a>

<!-- p>{Click }+a{here}+{ to continue} -->
<p>Click <a href="">here</a> to continue</p>
```

## Item numbering：$

```html
<!-- ul>li.item$*5 -->
<ul>
  <li class="item1"></li>
  <li class="item2"></li>
  <li class="item3"></li>
  <li class="item4"></li>
  <li class="item5"></li>
</ul>

<!-- h$[title=item$]{Header $}*3 -->
<h1 title="item1">Header 1</h1>
<h2 title="item2">Header 2</h2>
<h3 title="item3">Header 3</h3>

<!-- ul>li.item$$$*5 -->
<ul>
  <li class="item001"></li>
  <li class="item002"></li>
  <li class="item003"></li>
  <li class="item004"></li>
  <li class="item005"></li>
</ul>

<!-- ul>li.item$@-*5 -->
<ul>
  <li class="item5"></li>
  <li class="item4"></li>
  <li class="item3"></li>
  <li class="item2"></li>
  <li class="item1"></li>
</ul>

<!-- ul>li.item$@3*5 -->
<ul>
  <li class="item3"></li>
  <li class="item4"></li>
  <li class="item5"></li>
  <li class="item6"></li>
  <li class="item7"></li>
</ul>
```

## ID and Class attributes

```html
<!-- #header -->
<div id="header"></div>

<!-- .title -->
<div class="title"></div>

<!-- form#search.wide -->
<form id="search" class="wide"></form>

<!-- p.class1.class2.class3 -->
<p class="class1 class2 class3"></p>
```

## Custom attributes

```html
<!-- p[title="Hello world"] -->
<p title="Hello world"></p>

<!-- td[rowspan=2 colspan=3 title] -->
<td rowspan="2" colspan="3" title=""></td>

<!-- [a="value1" b="value2"] -->
<div a="value1" b="value2"></div>
```

## Implicit tag names

```html
<!-- .attr -->
<div class="attr"></div>

<!-- em>.attr -->
<em><span class="attr"></span></em>

<!-- ul>.attr -->
<ul>
  <li class="attr"></li>
</ul>

<!-- table>.row>.col -->
<table>
  <tr class="row">
    <td class="col"></td>
  </tr>
</table>
```