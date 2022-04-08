<hr/>画一条线

***a标签***

1. text-decoration:none;a标签去除下划线
2. text-decoration:underline;a标签添加下划线

***label 标签为 input 元素定义标注。for 属性应当与相关元素的 id 属性相同，规定 label 与哪个表单元素绑定。标记通常以下面两种方式中的一种来和表单控件相联系：将表单控件作为标记标签的内容，这样的就是隐式形式，或者为 <label> 标签下的 for 属性命名一个目标表单 id，这样就是显式形式。***

1. 显式的联系：<label for="SSN">Social Security Number:</label><input type="text" name="SocSecNum" id="SSN" />
2. 隐式的联系：<label>Date of Birth: <input type="text" name="DofB" /></label>
3. 第一个标记是以显式形式将文本 "Social Security Number:" 和表单的社会安全号码的文本输入控件 ("SocSecNum") 联系起来，它的 for 属性的值和控件的 id 一样，都是 SSN。第二个标记 ("Date of Birth:") 不需要 for 属性，它的相关控件也不需要 id 属性，它们是通过在 <label> 标签中放入 <input> 标签来隐式地连接起来的。

***tbody 标签表格主体（正文）。该标签用于组合 HTML 表格的主体内容。thead 元素用于对 HTML 表格中的表头内容进行分组，而 tfoot 元素用于对 HTML 表格中的表注（页脚）内容进行分组。***

1. thead、tfoot 以及 tbody 元素使您有能力对表格中的行进行分组。当您创建某个表格时，您也许希望拥有一个标题行，一些带有数据的行，以及位于底部的一个总计行。这种划分使浏览器有能力支持独立于表格标题和页脚的表格正文滚动。当长的表格被打印时，表格的表头和页脚可被打印在包含表格数据的每张页面上。
2. 属性                      值                                               描述
   align                      right,left,center,justify,char         定义 tbody 元素中内容的对齐方式。
   char                      character                                    规定根据哪个字符来进行文本对齐。
   charoff                  number                                       规定第一个对齐字符的偏移量。
   valign                    top,middle,bottom,baseline        规定 tbody 元素中内容的垂直对齐方式。
3. vertical-align:middle;垂直居中

***input标签***

1. checked 属性规定在页面加载时应该被预先选定的 input 元素。与 <input type="checkbox"> 或 <input type="radio"> 配合使用。单选框 复选框
2. disabled 属性规定应该禁用 input 元素。按钮也可用

***渐变色***

```
径向渐变：background:-webkit-radial-gradient(center,closest-corner,#ffffff,#1E90FF)

```