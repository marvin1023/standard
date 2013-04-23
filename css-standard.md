#CSS 部份
##基础
* css文件开始添加编码:`@charset "utf-8";`
* 选择器、属性和值都使用小写
* css请使用多行模式编写，上线之前再压缩（sublime text提供压缩的插件YUI Compressor，如果是用sass，可以选择直接解析成压缩的css）
* 使用简写模式（如：`border:1px solid #ccc;`）
* 代码缩进1个tab键(4个空格)
* z-index一般以5为一个步长（如50,55,60），方便以后增加或修改
* 请把所有前缀写在标准的前面(如-webkit-border-raidus:5px;-moz-border-raidus:5px;border-raidus:5px;)
* 不要写行内样式
* 不使用影响到页面性能expression表达式与filter，实现必要的特殊效果时，允许使用
* 使用!important请小心，确认是否有必要
* 请使用高效率选择器,可参阅[CSS选择器的优化](http://www.w3cplus.com/css/css-selector-performance)
* 使用clearfix或overflow清除子元素的浮动，而不是空标签
* 请不要直接定义标签样式(如span{}div{})
* 当值为0时的省略单位
* 样式表中中文字体名请使用转码后的unicode码，参阅：[css文件中的unicode参照](http://www.56.com/style/-doc-/v1/tpl/css_dev_spec/css_unicode.html)

###选择器权重
1. !important
2. 行内样式，指的是html文档中定义的style
3. ID选择器
4. 类，属性选择器和伪类选择器
5. 元素和伪元素

更多请查阅：[css选择器权重](http://www.w3cplus.com/css/css-specificity-things-you-should-know.html)

###注释
块级注释，用于布局结构或模块
	
	/* -------------------------------------------------
	 * block-hd
	 * -------------------------------------------------
	*/ 
	.block-hd{
	    line-height:30px;
	    text-align:right;
	}
	.block-hd h2{
	    float:left;
	}

单行注释，普通的注释
	 
	 /* more */
	.block-hd .more{
	    margin-right:10px;
	}

##各浏览器hack
请以标准浏览器为准书写css代码，如遇兼容问题，先考虑换实现方法，在万不得已的情况下，采用hack解决

###firefox
	
	/* Firefox 3+ */
	@-moz-document url-prefix() {}

###chrome及safari

	/* Chrome, Safari 3+ */
	@media screen and (-webkit-min-device-pixel-ratio:0) {}

###ie

选择器写法
	
	/* IE 6 and below */
	* html .selector  {} 
	
	/* IE 7 */
	*+html .selector {}
	
	/* IE 7 and below */
	.selector, {} 

属性写法

	.selector{
		color: blue\9; /* IE 6/7/8/9/10 */
		color: blue\9; /* IE 9/10 */
		*color:blue; /* ie6/7 */
		_color:blue; /* ie6 */
	}

更多请查阅：[hack速查英文版](http://browserhacks.com/) / [hack速查中文版](http://www.w3cplus.com/css/browser-hacks.html)

##图片优化
###图片本身的优化：

* 图像质量要求和图像文件大小决定你用什么格式的图片，用较小的图片文件呈现较好的图像质量。
* 当图片色彩过于丰富且无透明要求时，建议采用jpg格式并保存为较高质量。
* 当图片色彩过于丰富又有透明或半透明要求或阴影效果时，建议采用png24格式，并对IE6进行png8退化（或在不得已情况下使用滤镜）。
* 当图片色彩不太丰富时无论有无透明要求，请采用png8格式，大多数情况下建议采用这种格式。
* 当图片有动画时，只能使用gif格式。
* 你可以使用工具对图片进行再次压缩，但前提是不会影响色彩和透明。这里推荐几个优秀的在线压缩工具：[Smush.it](www.smushit.com/ysmush.it/)，[JPEGmini](http://jpegmini.com/main/shrink_photo)，[tiny png](http://tinypng.org/)

###图片合并（雪碧图）的使用：

多图合并注意事项

* 单个图标之间必须保留空隙，空隙大小由容器大小及显示方式决定。这样做的好处是既考虑了“容错性”又提高了图片的可维护性。
* 图标的排列方式排列方式分为以下几种：横向排列（容器宽度有限）、纵向排列（容器高度有限）、斜线排列（容器宽高不限），靠左排列（容器背景居左）、靠右排列（容器背景居右）、水平居中排列（容器背景水平居中）、垂直居中排列（容器背景垂直居中）。
* 合并后图片大小不宜超过50K，建议大小在20K-50K之间。
* 请保留雪碧图片的psd源文件，以方便后来的增删改，后来的所有的修改请在psd源文件中修改，然后再导出图片。

合并图片的一些原则（专题页面除外）

* 按照图片排列方式，把排列方式一样的图片进行合并，便于样式控制。
* 按照模块或元件，把同属于一个模块或元件的图片进行合并，方便模块或元件的维护。以导航模块为例，整个导航栏的icon为一个雪碧图片，而不是和其他的混合在一起，方便后来的修改或扩展。
* 按照图片大小，把大小一致或差不多的图片进行合并，可充分利用图片空间。
* 按照图片色彩，把色彩一致或差不多的图片进行合并，保证合并后图片的色彩不过于丰富，可防止色彩失真。


最后请不要过度使用sprite背景图片，而是按照或页面，或模块，或元件的方式合并为雪碧图，更好的考虑到未来的修改或扩展。


##参考资料：

* [NEC HTML规范](http://nec.netease.com/standard/html-structure.html)
* [56 HTML规范](http://www.56.com/style/-doc-/v1/tpl/)