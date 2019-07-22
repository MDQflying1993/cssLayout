#三栏布局之Grid布局
##Grid布局：
**Grid**是一个二维布局系统，可以把页面分割成不同的网格块，并且可以定义它们的大小，同时每个网格又可以独立设置自己的位置（这里区别于table）。

1. **容器:**网格布局的容器是设置display为grid或者inline-grid，这一点跟flex布局很像，而它的子元素就是网格元素。
2. **网格线:**分割网格的线称为网格线，包括横向（从左往右）和纵向（从右往左）。网格线可以通过grid-template-columns和grid-template-rows命名，默认以数字命名（注意是从1开始）。
3. **网格:**网格就是被网格线划分出来的单元格，也就是网格元素，这里跟table一样，多个网格可以合并。
4. **轨道:**相邻两个网格线之间的称为轨道。

**Grid布局定义：**使用display属性来定义一个网格容器，它的grid值决定了容器展现为块级还是内联形式。一旦启用网格容器，它的所有子元素都进入grid文档流，称为网格子项。

~~~
display: grid | inline-grid | subgrid
~~~

	* grid：定义一个块级的网格容器

	* inline-grid：定义一个内联的网格容器

	* subgrid：定义一个继承其父级网格容器的行和列的大小的网格容器，它是其父级网格容器的一个子项。

	* tips: column, float, clear和vertical-align对网格容器没有效果。

**容器属性：**

容器指定了网格布局后，接着需要划分行和列。

* grid-template-columns：属性定义每一列的列宽；
* grid-template-rows：属性定义每一行的行高；


~~~
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
}
表示指定了一个三行三列的网格，列宽和行高都是100px（此处也可用百分比）；
如果需要多次写重复值，可以使用repeat（）函数改写：

.container {
  display: grid;
  grid-template-columns: repeat(3, 33.33%);
  grid-template-rows: repeat(3, 33.33%);
}
repeat()接受两个参数，第一个参数是重复的次数（上例是3），第二个参数是所要重复的值。
repeat()重复某种模式也是可以的。
~~~



*  grid-row-gap：该属性设置行与行的间隔（行间距）；
*  grid-column-gap：该属性设置了列与列的间隔（列间距）；
*  grid-gap:	该属性是grid-column-gap和grid-row-gap合并的简写，

~~~
.container {
  grid-row-gap: 20px;
  grid-column-gap: 20px;
}

grid-gap: <grid-row-gap> <grid-column-gap>;
因此，以上可改写：
.container {
  grid-gap: 20px 20px;
}

~~~


* grid-template-areas：网格布局中允许指定区域，一个区域可有单个或者多个单元格组成，该属性用于定义区域；

~~~
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas: 'a b c'
                       'd e f'
                       'g h i';
}
~~~


* grid-auto-flow:划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格。默认的放置顺序是"先行后列"，即先填满第一行，再开始放入第二行。这个顺序由grid-auto-flow属性决定，默认值是row，即"先行后列"。也可以将它设成column，变成"先列后行"。


* justify-items 属性;
* align-items 属性;
* place-items 属性;
justify-items属性设置单元格内容的水平位置（左中右），align-items属性设置单元格内容的垂直位置（上中下）。

~~~
.container {
  justify-items: start | end | center | stretch;
  align-items: start | end | center | stretch;
}
这两个属性的写法完全相同，都可以取下面这些值。
start：对齐单元格的起始边缘。
end：对齐单元格的结束边缘。
center：单元格内部居中。
stretch：拉伸，占满单元格的整个宽度（默认值）。
.container {
  justify-items: start;
}
~~~

* justify-content 属性，
* align-content 属性，
* place-content 属性
justify-content属性是整个内容区域在容器里面的水平位置（左中右），align-content属性是整个内容区域的垂直位置（上中下）。

~~~
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
}
~~~

这两个属性的写法完全相同，都可以取下面这些值。（下面的图都以justify-content属性为例，align-content属性的图完全一样，只是将水平方向改成垂直方向。）
start - 对齐容器的起始边框。


* grid-auto-columns 属性，
* grid-auto-rows 属性
有时候，一些项目的指定位置，在现有网格的外部。比如网格只有3列，但是某一个项目指定在第5行。这时，浏览器会自动生成多余的网格，以便放置项目。

