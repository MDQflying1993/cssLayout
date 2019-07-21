## inline-block实现三栏布局
### display属性详解
display属性规定了一个元素应该生成的框的类型。display属性常用的属性值有none/inline/inline-block/block/table/inline-table/inherit，默认值为inline。  
**none**：元素不显示，在浏览器渲染页面时不会出现在渲染树中，同样，不会引起回流和重绘  
**inline**：行内元素，不独占一行，元素宽高由元素本身决定，不能设置margin-top/margin-bottom  
**inline-block**：行内块级元素，不独占一行，但是能改变元素的宽高，能设置margin/padding  
**block**：块级元素，独占一行，默认使用父级元素的宽度，能改变元素的宽高，能设置margin/padding  
**table**：块级表格，拥有块级元素的特点，也有表格元素的特点  
**inline-table**：行内块级元素，拥有行内块级元素的特点
### 使用inline-block实现三栏布局的原理
包裹层使用padding为两边留出位置，三栏设置display:inline-block放置在同一行，中间宽度为100%
### 使用inline-block实现三栏布局的优缺点
首先，最显而易见的就是代码换行带来的空格，在页面上显示就是两个inline-block元素之间会产生一个英文字母的空白间隙，因此要在包裹层设置letter-spacing为normal，消除单词之间的空隙，并将单词的字体大小设置为0，由于font-size属性具有继承性，在三栏中将字体大小恢复成原来的大小。然后每一栏的高度都是根据自身的内容填充，除了特意设置，三栏的高度不是等高的。最后，因为左右两栏的宽度是固定的，当页面宽度小于左右两栏的总和时，页面出现兼容性问题。
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
  border: 1px solid #000;
  padding: 0 200px;
  letter-spacing: normal;
  font-size: 0;
}
.layout>div{
  display: inline-block;
  width: 200px;
  font-size: 1rem;
  vertical-align: top;
}
.left{
  background-color: #f00;
  margin-left: -200px;
}
.layout .center{
  width: auto;
  background-color: #0f0;
}
.right{
  background-color: #00f;
  margin-right: -200px;
}
```