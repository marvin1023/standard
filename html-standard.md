#HTML 部份

##基础

1. HTML标签名、属性名必须全部采用小写，属性必须加引号，并且必须闭合，单标签也必须闭合，如：`<input type=”text” />`、`<br />`	
2. 结构(html)，表现(css)，行为(js)相分离，避免直接将css或js写在标签结构里
3. link引入css文件放在head部分，script引入js文件放在body底部
4. id用下划线（#demo_zone），class用中划线（.pager-nav）
5. 请不要在内联元素中嵌入块级元素，如span里面有div标签，a里面包裹h2等
6. 标签挂靠的class不要过多，最多别超过4个
7. 数据内容，大胆的使用table
8. a元素提供title属性，img提供alt属性，如果img大小固定，请记得使用width和height属性（如`<img src="" alt="" width="200" 1. height="100">`），如果做的是响应式就不用加width和height了
9. 页面中不要使用&nbsp进行缩进，如需缩进，使用CSS的text-indent来控制，如text-indent:2em用于中文的缩进两个空格
10. 代码缩进使用tab键（四个空格）
12. 对于一个语义化的内部标签，应尽量避免使用className。比如在这样一个列表中，li标签中的itm应去除：`<ul class="m-help"><li class="itm"></li><li class="itm"></li></ul>`

##结构

###使用html5文档申明,语言为简体中文，编码格式为utf-8，并添加关键字和描述及favicon
	<!DOCTYPE HTML>
	<html lang="zh-cn">
	<head>
	<meta charset="UTF-8">
	<link href="/favicon.ico" rel="shortcut icon">
	<meta name="keywords" content="">
	<meta name="description" content="">	
	<title>天涯社区</title>
	</head>
	<body>
	 
	</body>
	</html>

###判断ie浏览器，加载所需文件

	//为ie6-8添加一个ie.css文件
	<!--[if lte IE 8]><link href="css/ie.css" type="text/css" rel="stylesheet" media="all"><![endif]-->
	
	//为ie6添加处理png的js文件及处理图片重复加载问题
	<!--[if IE 6]>
	      <script type="text/javascript" src="js/DD_belatedPNG_0.0.8a-min.js?_v=<%=JS_VERSION%>"></script>
	      <script type="text/javascript">
	          //给所有需要处理的png图片加上dd-pngifx这个class，就可以处理了
	          DD_belatedPNG.fix(".dd-pngfix");
	          //顺便处理下ie6的图片重复加载问题，这个在TY.js已经处理
	          document.execCommand("BackgroundImageCache",false,true);
	      </script>
	<![endif]-->

###注释
采用类似标签闭合的写法，与HTML统一格式；注释文案两头空格，与CSS注释统一格式
。
开始注释：`<!-- 注释文案 -->`（文案两头空格）；结束注释：`<!-- /注释文案 -->`（文案前加“/”符号，类似标签的闭合）；允许只有开始注释！      

	<!-- header -->
    <div id="header">
    	<div class="add-inner"></div>
    </div>
    <!-- /header -->

###常规布局(使用emmet语法)
这个布局的特点是外层的wrap用来承载全屏的背景，里层的add-inner用来承载border，margin，padding等。如果你使用sass等css预处理器可以干掉下面的clearfix这个class，而通过@include clearfix来搞定。
	
	.page.layout-lmr //整个外围
	.wrap-header>#header>.add-inner //header部分
	.wrap-container>#container.clearfix>(#aside_first>.add-inner)+（.wrap-mr.clearfix>(#main>.add-inner)+(#aside_second>.add-inner)） //container部分
	.wrap-footer>#footer>.add-inner //footer部分

###关于h1标题
在首页的时候，网站的h1标题为站点名字，当网站在内页的时候，内页标题为h1。所以对站点名字输出进行判断，以jsp为例：
	
	<% if(isIndexPage) { %>
	  <h1 class="visuallyhidden">天涯游戏</h1>
	<% }else { %>
	  <strong class="visuallyhidden">天涯游戏</strong>
	<% } %>

当然大多数时候其实我们一般是显示logo，而网站名称我们也许是需要隐藏的，所以需要添加visuallyhidden这个class
	
	.visuallyhidden{
		position: absolute;
    	clip:rect(1px 1px 1px 1px);
	}

###边栏区块
边栏区块是指左右边栏的区块，加有aside-block这个class，然后每个区块有一个属于自己的id，以方便协作查阅及日后修改。标题使用block-hd包裹，以方便扩展右侧信息，内容由block-bd这个class包括起来。当然如果边栏区块足够简单如就一张图片，那就根本就不需要这个结构了。

	//基本常见结构
	<div id="" class="aside-block">
	  <div class="block-hd">
	    <h2></h2>
	    <a href="#" class="more"></a>
	  </div>
	  <div class="block-bd"></div>
	</div>

	//另一个版本，可以通过绝对定位到标题同一行右侧，也可以放在下面的右侧，灵活性更强
	<div id="" class="aside-block">
	  <div class="block-hd">
	    <h2></h2> 
	  </div>
	  <div class="block-bd">
	  	...
	  	<a href="#" class="more"></a>
	  </div>
	</div>	

###内容区块
内容区块指主体内容的一些区块，加有section-block这个class，和边栏区块一样，每个区块有一个唯一的id，标题使用block-hd包裹，以方便扩展右侧信息，内容由block-bd这个class包括起来。

	<div id="" class="section-block">
	  <div class="block-hd"><h2></h2></div>
	  <div class="block-bd"></div>
	</div>

###多栏区块
这里的多栏区块指的是二等分，三等分或四等分的情况，二等分的时候class为col-two,三等分的class为col-three，四等分的class为col-four，然后子元素有一个共同的class为col-block。对于最后一栏margin的处理，可以采用加个class为last，或者使用父元素的负margin来撑大容器。

	//两列
	.col-two>.col-block*2>(.block-hd>h2)+.block-bd
	//三列
	.col-three>.col-block*3>(.block-hd>h2)+.block-bd
	//四列
	.col-four>.col-block*4>(.block-hd>h2)+.block-bd

##常用标签及标签语义化
* [HTML 5 参考手册](http://www.w3school.com.cn/html5/html5_reference.asp)
* [这样去写你的HTML](http://sofish.de/1688)
* [NEC 常用标签](http://nec.netease.com/standard/html-format.html)

##常用html转义符
* space空格(`&nbsp;`)
* 1个汉字空格(`&emsp;`)
* 小于号<(`&lt;`)
* 大于号>(`&gt;`)
* 连接号&(`&amp;`)
* 双引号"(`&quot;`)
* 单引号'(`&apos;`)
* 版权©(`&copy;`)
* 中点·(`&middot`)

##参考资料：

* [NEC HTML规范](http://nec.netease.com/standard/html-structure.html)
* [56 HTML规范](http://www.56.com/style/-doc-/v1/tpl/)
* [这样去写你的HTML](http://sofish.de/1688)