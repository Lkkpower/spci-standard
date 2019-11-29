# CSS，LESS

### 缩进

* 使用soft tab（2个空格）。
```css
.element {
  position: absolute;
  top: 10px;
  left: 10px;

  border-radius: 10px;
  width: 50px;
  height: 50px;
}
```

### 分号

* 每个属性声明末尾都要加分号。
```css
.element {
  width: 20px;
  height: 20px;

  background-color: red;
}
```

### 空格

以下几种情况不需要空格：

* 属性名后
* 多个规则的分隔符','前
* ```!important``` '!'后
* 属性值中'('后和')'前
* 行末不要有多余的空格

以下几种情况需要空格：

* 属性值前
* 选择器'>', '+', '~'前后
* '{'前
* ```!important``` '!'前
* 属性值中的','后
* 注释'/*'后和'*/'前

```less
/* not good */
.element {
  color :red! important;
  background-color: rgba(0,0,0,.5);
}
/* good */
.element {
  color: red !important;
  background-color: rgba(0, 0, 0, .5);
}

/* not good */
.element ,
.dialog{
  ...
}
/* good */
.element,
.dialog {

}

/* not good */
.element>.dialog{
  ...
}
/* good */
.element > .dialog{
  ...
}

/* not good */
.element{
  ...
}
/* good */
.element {
  ...
}
```

### 换行

以下几种情况不需要换行：

* '{'前

以下几种情况需要换行：

* '{'后和'}'前
* 每个属性独占一行
* 多个规则的分隔符','后
```css
/* not good */
.element
{color: red; background-color: black;}
/* good */
.element {
  color: red;
  background-color: black;
}

/* not good */
.element, .dialog {
  ...
}
/* good */
.element,
.dialog {
  ...
}
```

### 引号

* 最外层统一使用双引号；
* url的内容要用引号；
* 属性选择器中的属性值需要引号。
```css
.element:after {
  content: "";
  background-image: url("logo.png");
}

li[data-type="single"] {
  ...
}
```


#### 命名

* 类名使用小写字母，以中划线分隔
* id采用驼峰式命名

```css
/* class */
.element-content {
  ...
}

/* id */
#myDialog {
  ...
}
```

### 属性声明顺序

* 相关的属性声明按右边的顺序做分组处理，组之间需要有一个空行。

```css
.declaration-order {
  display: block;
  float: right;

  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  border: 1px solid #e5e5e5;
  border-radius: 3px;
  width: 100px;
  height: 100px;

  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  text-align: center;

  color: #333;
  background-color: #f5f5f5;

  opacity: 1;
}
```

### 颜色

* 颜色16进制用小写字母；
* 颜色16进制尽量用简写。

```css
/* not good */
.element {
  color: #ABCDEF;
  background-color: #001122;
}

/* good */
.element {
  color: #abcdef;
  background-color: #012;
}
```

### 属性简写

* 属性简写需要你非常清楚属性值的正确顺序，而且在大多数情况下并不需要设置属性简写中包含的所有值，所以建议尽量分开声明会更加清晰；

* ```margin``` 和 ```padding``` 相反，需要使用简写；

* 常见的属性简写包括：
```
    * font
    * background
    * transition
    * animation
```

```css
/* not good */
.element {
  transition: opacity 1s linear 2s;
}

/* good */
.element {
  transition-delay: 2s;
  transition-timing-function: linear;
  transition-duration: 1s;
  transition-property: opacity;
}
```

### 媒体查询

* 尽量将媒体查询的规则靠近与他们相关的规则，不要将他们一起放到一个独立的样式文件中，或者丢在文档的最底部，这样做只会让大家以后更容易忘记他们。

```css
.element {
  ...
}

.element-avatar{
  ...
}

@media (min-width: 480px) {
  .element {
    ...
  }

  .element-avatar {
    ...
  }
}
```

### LESS相关

#### 代码组织

* 代码按一下顺序组织：
```
    * @import
    * 变量声明
    * 样式声明
```
```less
@import "mixins/size.less";
@default-text-color: #333;
.page {
  width: 960px;
  margin: 0 auto;
}
```

#### @import 语句

* @import 语句引用的文需要写在一对引号内，.less 后缀不得省略。引号使用 ' 和 " 均可，但在同一项目内需统一。

```less
/* Not recommended */
@import "mixins/size";
@import 'mixins/grid.less';

/* Recommended */
@import "mixins/size.less";
@import "mixins/grid.less";
```

#### 混入（Mixin）

* 在定义 ```mixin``` 时，如果 ```mixin``` 名称不是一个需要使用的 className，必须加上括号，否则即使不被调用也会输出到 CSS 中。
* 如果混入的是本身不输出内容的 mixin，需要在 mixin 后添加括号（即使不传参数），以区分这是否是一个 className。

```less
/* Not recommended */
.big-text {
  font-size: 2em;
}
h3 {
  .big-text;
  .clearfix;
}

/* Recommended */
.big-text() {
  font-size: 2em;
}
h3 {
  .big-text(); /* 1 */
  .clearfix(); /* 2 */
}
```

#### 避免嵌套层级过多

* 将嵌套深度限制在2级。对于超过3级的嵌套，给予重新评估。这可以避免出现过于详实的CSS选择器。
* 避免大量的嵌套规则。当可读性受到影响时，将之打断。推荐避免出现多于20行的嵌套规则出现。

#### 字符串插值

变量可以用类似ruby和php的方式嵌入到字符串中，像@{name}这样的结构: ```@base-url: "http://assets.fnord.com"; background-image: url("@{base-url}/images/bg.png");```


### 杂项

* 不允许有空的规则；
* 元素选择器用小写字母；
* 去掉小数点前面的0；
* 去掉数字中不必要的小数点和末尾的0；
* 属性值'0'后面不要加单位；
* 同个属性不同前缀的写法需要在垂直方向保持对齐，具体参照右边的写法；
* 无前缀的标准属性应该写在有前缀的属性后面；
* 不要在同个规则里出现重复的属性，如果重复的属性是连续的则没关系；
* 不要在一个文件里出现两个相同的规则；
* 用 ```border: 0;``` 代替 ```border: none;```；
* 选择器不要超过4层（在scss中如果超过4层应该考虑用嵌套的方式来写）；
* 发布的代码中不要有 @import；
* 尽量少用'*'选择器。
```css
/* not good */
.element {
}
/* not good */
LI {
  ...
}
/* good */
li {
  ...
}

/* not good */
.element {
  color: rgba(0, 0, 0, 0.5);
}
/* good */
.element {
  color: rgba(0, 0, 0, .5);
}

/* not good */
.element {
  width: 50.0px;
}
/* good */
.element {
  width: 50px;
}

/* not good */
.element {
  width: 0px;
}
/* good */
.element {
  width: 0;
}

/* not good */
.element {
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;

  background: linear-gradient(to bottom, #fff 0, #eee 100%);
  background: -webkit-linear-gradient(top, #fff 0, #eee 100%);
  background: -moz-linear-gradient(top, #fff 0, #eee 100%);
}
/* good */
.element {
  -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
      border-radius: 3px;

  background: -webkit-linear-gradient(top, #fff 0, #eee 100%);
  background: -moz-linear-gradient(top, #fff 0, #eee 100%);
  background: linear-gradient(to bottom, #fff 0, #eee 100%);
}

/* not good */
.element {
  color: rgb(0, 0, 0);
  width: 50px;
  color: rgba(0, 0, 0, .5);
}
/* good */
.element {
  color: rgb(0, 0, 0);
  color: rgba(0, 0, 0, .5);
}
```