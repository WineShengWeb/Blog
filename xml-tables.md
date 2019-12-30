# XML中常用的标签和表格属性

#### 常用标签

```
w:p	文本段落
w:pPr	段落设置
w:ind	缩进
w:jc	文本位置(left/center/right/...)
w:r	文字块
w:rPr	文本设置
w:rFonts  字体设置
w:color	文字颜色
w:sz	文字大小
w:t	文本内容
w:b	粗体
w:i	斜体
w:u	下划线
w:strike	删除线
w:tbl	表格
w:tblPr	表格设置
w:tblGrid	单元格(列属性)
w:tr	表格行
w:tc	表格列
w:tcPr	表格列设置
w:tcW	列宽
```

#### 表格属性

```xml
<w:tbl>  表格开始标志
<w:tblPr>表格属性


<w:tblW w:w="0" w:type="auto"/>这个type=还可以使用“pct”根据窗口调整
  <w:jc w:val="center"/>表格居中
  <w:tblBorders>边框线
    <w:top w:val="single" w:sz="4" wx:bdrwidth="10" w:space="0" w:color="auto"/> 上边线
    <w:bottom w:val="single" w:sz="4" wx:bdrwidth="10" w:space="0" w:color="auto"/>下边线
    <w:insideH w:val="single" w:sz="4" wx:bdrwidth="10" w:space="0" w:color="auto"/>横线
    <w:insideV w:val="single" w:sz="4" wx:bdrwidth="10" w:space="0" w:color="auto"/>竖线

  </w:tblBorders>说明：我画的表格是左右两边无边框的，所有少两行：<w:left w.../><w:right.../>

如果上下两条线是1.5，需要设置w:sz="12" wx:bdrwidth="30",具体换算不知是怎样的，待摸索。
</w:tblPr>
<w:tr >表格加一行
<w:tc> 表格加一列
 <w:tcPr> 单元格属性，由X行Y列决定在这一行中新加的一列就是一个单元格
  <w:tcW w:w="2490" w:type="dxa" /> 单元格宽
  </w:tcPr>
<w:p >单元格中加一段落
<w:pPr>段落属性
 <w:jc w:val="center"/>居中
</w:pPr>
<w:r>段落中文字行
<w:t>第一列</w:t>文字
</w:r>段落行结束，如果要换行，可重复这部分
</w:p>
</w:tc>完成一个单元格
<w:tc> 新单元格，不指定单元格属性，则默认居左。
<w:p >
<w:r>
<w:t>第二列</w:t>
</w:r>
</w:p>
</w:tc></w:tr>第一行第二列完成

<w:tr >开始新行
<w:tc> 
 <w:tcPr> 
  <w:tcW w:w="2490" w:type="dxa" /> 
<w:gridSpan w:val="2"/>这一列是合并列，合并了后面一列，所以跨度是2
  </w:tcPr>
<w:p >
<w:pPr>
 <w:jc w:val="center"/>
</w:pPr>
<w:r>
<w:t>2行1列</w:t>
</w:r>
</w:p>
</w:tc>
<w:tc> 这一列是原来没合并前写的，实际合并后就不应该写这部分，但是写上不报错，只是表格不是想象的那样了，导致第二行多出来第三列。
<w:p >
<w:r>
<w:t>2行2列</w:t>
</w:r>
</w:p>
</w:tc>
</w:tr>
</w:tbl>
```
