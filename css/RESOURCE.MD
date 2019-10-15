强制换行 
```css
word-break: break-all;
```
强制不换行 
```css
word-break: keep-all;
```

清除图片下方出现几像素的空白间隙
```css
img{display:block;}
#test{font-size:0;line-height:0;}
#test为img的父元素
```

让单行文本在容器内垂直居中
```css
#test{height:25px;line-height:25px;}
```
清除浮动
```css
#test{zoom:1;}
#test:after{display:block;clear:both;visibility:hidden;height:0;content:'';}
#test为浮动元素的父元素
```
移除img边框
```css
a img{ border:none; }
```
css手型点击样式
```css
input[type=submit],label,select,.pointer { cursor:pointer; }
```
移动超链接的虚线框
```css
a:active, a:focus{ outline:none; }
```
table边框合并，显示单线框
```css
table{
   border-collapse: collapse;
}
table tr td,table tr th{
   border:1px solid #e2e2e2;
}
```
移除input类型为number在谷歌浏览器下自带的上下箭头
```css
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none !important;
    margin: 0;
}
```
解决position:fixed抖动的问题
```html
<div style="position:fiexd;bottom:0px;">
  <div style="position:absolute;">
  </div>
</div>
```
vh、vw、vmin、vmax这四个单位都是基于视口的
vw是相对视口（viewport）的宽度而定的，长度等于视口宽度的1/100著作权归作者所有。
vh是相对视口（viewport）的高度而定的，长度等于视口高度的1/100著作权归作者所有。
vmin和vmax是相对于视口的高度和宽度两者之间的最小值或最大值著作权归作者所有。

rem是相对于根元素（html）的字体大小（font-size）来计算的长度单位著作权归作者所有。
em是相对于其父元素的字体大小 当元素自身设置了字体大小，那么如果它的其他css属性也使用em单位，则会基于它自身的字体大小著作权归作者所有。


只在IE下生效：
```
<!--[if IE]>
这段文字只在IE浏览器显示
<![endif]-->
```
http://www.cnblogs.com/taojiaqu/p/4894383.html
--------------------------------------------------------------------------------------

p标签左右两端对齐:
```css
text-align:justify;text-justify:inter-ideograph;
```
--------------------------------------------------------------------------------------
display:none 和visibility:hidden的区别
1. 使用display:none,元素会完全不显示；visibility:hidden,元素还占用空间；
2. display:none,内容元素都不能访问,但是设为visibility:hidden之后,可以通过设置子元素的visibility来显示子元素内
```css
* {
       outline: 0;
       padding: 0;
       margin: 0;
       border: 0;
}
```

去除li圆点
```css
li {list-style-type: none;}
```

CSS 选择符
1. id选择器（ # myid）
2. 类选择器（.myclassname）
3. 标签选择器（div, h1, p）
4. 相邻选择器（h1 + p）
5. 子选择器（ul > li）
6. 后代选择器（li a）
7. 通配符选择器（ * ）
8. 属性选择器（a[rel = "external"]）
9. 伪类选择器（a: hover, li:nth-child）

可继承的样式： font-size font-family color, text-indent;
不可继承的样式：border padding margin width height ;

清除浮动的几种方式,各自的优缺点：
使用空标签清除浮动 clear:both（理论上能清楚任何标签,,,增加无意义的标签）
使用overflow:auto（空标签元素清除浮动而不得不增加无意代码的弊端,,使用zoom:1用于兼容IE）
是用afert伪元素清除浮动(用于非IE浏览器)
