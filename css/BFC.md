### 关于BFC

#### 1.何为BFC

    FC：formatting Context：格式化上下文。

    **BFC：block  formatting context ：块级格式化上下文**

    IFC： inline formatting context ： 内联级元素内的渲染规则

    GFC：grid formatting context ： display为grid 的元素内的渲染规则

    FFC ：flex formatting conntext ：display 为flex的元素内的渲染规则

#### 2. 如何形成BFC

- 为根元素，即`<html></html>` 标签内就是一个BFC环境

- float 的值不为none

- overflow 的值不为visible

- display的值为 inline-block 、table-cell、table-caption

- position的值为 absolute 或者 flex



#### 3.BFC特性

1. 在格式化上下文中，从包含块的顶部开始，块级盒子会在垂直方向上一个接一个放置

2. 垂直方向上的距离是有margin决定的，属于同一个BFC的两个相邻Box的margin会发生重叠（上下相邻 /父元素和子元素）

3. BFC的区域不会和float元素的区域重叠

4. 在BFC中，每个box的左外边缘 都与  包含块的左边缘相接触 (对于从右到左的格式化，右边缘相接触)

5. 计算BFC的高度时，浮动元素也参与计算。

6. BFC为页面的独立容器，里面的子元素不会影响外面的元素

 
