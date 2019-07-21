## table实现三栏布局
### display属性详解
display属性规定了一个元素应该生成的框的类型。display属性常用的属性值有none/inline/inline-block/block/table/inline-table/inherit，默认值为inline。  
**none**：元素不显示，在浏览器渲染页面时不会出现在渲染树中，同样，不会引起回流和重绘  
**inline**：行内元素，不独占一行，元素宽高由元素本身决定，不能设置margin-top/margin-bottom  
**inline-block**：行内块级元素，不独占一行，但是能改变元素的宽高，能设置margin/padding  
**block**：块级元素，独占一行，默认使用父级元素的宽度，能改变元素的宽高，能设置margin/padding  
**table**：块级表格，拥有块级元素的特点，也有表格元素的特点  
**inline-table**：行内块级元素，拥有行内块级元素的特点
### 使用table实现三栏布局的原理
包裹层设置dipslay:table，三栏设置display:table-cell，便能轻松实现三栏布局，三栏之间的间隔可以通过border-spacing设置。
### 使用table实现三栏布局的优缺点
首先，使用table实现的三栏布局是等高的，这是优点也是缺点，有时需要在左右两栏下面放置另外的模块时，显然table实现的三栏布局并不适用，而其他布局可以轻松实现。然后，使用table实现的三栏布局中间模块不能自适应，不能优先渲染中间内容部分。最后，设置了display:table之后不能设置浮动和绝对布局，不兼容ie6、7。
### 使用display:table实现三栏布局和直接使用表格元素实现三栏布局的不同
一是从文件大小来说，使用表格元素实现的三栏布局因为有很多嵌套的元素而导致本来几k的代码就能实现的布局而表格元素需要十几k，造成了资源的浪费。二是，表格元素要在页面完全加载之后才会显示，在这之前就是一片空白，造成了不好的用户体验。三是，表格元素的使用需要在一定的语义下，否则不利于seo。  
而使用table实现三栏布局，一是不需要很多嵌套的元素，许多“缺少”的元素会被浏览器自动渲染，而不出现在dom层中，最终实现和表格元素一样的效果。二是table可以边加载边渲染，不需要等到页面完全加载完毕后才显示出来。三是table没有seo问题。
### html部分
```
<div class="layout">
    <div class="left">left</div>
    <div class="center">center</div>
    <div class="right">right</div>
</div>
```
### css部分
```
.layout{
  text-align: center;
  display: table;
  width: 100%;
  border-spacing: 50px;
  border: 1px solid #000;
}
.layout>div{
  display: table-cell;
  width: 200px;
}
.left{
  background-color: #f00;
}
.center{
  width: 100%;
  background-color: #0f0;
}
.right{
  background-color: #00f;
}
```