***position 属性规定元素的定位类型。***

1. absolute 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
2. fixed 生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
3. relative 生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。
4. static 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。
5. inherit规定应该从父元素继承 position 属性的值。

***display 属性规定元素应该生成的框的类型。***

1. none	此元素不会被显示。
   block	此元素将显示为块级元素，此元素前后会带有换行符。
   inline	默认。此元素会被显示为内联元素，元素前后没有换行符。
   inline-block	行内块元素。（CSS2.1 新增的值）
   list-item	此元素会作为列表显示。
   run-in	此元素会根据上下文作为块级元素或内联元素显示。
   compact	CSS 中有值 compact，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。
   marker	CSS 中有值 marker，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。
   table	此元素会作为块级表格来显示（类似 <table>），表格前后带有换行符。
   inline-table	此元素会作为内联表格来显示（类似 <table>），表格前后没有换行符。
   table-row-group	此元素会作为一个或多个行的分组来显示（类似 <tbody>）。
   table-header-group	此元素会作为一个或多个行的分组来显示（类似 <thead>）。
   table-footer-group	此元素会作为一个或多个行的分组来显示（类似 <tfoot>）。
   table-row	此元素会作为一个表格行显示（类似 <tr>）。
   table-column-group	此元素会作为一个或多个列的分组来显示（类似 <colgroup>）。
   table-column	此元素会作为一个单元格列显示（类似 <col>）
   table-cell	此元素会作为一个表格单元格显示（类似 <td> 和 <th>）
   table-caption	此元素会作为一个表格标题显示（类似 <caption>）
   inherit	规定应该从父元素继承 display 属性的值。

***background-position 属性设置背景图像的起始位置。***

1. top left       如果您仅规定了一个关键词，那么第二个值将是"center"。默认值：0% 0%。
   top center 
   top right
   center left
   center center
   center right
   bottom left
   bottom center
   bottom right
2. x% y%第一个值是水平位置，第二个值是垂直位置。左上角是 0% 0%。右下角是 100% 100%。如果您仅规定了一个值，另一个值将是 50%。
3. xpos ypos第一个值是水平位置，第二个值是垂直位置。左上角是 0 0。单位是像素 (0px 0px) 或任何其他的 CSS 单位。如果您仅规定了一个值，另一个值将是50%。您可以混合使用 % 和 position 值。


***table表格***

1. thead标头行   th标头单元格
2. tbody正文    tr行，td单元格
3. border边框，后面有三个参数    边框宽度，实线虚线，颜色
4. text-align文字排列   center居中
5. border-collapse 属性设置表格的边框是否被合并为一个单一的边框，还是象在标准的 HTML 中那样分开显示。collapse  如果可能，边框会合并为一个单一的边框。会忽略 border-spacing 和 empty-cells 属性。

position 属性规定元素的定位类型。

1. absolute  生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
2. fixed  生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
3. relative  生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。
4. static  默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。
5. inherit  规定应该从父元素继承 position 属性的值。