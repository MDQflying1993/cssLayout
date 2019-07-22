#三栏布局之Flex布局
##Flex布局：
**Flex**是Flexible Box的缩写，即弹性布局，用来为盒装模型提供最大的灵活性。任何一个容器都可以被指定为Flex布局，行内元素也可以被指定为Flex布局。

采用Flex布局的元素，成为Flex容器（flex container）简称“容器”。它所有的子元素自动成为容器成员，即容器的项（items）

**容器属性**


* flex-direction：决定主轴的方向，即items的排列方向；
	* row（默认值）:表示主轴为水平方向，起点在左；
	* row-reverse：主轴为水平方向，起点在右；
	* column：主轴为垂直方向，起点在上沿；
	* column-reverse：主轴为垂直方向，起点在下沿；
*  flex-wrap：默认情况下，items都排在一条线上（即主轴），flex-wrap属性决定的是，如果一条主轴线排不下该如何换行？
	* nowrap（默认）：不换行；
	* wrap：换行，第一行在上方；
	* wrap-reverse：换行，第一行在下方，第二行在上； 
*  flex—flow：该属性是flex-direction属性和flex-wrap属性的简写形式，默认row，nowrap。
*  justify-content：该属性定义了item在主轴上的对齐方式
	* justify-content:flex-start 表示左对齐（默认）
	* justify-content: flex-end 表示右对齐
	* justify-content: center 表示居中对齐
	* justify-content:space-between 表示两端对齐，item之间的间隔都相等
	* justify-content:space-around表示每个item两侧的间隔相等，所以item之间的间隔比item与边框的间隔大一倍。 
	
*  align-items：该属性定义item在交叉轴上的对齐方式。
	* flex-start：交叉轴的起点对齐
	* flex-end:交叉轴的终点对齐
	* center：交叉轴的中点对齐
	* baseline：项目的第一行文字的基线对齐。
   * stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。  
* align-content：该属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
	* flex-start：与交叉轴的起点对齐。
   * flex-end：与交叉轴的终点对齐。
	* center：与交叉轴的中点对齐。
	* space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
	* space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
	* stretch（默认值）：轴线占满整个交叉轴。

	
**item	属性：**
	
	* order：该属性定义项目的排列顺序，数值越小，排列越靠前，默认为0；
	* flex-grow：该属性定义项目的放大比例，默认值为0，此时即使存在剩余空间，也不会放大
	* flex-shrink：该属性定义项目的缩小比例，默认为1，即如果空间不足，该项目将会缩小，如果为0，则不会缩小，注：负值对该属性无效
	* flex-basis：该属性定义了在分配多余空间前，项目占据的主轴空间（main size），浏览器根据此属性计算主轴是否有多余空间，默认值为auto，即项目的本来大小。
	* flex：该属性是flex-grow和flex-shrink及flex-basis的简写，默认值为0 1 auto；
	* align-self：该属性可以允许单个项目与其他项目不一样的对齐方式，可以覆盖align-items属性，默认值为auto，表示继承父元素的align-items属性，如果没有父元素，等同于stretch。




三栏布局基础HTML

~~~
<body>
    <div class="container">
        <!-- 优先渲染 -->
        <div class="center">
            center
        </div>
        <div class="left">
            left
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
  display: flex;
}
.center {
  background-color: red;
  width: 100%;
  order: 2;
}
.left {
  background-color: green;
  width: 200px;
  flex-shrink: 0;
  order: 1;
}
.right {
  background-color: blue;
  width: 200px;
  flex-shrink: 0;
  order: 3;
}
~~~


###步骤：
1. 设置容器为flex布局，display:flex;
2. center的宽度设置为width:100%,left和right设置为200px；
3. 设置center部分可以收缩，设置flex-shrink：0；
4. 使用order属性给三个部分的 DOM 结构进行排序：left：order: 1，center：order: 2，right：order: 3

**flex-shrink：**
该属性用于定义对应item的缩小比例，默认为1，如果空间不足则项目缩小，如果有一项为0，其他为1，则当空间不足时，前者不缩小；


###Flex布局优缺点：
1. **优点：**弹性布局比较灵活，行内元素亦可以使用Flex布局，任何一个容器都可以被指定为弹性布局，即：display:flex(注：Webkit内核，如Safari，需要添加前缀，即display：-webkit-flex;2在Flex布局中，子元素的float，clear，vertical-align属性都会失效)
2.  **缺点：**flex布局时CSS3中引入，在IE9.0以下版本中不兼容，需注意版本兼容问题