grid-auto-columns属性和grid-auto-rows属性用来设置，浏览器自动创建的多余网格的列宽和行高。它们的写法与grid-template-columns和grid-template-rows完全相同。如果不指定这两个属性，浏览器完全根据单元格内容的大小，决定新增网格的列宽和行高。

下面的例子里面，划分好的网格是3行 x 3列，但是，8号项目指定在第4行，9号项目指定在第5行。

~~~

.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-auto-rows: 50px; 
}
~~~

* grid-template 属性，
* grid 属性
grid-template属性是grid-template-columns、grid-template-rows和grid-template-areas这三个属性的合并简写形式。

grid属性是grid-template-rows、grid-template-columns、grid-template-areas、 grid-auto-rows、grid-auto-columns、grid-auto-flow这六个属性的合并简写形式。



**项目属性：**

* grid-column-start 属性，
* grid-column-end 属性，
* grid-row-start 属性，
* grid-row-end 属性
项目的位置是可以指定的，具体方法就是指定项目的四个边框，分别定位在哪根网格线。

~~~
grid-column-start属性：左边框所在的垂直网格线
grid-column-end属性：右边框所在的垂直网格线
grid-row-start属性：上边框所在的水平网格线
grid-row-end属性：下边框所在的水平网格线

.item-1 {
  grid-column-start: 2;
  grid-column-end: 4;
} 

~~~

* grid-column 属性，
* grid-row 属性
grid-column属性是grid-column-start和grid-column-end的合并简写形式，grid-row属性是grid-row-start属性和grid-row-end的合并简写形式。

~~~
.item {
  grid-column:  / ;
  grid-row:  / ;
}
~~~
如：

~~~
.item-1 {
  grid-column: 1 / 3;
  grid-row: 1 / 2;
}
/* 等同于 */
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 1;
  grid-row-end: 2;
}
上面代码中，项目item-1占据第一行，从第一根列线到第三根列线。

这两个属性之中，也可以使用span关键字，表示跨越多少个网格。
~~~



~~~
.item-1 {
  background: #b03532;
  grid-column: 1 / 3;
  grid-row: 1 / 3;
}
/* 等同于 */
.item-1 {
  background: #b03532;
  grid-column: 1 / span 2;
  grid-row: 1 / span 2;
}
  
~~~  
  
  
 * grid-area
 grid-area属性指定项目放在哪一个区域
 
  ~~~
  .item-1 {
  grid-area: e;
}
grid-area属性还可用作grid-row-start、grid-column-start、grid-row-end、grid-column-end的合并简写形式，直接指定项目的位置。

.item {
  grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
}
例如：

.item-1 {
  grid-area: 1 / 1 / 3 / 3;
}
  ~~~
  
  
  
 * justify-self 属性，
 * align-self 属性，
* place-self 属性
justify-self属性设置单元格内容的水平位置（左中右），跟justify-items属性的用法完全一致，但只作用于单个项目。

align-self属性设置单元格内容的垂直位置（上中下），跟align-items属性的用法完全一致，也是只作用于单个项目。

~~~
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
这两个属性都可以取下面四个值。

start：对齐单元格的起始边缘。
end：对齐单元格的结束边缘。
center：单元格内部居中。
stretch：拉伸，占满单元格的整个宽度（默认值）。
例如：
.item-1  {
  justify-self: start;
}
~~~
	
三栏布局基础HTML

~~~
<body>
    <div class="container">
        <div class="left">
            left
        </div>
        <!-- 这时的center要放在中间 -->
        <div class="center">
            center
        </div>
        <div class="right">
            right
        </div>
    </div>
</body>
~~~

基础CSS


~~~
 .container {
        display: grid;
        width: 100%;
        grid-template-rows: 100px;
        grid-template-columns: 200px auto 200px;
    }
~~~


步骤：

1. 给 container 设置为display: grid
2. 设置三栏的高度：grid-template-rows: 100px
3. 设置三栏的宽度，中间自适应，两边固定：grid-template-columns: 200px auto 200px;


###Grid布局优缺点：

1. Grid布局相对flex布局更加全面，是一种二维布局，可以轻松实现较为复杂的二维布局；
2. 缺点是兼容性不够好
















