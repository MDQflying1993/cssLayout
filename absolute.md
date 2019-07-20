#### absolute布局
##### 什么是定位
css中position属性，position的四个值：relative/absolute/fixed/static（相对/绝对/固定/静止）通过这些属性可以实现布局，使用（top/right/bottom/left)来调整元素位置。
##### 属性描述
static（静态）：没有特别的设定，基本就是默认设置，不能用z-index进行层次分级，在普通流中，各个元素之间默认的属性。

relative（相对定位）：设定元素不可重叠，**不脱离文档流** ，参考自身静态位置通过top/right/bottom/left定位。

absolute（绝对定位）：**脱离文档流** ，通过top/right/bottom/left定位，选取其最近的一个具有定位设置的父级对象进行定位，如果设置对象的父级没有设置定位属性，absolute元素将以body坐标原点进行定位。

fixed（固定定位）：该对象的参照对象是可视窗口而非body或者父级元素。使用了fixed的元素不会随着窗口的滚动而滚动，属于absolute的子集。
##### 各个属性的具体作用
static：通常情况下不会使用，但是会存在某些场景，就是想把position从其他值修改成默认值的时候

relative：一个元素设定了position:relative，因为其不脱离文档流，如果不设置TLBR的话，它的位置不会改变，且不会影响当前布局，相当于什么事没有发生一样，设置了TLBR后，元素会向其他方向偏移，**但它原有的位置还是占据着的**。

absolute：完全脱离文档流，原来的位置不再占有，可以设置TRBL任意移动
**特别说明：对元素设置absolute后，其父元素都没有设置position：absolute/relative/fixed其会以body为父级**

fixed：不会随着页面的滚动而滚动，最形象的就是网页中的广告，即使你滚动页面，也会随时跟着你。

##### 布局技巧
如果对元素设置absolute后，其父级元素都没有设置position：relative，会以body为父级。这样对于我们量像素很麻烦。
当子代设置了position：absolute后，其父元素设置了position：relative，这个子代就会从父元素最上方作为起点移动，并且遵循**就近原则**，即子代向上寻找父元素，当找第一个有父级元素设置了position：relative就以它最左上方作为起点。

relative和absolute相结合的方式，对定位布局起到了便利，需要移动的距离也得到了缩小，不用从body开始整个页面来量取像素，同时也方便管理，结构清晰。

##### 优缺点
float布局与position布局的最大区别就是是否占据文档流的问题，虽然position布局也有absolute和fixed这两个同样不占据文档流的属性，但这两个并不适合对给整个网页布局，因为使用它后就得为文档的每个元素设置一个xy坐标来定位。
float布局显得更加灵活。有些时候使用position布局有更好的效果。
在性能问题上，比如reflow问题，将元素的position设置为absolute和fixed可以使元素从文档流中脱离出来而单独存在，而浏览器需要渲染时只需要渲染该元素以及该元素下方的元素，在某种程度上可以减少渲染时间。所以如果是设置js动画等，用absolute或fixed更好。