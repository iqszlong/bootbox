# bootbox.less

`bootbox.less` 是早期开发KPPW2.2所留下来的组件代码集，现在用于存放私有组件、补全less混合库和旧版样式。在KPPW2.5的使用中注释了和bootstrap中互相冲突的地方和冗余组件。bootbox实际上可以独立使用的，目前还没有把独立使用的文件分离出来，只能通过去掉注释来使用。`bootbox.less` 在编写上参考了bootstrap的写法，将组件分离以，引用文件的形式调用组件样式。


bootbox.less的内容：

	@import 'variable.less'; 		//存放变量（不输出）
	@import 'mixin.less';    		//存放混合类（不输出）
	
	@import 'resets.less';	 		//初始化
	//@import 'print.less';  		//打印（与bootstrap相同故注释）
	
	@import "scaffolding.less";		//脚手架 定义基本的html标签的样式
	
	@import 'grid.less';			//布局 定义基本布局
	@import 'base.less';			//kppw2.2旧版样式
	@import 'shortcut.less';		//定义less简写（不输出）

	//color
	@import 'brand-color.less';		//颜色变量定义 （不输出）

	//ui
	@import 'stars.less';			//星级评定
	//@import 'album.less';			//相册样式（暂时不使用）
	//@import 'icon.less';			//图片背景图标（使用字体图标代替故注释）
	@import 'list.less';			//列表样式
	@import 'nav.less';				//导航样式
	@import 'tab.less';				//选卡样式
	
	@import 'wallpaper.less';		//64位图片变量（不输出）


bootbox.less 参考 

+	[clearless <i class="fa fa-external-link-square"></i>](http://clearleft.github.io/clearless/)
+	[veryless <i class="fa fa-external-link-square"></i>](https://github.com/feichang/veryless)
+	[css参考 <i class="fa fa-external-link-square"></i>](http://www.w3school.com.cn/cssref/index.asp)

less学习

+	[LESS一种动态样式语言 <i class="fa fa-external-link-square"></i>](http://www.bootcss.com/p/lesscss/)
+	[Less.js 中文文档 <i class="fa fa-external-link-square"></i>](http://less.bootcss.com/)

less工具

+	[lesshat <i class="fa fa-external-link-square"></i>](http://lesshat.madebysource.com/)
+	[Koala - LESS/Sass/Compass/CoffeeScript编译工具 <i class="fa fa-external-link-square"></i>](http://koala-app.com/index-zh.html)

新增字体图标

+	[fontawesome 翻墙可看 ](http://fortawesome.github.io/Font-Awesome/)
+	[ionicons](http://ionicons.com/)


## variable.less

`variable.less` 为第一项，否则会编译出错，提示找不到对应的变量。其中包含了2个开关、4中颜色定义、页面字体、图片路径、`nav.less` 导航组件变量和`grid.less` 栅格变量

	//ie开关
	@disable-filters: 		false;//关闭ie滤镜
	@using-ieclasses: 		false;//打开ie样式 
	
	// 颜色
	@gary-color:			#fafafa;
	@solid-color:           @gray-lighter;
	@white-color:           white;
	@normal-color:          #666;
	
	@font-family-sans-serif: "\5FAE\8F6F\96C5\9ED1","Hiragino Sans GB";
	
	//图片路径
	@img-path:         		"../img/";
	
	//导航
	@nav-font-size-base: 		14px;
	@nav-height: 				45px;	
	@nav-link-padding-h:   		0px;
	@nav-link-padding-v:   		15px;
	
	//布局
	@column-width: 30;
	@gutter-width: 10;
	@columns: 24;
	//使用流式布局
	@total-width: 100%;
	//是否使用响应式布局
	@responsive: false;


## mixin.less
`mixin.less` 是混合类函数，不会生成css类，只能在less文件中调用生成对应的样式。

现有类列表：

1.	.font-size-rems(@px-size)
+	.font-size-ems(@target-px-size, @context-px-size:@base-font-size)
+	.font-face( @family-name, @font-path, @font-weight:normal, @font-style:normal, @include-svg:false ) when not (@include-svg)
	+	.font-face( @family-name, @font-path, @font-weight:normal, @font-style:normal, @include-svg:true ) when (@include-svg)
+	//.wrap-words()
+	//.tab-focus()
+	.border-radius(@radius:5px) 
+	.box-shadow(@shadow: 1px 1px 2px rgba(0,0,0,0.25))
	+	.box-shadow(@shadow_inset,@shadow_outset)
	+	.box-shadow(@shadow_one,@shadow_two,@shadow_three) 
+	.filter(@filter: grayscale(100%))
+	//.transition(@transition)
+	//.rotate(@rotation)
+	//.placeholder(@color: #DDD)
+	//.opacity(@transparency:50) when not (@disable-filters)
+	//.opacity(@transparency:50) when (@disable-filters)
+	//#gradient .horizontal (@start-color, @end-color) when not (@disable-filters)
	+	//#gradient .horizontal (@start-color, @end-color) when (@disable-filters)
	+	//#gradient .vertical (@start-color, @end-color) when (@disable-filters) 
	+	//#gradient .vertical (@start-color, @end-color) when not (@disable-filters) 
+	.clearfix() when not (@using-ieclasses)
	+	.clearfix() when (@using-ieclasses) 
+	.inline-block() when (@using-ieclasses) 
	+	.inline-block() when not (@using-ieclasses)
+	.ir() 
+	.hidden() 
+	.visually-hidden()
+	.size(@thesize) 
	+	.size(@width, @height)
+	.col(@column)
+	.retina-image(@file-1x, @file-2x, @width-1x, @height-1x)
+	.c-png24(@color, @url)
+	.background-clip(@background-clip: border-box)
+	.background-origin(@background-origin: padding-box)
+	.background-rgba(@red, @green, @blue, @alpha:1)
+	.background-size(@background-size: auto)
+	.resizable(@direction: both)
+	.flexbox()
+	.flex(@flex)
+	.flex-direction(@direction)
+	.order(@order)
+	.justify-content(@justify-method)
+	.align-items(@align-method)
+	.flex-wrap(@wrap-method)
+	.align-self(@value)
+	.user-select()
+	.fixed-width(@value)
+	.fixed-height(@value)
+	.brimming()
+	.selection(@color:#fff,@bg:#39f)
+	.msgrid()
+	.msgrid-site(@column,@row,@colspan,@rowspan)

注意：带 '//' 开头的是注释项目，主要是和bootstrap重复了。

注释了bootstrap已有的clearfix()，使用bootbox中的clearfix()增加了ie支持，注意使用时需要添加 `@using-ieclasses` 变量声明（值为'true'和'false'）。

### .font-size-rems()

根据 `@base-font-size` 和 `@px-size` 的值生成两个单位（px、rem）的字体大小，@px-size单位必须是像素。

	.font-size-rems(@px-size){
		@rem-size: @px-size / @base-font-size;
		font-size: ~"@{px-size}px"; 
		font-size: ~"@{rem-size}rem";
	}

例子

	/* less输入: */
	p {
	    .font-size-rems( 12 );
	}
	/* 输出css: */
	p {
	    font-size: 12px;    
	    font-size: 0.75rem;
	}


### .font-size-ems()

px像素值转换为ems的font-size属性。例如，如果您设置您的基本字体大小为62.5％，则只需设置 `@base-font-size` 值为10。

	.font-size-ems(@target-px-size, @context-px-size:@base-font-size) {
		font-size: (@target-px-size / @context-px-size) * 1em;
	}


*	`@target-px-size`：字体大小（像素）转换为ems。 
*	`@context-px-size`：当前上下文（可选）字体大小（以像素为单位）。如果未指定 `@base-font-size` 则取这个值。

例子
	
	/* less输入: */
	p {
	    .font-size-ems( 12 );
	}
	/* 输出css: */
	p {
	    font-size: 0.75em;
	}


### .font-face()

为文档设定新字体，字体文件需要几种格式（`*.eot`、`*.woff`、`*.ttf`、`*.svg`）其中 `*.svg` 为可选项。


	.font-face( @family-name, @font-path, @font-weight:normal, @font-style:normal, @include-svg:false ) when not (@include-svg) {
		@font-face {
		    font-family: @family-name;
		    src: url('@{font-path}.eot');
		    src: url('@{font-path}.eot?#iefix') format('embedded-opentype'),
		         url('@{font-path}.woff') format('woff'),
		         url('@{font-path}.ttf') format('truetype');
		    font-weight: @font-weight;
		    font-style: @font-style;
		}
	}


	.font-face( @family-name, @font-path, @font-weight:normal, @font-style:normal, @include-svg:true ) when (@include-svg) {
		@font-face {
		    font-family: @family-name;
		    src: url('@{font-path}.eot');
		    src: url('@{font-path}.eot?#iefix') format('embedded-opentype'),
		         url('@{font-path}.woff') format('woff'),
		         url('@{font-path}.ttf') format('truetype'),
				 url('@{font-path}.svg#@{family-name}') format('svg');
		    font-weight: @font-weight;
		    font-style: @font-style;
		}
	}



*	`@font-family`：字体名称，用来调用字体的名称。 
*	`@font-path`：字体路径，css文件访问字体文件的路径。
*	`@font-weight`: (可选) 加粗属性的值. 默认为 `normal`
*	`@font-style`: (可选) 文字样式的值. 默认为 `normal`
*	`@include-svg`: SVG格式字体。

### .wrap-words()

文字换行，强制换行

	.wrap-words() {
		-ms-word-break: break-all;
		word-break: break-all;
		word-break: break-word;
	 	-webkit-hyphens: auto;
	 	-moz-hyphens: auto;
	 	hyphens: auto;
	 }



###.tab-focus() 

谷歌内核选卡聚焦样式

	 .tab-focus() {
	   // Default
	   outline: thin dotted #333;
	   // Webkit
	   outline: 5px auto -webkit-focus-ring-color;
	   outline-offset: -2px;
	 }


### .border-radius()

圆角，设置圆角

	.border-radius(@radius:5px) {
	    -webkit-border-radius: @arguments;
		-moz-border-radius: @arguments;
		border-radius: @arguments;
		// 背景不超出圆角
		-moz-background-clip: padding; 
		-webkit-background-clip: padding-box; 
		background-clip: padding-box;
	}

*	`@radius` 是圆角的弧度,默认5px。

例子

	/* less输入 */
	.example1 {
	    .border-radius( 5px );
	}
	.example2 {
	    .border-radius( 5px, 7px, 5px, 10px );
	}
	/* 输出css: */
	.example1 {
	    -moz-border-radius: 5px;
	    border-radius: 5px;
	}
	.example2 {
	    -webkit-border-top-left-radius: 5px;
	    -webkit-border-top-right-radius: 7px;
	    -webkit-border-bottom-left-radius: 5px;
	    -webkit-border-bottom-right-radius: 10px;
	    -moz-border-radius-topleft: 5px;
	    -moz-border-radius-topright: 7px;
	    -moz-border-radius-bottomleft: 5px;
	    -moz-border-radius-bottomright: 10px;
	    border-top-left-radius: 5px;
	    border-top-right-radius: 7px;
	    border-bottom-left-radius: 5px;
	    border-bottom-right-radius: 10px;
	}


### .box-sizing()

css3中box-sizing属性的兼容写法。


	.box-sizing(@type: border-box) {
		-moz-box-sizing: @type;
		-webkit-box-sizing: @type;
		-ms-box-sizing: @type;
		box-sizing: @type;
	}
例子：

	/* less输入: */
	.example {
	    .box-sizing( border-box );
	}
	/* 输出css: */
	.example {
	    -moz-box-sizing: border-box;
	    -webkit-box-sizing: border-box;
	    -ms-box-sizing: border-box;
	    box-sizing: border-box;
	}



### .box-shadow()

css3中box-shadow属性的兼容写法。
	
	.box-shadow(@shadow: 1px 1px 2px rgba(0,0,0,0.25)) {
		-webkit-box-shadow: @shadow;
		-moz-box-shadow: @shadow;
		box-shadow: @shadow;
	}

例子：

	/* less输入: */
	.example {
	    .box-shadow( 2px 2px 3px #999 );
	}
	/* 输出css: */
	.example {
	    -webkit-box-shadow: 2px 2px 3px #999;
	    -moz-box-shadow: 2px 2px 3px #999;
	    box-shadow: 2px 2px 3px #999;
	}

### .filter()

css3滤镜属性，了解更多 [-webkit-filter是神马？ <i class="fa fa-external-link-square"></i>](http://www.qianduan.net/what-is-webkit-filter.html)

	.filter(@filter: grayscale(100%)) {
		-webkit-filter: @filter;
		-moz-filter: @filter;
		-ms-filter: @filter;
		-o-filter: @filter;
		filter: @filter;
	}

### .transition()

css3动画过渡属性，了解更多 [CSS3动画参考 <i class="fa fa-external-link-square"></i>](http://ecd.tencent.com/css3/guide.html?transition-property)



	.transition(@transition) {
	   -webkit-transition: @transition;
	           transition: @transition;
	}
	.transition-delay(@transition-delay) {
	   -webkit-transition-delay: @transition-delay;
	           transition-delay: @transition-delay;
	}
	.transition-duration(@transition-duration) {
	   -webkit-transition-duration: @transition-duration;
	           transition-duration: @transition-duration;
	}
	.transition-transform(@transition) {
	   -webkit-transition: -webkit-transform @transition;
	      -moz-transition: -moz-transform @transition;
	        -o-transition: -o-transform @transition;
	           transition: transform @transition;
	}

例子

	/* less输入: */
	.example {
	    .transition( all .2s ease-in-out );
	}
	/* 输出css: */
	.example {
	    -webkit-transition: all .2s ease-in-out;
	    -moz-transition: all .2s ease-in-out;
	    transition: all .2s ease-in-out;
	}


### .rotate()

css3旋转属性， [CSS3动画参考 <i class="fa fa-external-link-square"></i>](http://ecd.tencent.com/css3/guide.html?rotate)

	.rotate(@rotation) {
		-webkit-transform: rotate(@rotation);
	 	-moz-transform: rotate(@rotation);
	 	-o-transform: rotate(@rotation);
	 	transform: rotate(@rotation);
	}

例子

	/* less输入: */
	.example {
	    .rotate( 2.5deg );
	}
	/* 输出css: */
	.example {
	    -webkit-transform: rotate(2.5deg);
	    -moz-transform: rotate(2.5deg);
	    -o-transform: rotate(2.5deg);
	    transform: rotate(2.5deg);
	}


### .placeholder()

输入框占位符样式

	
	.placeholder(@color: #DDD) {
	 	:-moz-placeholder {
	 		color: @color;
	 	}
	 	::-webkit-input-placeholder {
	 		color: @color;
	 	}
	}

例子：

	/* less输入: */
	.placeholder( #F00 );
	/* 输出css: */
	:-moz-placeholder {
	    color: #F00;
	}
	::-webkit-input-placeholder {
	    color: #F00;
	}


### .opacity()

透明度，默认透明度是50%。

	.opacity(@transparency:50) when not (@disable-filters){
		opacity:@transparency/100;
		-moz-opacity:@transparency/100;
		-khtml-opacity: @transparency/100;
		filter:alpha(opacity=@transparency);
	}
	
	.opacity(@transparency:50) when (@disable-filters){
		opacity:@transparency/100;
		-moz-opacity:@transparency/100;
		-khtml-opacity: @transparency/100;
	}


### #gradient > .vertical()

css3渐变，

	#gradient {
		.horizontal (@start-color, @end-color) when not (@disable-filters) {
			background-color: @end-color;
			background-repeat: repeat-x;
			background-image: -khtml-gradient(linear, left top, right top, from(@start-color), to(@end-color)); /* Konqueror */
			background-image: -moz-linear-gradient(left, @start-color, @end-color); /* FF 3.6+ */
			background-image: -ms-linear-gradient(left, @start-color, @end-color); /* IE10 */
			background-image: -webkit-gradient(linear, left top, right top, color-stop(0%, @start-color), color-stop(100%, @end-color)); /* Safari 4+, Chrome 2+ */
			background-image: -webkit-linear-gradient(left, @start-color, @end-color); /* Safari 5.1+, Chrome 10+ */
			background-image: -o-linear-gradient(left, @start-color, @end-color); /* Opera 11.10 */
			background-image: -ms-linear-gradient(left, @start-color 0%, @end-color 100%);  /* IE10+ */
			background-image: linear-gradient(left, @start-color, @end-color); /* the standard */
			filter: e(%("progid:DXImageTransform.Microsoft.gradient(startColorstr='%d', endColorstr='%d', GradientType=1)",@start-color,@end-color)); /* IE6 & IE7 */
			-ms-filter: %("progid:DXImageTransform.Microsoft.gradient(startColorstr='%d', endColorstr='%d', GradientType=1)",@start-color,@end-color); /* IE8+ */
		}
		.horizontal (@start-color, @end-color) when (@disable-filters) {
			background-color: @end-color;
			background-repeat: repeat-x;
			background-image: -khtml-gradient(linear, left top, right top, from(@start-color), to(@end-color)); /* Konqueror */
			background-image: -moz-linear-gradient(left, @start-color, @end-color); /* FF 3.6+ */
			background-image: -ms-linear-gradient(left, @start-color, @end-color); /* IE10 */
			background-image: -webkit-gradient(linear, left top, right top, color-stop(0%, @start-color), color-stop(100%, @end-color)); /* Safari 4+, Chrome 2+ */
			background-image: -webkit-linear-gradient(left, @start-color, @end-color); /* Safari 5.1+, Chrome 10+ */
			background-image: -o-linear-gradient(left, @start-color, @end-color); /* Opera 11.10 */
			background-image: -ms-linear-gradient(left, @start-color 0%, @end-color 100%);  /* IE10+ */
			background-image: linear-gradient(left, @start-color, @end-color); /* the standard */
		}
		.vertical (@start-color, @end-color) when (@disable-filters)  {
			background-color: @end-color;
			background-repeat: repeat-x;
			background-image: -khtml-gradient(linear, left top, left bottom, from(@start-color), to(@end-color)); /* Konqueror */
			background-image: -moz-linear-gradient(@start-color, @end-color); /* FF 3.6+ */
			background-image: -ms-linear-gradient(@start-color, @end-color); /* IE10 */
			background-image: -webkit-gradient(linear, left top, left bottom, color-stop(0%, @start-color), color-stop(100%, @end-color)); /* Safari 4+, Chrome 2+ */
			background-image: -webkit-linear-gradient(@start-color, @end-color); /* Safari 5.1+, Chrome 10+ */
			background-image: -o-linear-gradient(@start-color, @end-color); /* Opera 11.10 */
			background-image: -ms-linear-gradient(top, @start-color 0%, @end-color 100%);  /* IE10+ */
			background-image: linear-gradient(@start-color, @end-color); /* the standard */
		}
		.vertical (@start-color, @end-color) when not (@disable-filters)  {
			background-color: @end-color;
			background-repeat: repeat-x;
			background-image: -khtml-gradient(linear, left top, left bottom, from(@start-color), to(@end-color)); /* Konqueror */
			background-image: -moz-linear-gradient(@start-color, @end-color); /* FF 3.6+ */
			background-image: -ms-linear-gradient(@start-color, @end-color); /* IE10 */
			background-image: -webkit-gradient(linear, left top, left bottom, color-stop(0%, @start-color), color-stop(100%, @end-color)); /* Safari 4+, Chrome 2+ */
			background-image: -webkit-linear-gradient(@start-color, @end-color); /* Safari 5.1+, Chrome 10+ */
			background-image: -o-linear-gradient(@start-color, @end-color); /* Opera 11.10 */
			background-image: -ms-linear-gradient(top, @start-color 0%, @end-color 100%);  /* IE10+ */
			background-image: linear-gradient(@start-color, @end-color); /* the standard */
			filter: e(%("progid:DXImageTransform.Microsoft.gradient(startColorstr='%d', endColorstr='%d', GradientType=0)",@start-color,@end-color)); /* IE6 & IE7 */
			-ms-filter: %("progid:DXImageTransform.Microsoft.gradient(startColorstr='%d', endColorstr='%d', GradientType=0)",@start-color,@end-color); /* IE8+ */
		}
	}


*	`@start-color` 开始颜色
*	`@end-color` 结束颜色
*	`@disable-filters` IE滤镜开关

例子（纵向）：

	/* less输入: */
	.example {
	    #gradient > .vertical( #F00, #555);
	}
	/* 输出css: */
	.example {
	    background-color: #555;
	    background-repeat: repeat-x;
	    background-image: -khtml-gradient(linear, left top, left bottom, from(#F00), to(#555));
	    background-image: -moz-linear-gradient(#F00, #555);
	    background-image: -ms-linear-gradient(#F00, #555);
	    background-image: -webkit-gradient(linear, left top, left bottom, color-stop(0%, #F00), color-stop(100%, #555));
	    background-image: -webkit-linear-gradient(#F00, #555);
	    background-image: -o-linear-gradient(#F00, #555);
	    background-image: -ms-linear-gradient(top, #F00 0%, #555 100%);
	}


例子（横向）:

	/* less输入: */
	.example {
	    #gradient > .horizontal( #F00, #555);
	}
	/* 输出css: */
	.example {
	    background-color: #555;
	    background-repeat: repeat-x;
	    background-image: -khtml-gradient(linear, left top, right top, from(#F00), to(#555));
	    background-image: -moz-linear-gradient(left, #F00, #555);
	    background-image: -ms-linear-gradient(left, #F00, #555);
	    background-image: -webkit-gradient(linear, left top, right top, color-stop(0%, #F00), color-stop(100%, #555));
	    background-image: -webkit-linear-gradient(left, #F00, #555);
	    background-image: -o-linear-gradient(left, #F00, #555);
	    background-image: -ms-linear-gradient(left, #F00 0%, #555 100%);
	    background-image: linear-gradient(left, #F00, #555);
	}



### .clearfix()

清除浮动

	.clearfix() when not (@using-ieclasses) {
		&:before,
		&:after {
		    content: "";
		    display: table;
		}
		&:after {
		    clear: both;
		}
		*zoom: 1;
	}
	
	.clearfix() when (@using-ieclasses) {
		&:before,
		&:after {
		    content: "";
		    display: table;
		}
		&:after {
		    clear: both;
		}
		#ie6 &, #ie7 & {
			zoom: 1;
		}
	}

*	`@using-ieclasses` IE兼容开关

例子

	/* less输入: */
	.example {
	    .clearfix();
	}
	/* 输出css: */
	.example:before,
	.example:after {
	    content: "";
	    display: table;
	}
	.example:after {
	    clear: both;
	}
	#ie6 .example,
	#ie7 .example {
	    zoom: 1;
	}


### .inline-block()

inline-block增加ie7兼容

	//内敛
	.inline-block() when (@using-ieclasses) {
		display: inline-block;
		#ie7 & {
			display: inline;
			zoom: 1;
		}
	}
	
	.inline-block() when not (@using-ieclasses) {
		display: inline-block;
		*display: inline;
		*zoom: 1;
	}

*	`@using-ieclasses` IE兼容开关

例子：

	/* less输入: */
	.example {
	    .inline-block();
	}
	/* 输出css: */
	.example {
	    display: inline-block
	}
	#ie7 .example {
	    display: inline;
	    zoom: 1;
	}

### .ir()

用背景代替文字显示内容

	.ir() {
		border: 0;
		font: 0/0 a;
		text-shadow: none;
		color: transparent;
		background-color: transparent;
	}

例子：

	/* less输入: */
	.example {
	    .ir();
	    background-image: url('/text.png');
	}
	/* 输出css: */
	.example {
	    border: 0;
	    font: 0/0 a;
	    text-shadow: none;
	    color: transparent;
	    background-color: transparent;
	    background-image: url('/text.png');
	}

### .hidden()

隐藏内容

	.hidden() {
		display: none !important;
		visibility: hidden;
	}

例子：
	
	/* less输入: */
	.example {
	    .hidden();
	}
	/* 输出css: */
	.example {
	    display: none !important;
	    visibility: hidden;
	}

### .visually-hidden()

隐藏元素但允许键盘聚焦和屏幕阅读器识别内容

	.visually-hidden() {
		border: 0;
		clip: rect(0 0 0 0);
		height: 1px;
		margin: -1px;
		overflow: hidden;
		padding: 0;
		position: absolute;
		width: 1px;
		&.focusable:active,
		&.focusable:focus {
		    clip: auto;
		    height: auto;
		    margin: 0;
		    overflow: visible;
		    position: static;
		    width: auto;
		}
	}

例子

	/* less输入: */
	.example {
	    .visually-hidden();
	}
	/* 输出css: */
	.example {
	    border: 0;
	    clip: rect(0 0 0 0);
	    height: 1px;
	    margin: -1px;
	    overflow: hidden;
	    padding: 0;
	    position: absolute;
	    width: 1px;
	}
	.example.focusable:active,
	.example.focusable:focus {
	    clip: auto;
	    height: auto;
	    margin: 0;
	    overflow: visible;
	    position: static;
	    width: auto;
	}


###  .size()

设置元素的宽和高

	.size(@thesize) {
		width: @thesize;
		height: @thesize;
	}
	
	.size(@width, @height) {
		width: @width;
		height: @height;
	}

*	`@size` 同时设置相同的宽和高属性
*	`@width` 单独设置宽度属性
*	`@height` 单独设置高度属性

例子

	/* less输入: */
	.example1 {
	    .size( 30px );
	}
	.example2 {
	    .size( 20px, 70px );
	}
	/* 输出css: */
	.example1 {
	    width: 30px;    
	    height: 30px;
	}
	.example2 {
	    width: 20px;
	    height: 70px;
	}

### .col()

百分比列，将宽度以百分比等分出几列。

	
	.col(@column){
		display: inline;
		float: left;
		width:100/@column *1%;
	}


*	`@column` 是列的个数

例子

	/* less输入: */
	.example1 {
	    .col(2);
	}
	/* 输出css: */
	.example1 {
		display: inline;
		float: left;
	    width: 50%;    
	}

### .retina-image()

视网膜屏幕图片，1倍大小和双倍大小的背景图片自动判断在视网膜屏幕上切换显示。

	.retina-image(@file-1x, @file-2x, @width-1x, @height-1x) {
	  background-image: url("@{file-1x}");
	
	  @media
	  only screen and (-webkit-min-device-pixel-ratio: 2),
	  only screen and (   min--moz-device-pixel-ratio: 2),
	  only screen and (     -o-min-device-pixel-ratio: 2/1),
	  only screen and (        min-device-pixel-ratio: 2),
	  only screen and (                min-resolution: 192dpi),
	  only screen and (                min-resolution: 2dppx) {
	    background-image: url("@{file-2x}");
	    background-size: @width-1x @height-1x;
	  }
	}

*	`@file-1x` 1倍大小图片路径。
*	`@file-2x` 2倍大小图片路径。
*	`@width-1x` 1倍大小背景显示区域的宽度，背景图会拉伸处理
*	`@height-1x` 1倍大小背景显示区域的高度，背景图会拉伸处理


例子

	// less输入
	.jumbotron {
	   .retina-image("/img/bg-1x.png", "/img/bg-2x.png", 100px, 100px);
	}

### .c-png24()

png24位图片背景透明，主要是兼容IE6写的。

	.c-png24(@color, @url){
		background: @color url("@{url}") no-repeat 0 0;
	    _background: @color none;
	    filter: ~"progid:DXImageTransform.Microsoft.AlphaImageLoader(src='@{url}', sizingMethod='scale')";
	}

*	`@color` 背景颜色
*	`@url` 图片路径（注意：路径最好是绝对路径或者网络路径，否则会出现IE6读不出图片的问题。）

例子

	.c-png24(#ccc, "http://taobao.com/logo.jpg");


### .background-clip()

背景覆盖的位置，规定背景的绘制区域 [查看更多 <i class="fa fa-external-link-square"></i>](http://www.w3school.com.cn/cssref/pr_background-clip.asp)


	.background-clip(@background-clip: border-box){
		-moz-background-clip: @background-clip;
		  -webkit-background-clip: @background-clip;
			background-clip: @background-clip;
	}

*	`@background-clip` 默认值是border-box。取值范围是 border-box | padding-box | content-box。


### .background-origin()

背景开始的位置，相对于内容框来定位背景图像 [查看更多 <i class="fa fa-external-link-square"></i>](http://www.w3school.com.cn/cssref/pr_background-origin.asp)

	.background-origin(@background-origin: padding-box){
		-moz-background-origin: @background-origin;
		  -webkit-background-origin: @background-origin;
		    background-origin: @background-origin;
	}


*	`@background-origin` 默认值是padding-box。取值范围是 padding-box | border-box | content-box;


### .background-rgba()

背景半透明

	.background-rgba(@red, @green, @blue, @alpha:1){
	
			@filtercolor:`(_f = function(d){ var v = (parseInt(d)|0).toString(16);return v.length<2 ? "0"+v : v;},
							'#'+_f(@{alpha}*255) + _f(@{red}) + _f(@{green})+ _f(@{blue}))`;
			
			background-color: ~'rgba(@{red},@{green},@{blue},@{alpha})';
	    -ms-filter:~"progid:DXImageTransform.Microsoft.gradient(startColorstr='@{filtercolor}',endColorstr='@{filtercolor}')";
	    filter:~"progid:DXImageTransform.Microsoft.gradient(startColorstr='@{filtercolor}',endColorstr='@{filtercolor}')";	
	}

*	`@red, @green, @blue` rgb颜色的取值
*	`@alpha` 透明度的值，默认值是1（不透明）。取值范围是0~1。

### .background-size()

背景图片的尺寸 [查看更多 <i class="fa fa-external-link-square"></i>](http://www.w3school.com.cn/cssref/pr_background-size.asp)

	.background-size(@background-size: auto){
		-moz-background-size: @background-size;
		  -webkit-background-size: @background-size;
		    -o-background-size: @background-size;
		      background-size: @background-size;
	}


### .resizable()

元素允许被调整宽高。

	.resizable(@direction: both) {
	  resize: @direction;
	  overflow: auto; // Safari fix
	}

*	`@direction` 默认值both，取值范围 horizontal, vertical, both

### .flexbox()

伸缩容器布局方式：box，css3中新的快速布局方式 包含旧版和新版box布局

注：该布局方式和columns布局方式不能同时使用。

[参考资料（En） <i class="fa fa-external-link-square"></i>](http://bocoup.com/weblog/dive-into-flexbox/)   [参考资料（中文） <i class="fa fa-external-link-square"></i>](http://www.w3cplus.com/css3/flexbox-basics.html)  [less代码来源 <i class="fa fa-external-link-square"></i>](https://github.com/RubyLouvre/myless/blob/master/flexbox.less) [维基百科 <i class="fa fa-external-link-square"></i>](http://www.w3.org/html/ig/zh/wiki/Css3-flexbox/zh-hans)

### .flex(@flex)

flex用来决定伸缩项目的伸缩性。一个伸缩容器会等比地按照各伸缩项目的扩展比率分配剩余空间，也会按照收缩比率缩小各项目以避免溢出。

* `flex-grow` 此属性值为正数值，用来设置扩展比率，也就是剩余空间是正值的时候此伸缩项目相对于伸缩容器里其他伸缩项目能分配到空间比例。若省略则会被设置为“1”。

* `flex-shrink` 此属性值为正数值，用来设置收缩比率，也就是剩余空间是负值的时候此伸缩项目相对于伸缩容器里其他伸缩项目能收缩的空间比例。若省略则会被设置为“1”，在收缩的时候收缩比率会以伸缩基准值加权。

* `flex-basis` 与width属性使用相同的值，可以用来设置flex-basis长写并指定伸缩基准值，也就是根据可伸缩比率计算 出剩余空间的分布之前，伸缩项目主轴长度的起始数值。若在flex缩写省略了此属性设置，则flex-basis的指定值是“0”，若flex-basis的指定值是“auto”，则伸缩基准值的指定值是元素主轴长度属性的值。

理论上是需要设定3个值的，但实际应用中可以只设1个值，部分浏览器会自动补全后面两个值。


### .flex-direction(@direction)

flex-direction属性可以用来设定伸缩容器的主轴的方向，这也决定了用户代理配置伸缩项目的方向。主要适用于伸缩容器，`@direction`主要包括以下几个值：

* `row`flex-direction的默认值，表示伸缩容器的主轴与当前书写模式的行内轴（文字布局的主要主向）。主轴起点与主轴终点方向分别等同于当前书写模式的始与结方向。
* `row-reverse`表示的是除了主轴起点与主轴终点方向交换以外同row属性值的作用。
* `column` 表示的是伸缩容器的主轴与当前书写模式的块轴（块布局的主要方向）同向。主轴起点与主轴终点方向分别等同于当前书写模式的前与后方向。简单的可以理解为列布局。
* `column-reverse` 表示的是除了主轴起点与主轴终点方向交换以外同“column”的属性值作用。

### .order(@order)

order属性是用来设置伸缩项的显示顺序，默认状态下，用户代理会用伸缩项目出现在源文档的次序配置这些伸缩项目。order属性透过将元素分到有序号的组以控制元素出现的顺序。在伸缩布局中，order属性控制伸缩项目在伸缩容器里的顺序。
`@order`取值越大，越排在后面。并且`@order`可以取负值。

### .justify-content(@justify-method)

justify-content属性主要用来设置伸缩项目沿主轴的对齐方式，从而调整伸缩项目之间的间距。设置了这个属性，在主轴方向上设置的任何margin都不会起作用。`@justify-method` 包括一下几个值：

* `flex-start` 伸缩项目向一行的起始位置靠齐。该行的第一个伸缩项目在主轴起点边的外边距与该行在主轴起点的边对齐，同时所有后续的伸缩项目与其前一个项目对齐。
* `flex-end` 伸缩项目向一行的结束位置靠齐。该行的最后一个伸缩项目在主轴终点边的外边距与该行在主轴终点的边对齐，同时所有前面的伸缩项目与其后一个项目对齐。
* `center` 伸缩项目向一行的中间位置靠齐。该行的伸缩项目将相互对齐并在行中居中对齐，同时第一个项目与该行的在主轴起点的边的距离等同与最后一个项目与该行在主轴终点的边的距离（如果剩余空间是负数，则保持两端溢出的长度相等）。
* `space-between` 伸缩项目会平均地分布在一行里。如果剩余空间是负数，或该行只有一个伸缩项目，则此值等效于「flex-start」。在其它情况下，第一个项目在主轴起点边的外边距会与该行在主轴起点的边对齐，同时最后一个项目在主轴终点边的外边距与该行在主轴终点的边对齐，而剩下的伸缩项目在确保两两之间的空白空间相等下平均分布。

### .align-items(@align-method)

align-items属性，它充许您调整伸缩项目在侧轴的对齐方式，`@align-method` 主要包括以下几个值：

* `flex-start/baseline` 伸缩项目在侧轴起点边的外边距紧靠住该行在侧轴起点的边。
* `flex-end` 伸缩项目在侧轴终点边的外边距靠住该行在侧轴终点的边。
* `center` 伸缩项目的外边距盒在该行的侧轴上居中放置。（如果伸缩行的尺寸小于伸缩项目，则伸缩项目会向两个方向溢出相同的量）。
* `stretch` 伸缩项目拉伸，填满整个侧轴（注意：如果伸缩伸缩的高度有限制，此可能导致伸缩项目的内容溢出该项目。
伸缩项目在侧轴起点边的外边距会紧靠住该行在侧轴起点的边。）

### .flex-wrap(@wrap-method)

flex-wrap属性主要用来控制伸缩容器是单行还是多行，也决定了侧轴方向一新的一行的堆放方向。主要适用于伸缩容器，`@wrap-method` 主要包括以下几个值：

* `nowrap` flex-wrap的默认值，表示的是伸缩容器为单行。侧轴起点方向等同于当前书写模式的起点或前/头在侧轴的那一边，而侧轴终点方向是侧轴起点的相反方向。
* `wrap` 表示的是伸缩容器为多行。侧轴起点方向等同于当前书写模式的起眯或前/头在侧轴的那一边，而侧轴终点方向是侧轴起点的相反方向。
* `wrap-reverse` 除了侧轴起点与侧轴终点方向交换以外同wrap所起作用相同。
*

### .align-self(@value)

 align-self 用来在单独的伸缩项目上覆写默认的对齐方式。（对于匿名伸缩项目，「align-self」的值永远与其关联的伸缩容器的「align-items」的值相同。）`@value`的值为：`flex-start`、`flex-end`、`center`、`stretch`

### .user-select()

用户是否可选内容，使用后用户无法选择内容。

### .brimming()

充满整个，宽高将设定为100%；

### .selection(@color:#fff,@bg:#39f)

用户选择内容的底色和字体颜色

* `@color` 前景色
* `@bg` 背景色

### .msgrid()

显示为grid布局与.msgrid-site()配合使用

微软IE10+栅格布局 [参考资料（En） <i class="fa fa-external-link-square"></i>](http://msdn.microsoft.com/en-us/library/ie/hh673533(v=vs.85).aspx) [参考资料（中文） <i class="fa fa-external-link-square"></i>](http://www.w3cplus.com/css3/css3-grid-layout-module.html)

### .msgrid-site(@column,@row,@colspan,@rowspan)

* `@column` 定义列
* `@row` 定义行
* `@colspan` 跨越的列
* `@rowspan` 跨越的行


## resets.less

`resets.less` 包含两种重置文档格式 normalize() 和 reset()。normalize()是带基本的html标记样式的，reset()是去掉了所有的html基本样式。默认设置为reset()。

*	normalize文档来源 [github <i class="fa fa-external-link-square"></i>](http://github.com/necolas/normalize.css)
*	reset文档来源 [meyerweb <i class="fa fa-external-link-square"></i>](http://meyerweb.com/eric/tools/css/reset/)



## scaffolding.less

脚手架的一些定义，由于和bootstrap重复了，所以基本上只保留了不同的内容。

	/* 统一上标和下标 */
	  sub, sup {
	    font-size: 75%;
	    line-height: 0;
	    position: relative;
	    vertical-align: text-top;
	  }
	
	  :root sub, :root sup{
	    vertical-align: baseline; /* for ie9 and other mordern browsers */
	  }
	  sup {
	    top: -0.5em;
	  }
	  sub {
	    bottom: 0;
	  }

内容参照了 [typo <i class="fa fa-external-link-square"></i>](http://typo.sofi.sh/)


## grid.less

栅格定义，主要用于定义布局的宽度。

	
	
	// Utility variable — you should never need to modify this
	@gridsystem-width: (@column-width*@columns) + (@gutter-width*@columns) * 1px;
	
	// Set @total-width to 100% for a fluid layout
	@total-width: @gridsystem-width;

	.container when not (@responsive){ width:@total-width; margin: auto; }
	
	.row(@columns:@columns) {
		display: block;
		width: @total-width*((@gutter-width + @gridsystem-width)/@gridsystem-width);
		margin: 0 @total-width*(((@gutter-width*.5)/@gridsystem-width)*-1);
		// *width: @total-width*((@gutter-width + @gridsystem-width)/@gridsystem-width)-@correction;
		// *margin: 0 @total-width*(((@gutter-width*.5)/@gridsystem-width)*-1)-@correction;
		.clearfix;
	}
	.column(@x,@columns:@columns) {
		display: inline;
		float: left;
		width: @total-width*((((@gutter-width+@column-width)*@x)-@gutter-width) / @gridsystem-width);
		margin: 0 @total-width*((@gutter-width*.5)/@gridsystem-width);
		// *width: @total-width*((((@gutter-width+@column-width)*@x)-@gutter-width) / @gridsystem-width)-@correction;
		// *margin: 0 @total-width*((@gutter-width*.5)/@gridsystem-width)-@correction;
	}
	.push(@offset:1) {
		margin-left: @total-width*(((@gutter-width+@column-width)*@offset) / @gridsystem-width) + @total-width*((@gutter-width*.5)/@gridsystem-width);
	}
	.pull(@offset:1) {
		margin-right: @total-width*(((@gutter-width+@column-width)*@offset) / @gridsystem-width) + @total-width*((@gutter-width*.5)/@gridsystem-width);
	}


*	`@column-width` 默认值30，代表栅格的列宽。
*	`@gutter-width` 默认值10，代表栅格的间距。
*	`@columns`默认值24，代表栅格的列数。
*	`@gridsystem-width, @total-width` 栅格总宽度，不需要定义，直接会计算出来。
*	`@responsive` 是否使用响应式，由于此布局为固定布局，故只用于非响应式布局。

### .row()

栅格占一行，根据设定的栅格列数计算出一行的宽度。和bootstrap的row不相同的地方就是会有宽度在里面。

例子

	.setRow{
		.row(24);
	}

	.setRow{
		display: block;
		width:950px;
		margin:0 -10px;
	}
	

### .column()

设置栅格列数

	.column(@x,@columns:@columns) {
		display: inline;
		float: left;
		width: @total-width*((((@gutter-width+@column-width)*@x)-@gutter-width) / @gridsystem-width);
		margin: 0 @total-width*((@gutter-width*.5)/@gridsystem-width);
		// *width: @total-width*((((@gutter-width+@column-width)*@x)-@gutter-width) / @gridsystem-width)-@correction;
		// *margin: 0 @total-width*((@gutter-width*.5)/@gridsystem-width)-@correction;
	}


例子
	
	/* less输入 */
	.main{
		.column(2);
	}
	
	/* 输出css */
	.main {
	  display: inline;
	  float: left;
	  width: 70px;
	  margin: 0 5px;
	}

### .push()

向左边留出空白。默认为1列的宽度

	.push(@offset:1) {
		margin-left: @total-width*(((@gutter-width+@column-width)*@offset) / @gridsystem-width) + @total-width*((@gutter-width*.5)/@gridsystem-width);
	}
	

例子
	
	/* less 输入 */
	.main{
		.push(2);
	}
	/* 输出css */
	.main {
	  margin-left: 85px;
	}


### .pull()

向右边边留出空白。默认为1列的宽度

例子
	
	/* less 输入 */
	.main{
		.pull(2);
	}
	/* 输出css */
	.main {
	  margin-right: 85px;
	}


## base.less

`base.less` 里面主要是一些零散样式大部分是直接输出成css在页面上使用的。

*	`.font_simsun` 	字体为宋体
*	`.ov_visibel`		超出显示
*	`.ov_hide`		超出隐藏
*	`.ws_normal`		文字普通显示
*	`.ws_break`		文字强制换行
*	`.ws_prewrap`		文字显示空格
*	`.ws_hide`		文字不换行隐藏
*	`.t_l`			文字左对齐
*	`.t_c`			文字居中对齐
*	`.t_r`			文字右对齐
*	`.block`			块级显示元素
*	`.hidden`			隐藏元素
*	`.fl_l`			左浮动
*	`.fl_r`			右浮动
*	`.fl_n`			不浮动
*	`.mar0~.mar_30`	边距上、下、左、右最大30px，已5px为基数递增
*	`.po_ab`			绝对定位
*	`.po_re`			相对定位
*	`.col1~9`			1~9等分列
*	`.arrow_b()`		下箭头
*	`.arrow_t()`		上箭头
*	`.arrow_r()`		右箭头
*	`.arrow_l()`		左箭头
*	`.fixed-top`		固定顶部
*	`.fixed-bottom`	固定底部
*	`.fixed-left`		固定左边
*	`.fixed-right`	固定右边

带'()'的是less使用的类，不会输出在css文件里面。


## shortcut.less

less调用的简写

*	`.display-b()`	block
*	`.display-i()`	inline
*	`.display-ib()`	inline-block
*	`.font-fm()`		微软雅黑
*	`.font-fs()`		宋体
*	`.font-fa()`		Arial
*	`.font-w700()`	字体粗700
*	`.font-w400()`	字体粗400
*	`.font-s()`		字体大小，默认12px
*	`.font-s1~100()`	字体大小1~100px
*	`.list-sn()`		列表去掉列表项样式
*	`.text-n()`		去掉下划线等
*	`.text-c()`		文字居中
*	`.text-l()`		文字左对齐
*	`.text-r()`		文字右对齐

## stars.less

`stars.less` 是星级评定的组件样式，基本都是输出css。

	<span class="stars a5 s5"><span class="star_selected"></span></span>
	
*	`.stars` 是基础类，有16x16px的宽和高设有星星的背景图片
*	`.a5` 是星星总数5颗星，取值范围是 a3 | a5 | a8 | a10，星星数量依次类推。
*	`.s5` 是星星选中5颗星，默认是选中1颗星，取值范围是 s0 ~ s9 其中以每0.5递增 s0d5 为类名，sall是选中全部。理论上选中的数量不能超过星星总数。
*	`.star_selected` 是显示选中星星的区域。

[效果演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/full/euolw/)
[代码演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/pen/euolw/)


## brand-color.less

主要是各大品牌的颜色变量

	@KK-BLUE:					#2f549f; //blue
	@BC-FONTAS: 				#1E9F75; //green
	@BC-ABOUTMEBLUE:			#00405d; //blue
	@BC-ABOUTMEYELLOW:			#ffcc33; //yellow
	@BC-ADOBE:					#ff0000; //red
	@BC-AIM:					#fcd20b; //yellow
	@BC-AMAZON:					#e47911; //orange
	@BC-ANDROID:				#a4c639; //green
	@BC-ANGIESLIST:				#7fbb00; //green
	@BC-AOL:					#0060a3; //blue
	@BC-ATLASSIAN:				#003366; //blue
	@BC-BEHANCE:				#053eff; //blue
	@BC-BIGCARTEL:				#97b538; //green
	@BC-BLOGGER:				#fc4f08; //orange
	@BC-CARBONMADE:				#613854; //purple
	@BC-DELICIOUS:				#205cc0; //blue
	@BC-DESIGNMOO:				#e54a4f; //pink
	@BC-DEVIANTART:				#4e6252; //dark
	@BC-DISQUSBLUE:				#59a3fc; //blue
	@BC-DISQUSORANGE:			#db7132; //orange
	@BC-DRIBBBLE:				#ea4c89; //pink
	@BC-DROPBOX:				#3d9ae8; //blue
	@BC-DRUPAL:					#0c76ab; //blue
	@BC-EBAY:					#89c507; //green
	@BC-EMBER:					#f05e1b; //orange
	@BC-ENGADGET:				#00bdf6; //blue
	@BC-ENVATO:					#528036; //green
	@BC-ETSY:					#eb6d20; //orange
	@BC-EVERNOTE:				#5ba525; //green
	@BC-FABCOM:					#dd0017; //red
	@BC-FACEBOOK:				#3b5998; //blue
	@BC-FLICKRBLUE:				#0063dc; //blue
	@BC-FLICKRPINK:				#ff0084; //pink
	@BC-FORRST:					#5b9a68; //green
	@BC-FOURSQUARE:				#25a0ca; //blue
	@BC-GARMIN:					#007cc3; //blue
	@BC-GETGLUE:				#2d75a2; //blue
	@BC-GIMMEBAR:				#f70078; //pink
	@BC-GITHUB:					#4183c4; //blue
	@BC-GOOGLE:					#db4a39; //pink
	@BC-GROOVESHARK:			#f77f00; //orange
	@BC-HOOTSUITE:				#003366; //blue
	@BC-HEROKULIGHT:			#c7c5e6; //purple
	@BC-HEROKUDARK:				#6567a5; //purple
	@BC-HTML5:					#ec6231; //orange
	@BC-IMDB:					#f3ce13; //yellow
	@BC-INSTAGRAM:				#634d40; //dark
	@BC-INTEL:					#0071c5; //blue
	@BC-INTUIT:					#365ebf; //blue
	@BC-KICKSTARTER:			#87c442; //green
	@BC-KIPPT:					#e03500; //red
	@BC-LASTFM:					#c3000d; //red
	@BC-LINKEDIN:				#0e76a8; //blue
	@BC-MEETUP:					#e51937; //red
	@BC-NOKIA:					#183693; //blue
	@BC-NVIDIA:					#76b900; //green
	@BC-PATH:					#e41f11; //red
	@BC-PAYPALDARK:				#1e477a; //blue
	@BC-PAYPALLIGHT:			#3b7bbf; //blue
	@BC-PINBOARD:				#0000e6; //blue
	@BC-PINTEREST:				#910101; //red
	@BC-PLAYSTATION:			#665cbe; //purple
	@BC-POCKET:					#ee4056; //red
	@BC-QUORA:					#a82400; //red
	@BC-QUOTEFM:				#66ceff; //blue
	@BC-RDIO:					#008fd5; //blue
	@BC-READABILITY:			#9c0000; //purple
	@BC-RSS:					#ee802f; //orange
	@BC-SAMSUNG:				#0c4da2; //blue
	@BC-SKYPE:					#00aff0; //blue
	@BC-SNAGAJOB:				#f47a20; //orange
	@BC-SOFTONIC:				#008ace; //blue
	@BC-SOUNDCLOUD:				#ff7700; //orange
	@BC-SPOTIFY:				#64b41a; //green
	@BC-SPRINT:					#fee100; //yellow
	@BC-SQUARESPACE:			#121212; //black
	@BC-STAPLES:				#cc0000; //red
	@BC-STRIPE:					#008cdd; //blue
	@BC-STUMBLEUPON:			#f74425; //orange
	@BC-T-MOBILE:				#ea0a8e; //pink
	@BC-TECHNORATI:				#40a800; //green
	@BC-THENEXTWEB:				#ef4423; //red
	@BC-TRULIA:					#5eab1f; //green
	@BC-TUMBLR:					#34526f; //blue
	@BC-TWITCHTV:				#6441a5; //purple
	@BC-TWITTER:				#00a0d1; //blue
	@BC-TYPO3:					#ff8700; //orange
	@BC-UBUNTU:					#dd4814; //orange
	@BC-USTREAM:				#3388ff; //blue
	@BC-VERIZON:				#ef1d1d; //red
	@BC-VIMEO:					#86c9ef; //blue
	@BC-VIRB:					#06afd8; //blue
	@BC-VIRGINMEDIA:			#cc0000; //red
	@BC-WOOGA:					#5b009c; //purple
	@BC-WORDPRESSBLUE:			#21759b; //blue
	@BC-WORDPRESSORANGE:		#d54e21; //pink
	@BC-WORDPRESSGREY:			#464646; //black
	@BC-XBOX:					#9bc848; //green
	@BC-YAHOO:					#720e9e; //purple
	@BC-YANDEX:					#ffcc00; //orange
	@BC-YELP:					#c41200; //red
	@BC-YOUTUBE:				#c4302b; //red
	@BC-ZERPLY:					#9dcc7a; //green
	@BC-ZOOTOOL:				#5e8b1d; //green
	@BC-TAOBAO:					#f40; //orange



## album.less

`album.less` 是一个相册类型的列表展示样式，每个项可以展示最多4张图

下面是html代码的例子

	<div class="albums ab_col5 clearfix">
        <dl class="album_item">
          <dd class="ab_fream">
            <ul>
              <li><img src="http://photo.yupoo.com/wmq719/C5TAowHQ/small.jpg" alt="yupoo"></li>
              <li><img src="http://photo.yupoo.com/wmq719/C5TAkRbY/small.jpg" alt="yupoo"></li>
            </ul>
          </dd>
          <dt class="ab_title">Walking Peking</dt>
          <dd class="ab_info ws_break">
            <span class="ab_time" title="最后更新时间:2004-10-15 12:15:10"><time>2004-10-15 12:15:10</time></span>
            <em class="ab_count" title="相片数量:10张">10P</em>
            <p class="ab_des">我是头戴皇冠身披紫色战袍的小王子住在大观园的牡丹王国里与那些蜂啊蝶啊相比我实在不算勇敢不能劈荆斩棘不能所向无敌但是在你的面前我就能变身成超人一切无所畏惧</p>
          </dd>
        </dl>
	</div>

*	`.albums` 基础类
*	`.ab_col5` 列表项目以5个为一列展示，取值范围是 `ab_col2 | ab_col3 | ab_col4 | ab_col5`
*	`.album_item` 列表项目
*	`.ab_fream` 图片显示区域的框架
*	`.ab_title` 列表项的标题
*	`.ab_info` 列表项的信息栏
*	`.ab_time` 时间戳
*	`.ab_count` 图片总数
*	`.ab_des` 项目描述

[效果演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/full/sfAiH/) 
[代码演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/pen/sfAiH)



## icon.less

`icon.less` 是早期的图片背景图标，有三个尺寸16px、32px和64px；

下面是同一个图标三种大小的例子

	<span class="icon16 four-case"></span>
	<span class="icon32 four-case"></span>
	<span class="icon48 four-case"></span>

[图标来源 <i class="fa fa-external-link-square"></i>](http://www.gentleface.com/free_toolbar_icon_set_ch.html "图标来源")
[站酷资源 <i class="fa fa-external-link-square"></i>](http://www.zcool.com.cn/gfx/ZMTA0NTky.html "站酷资源")

[效果演示 <i class="fa fa-external-link-square"></i>](http://jsfiddle.net/iqszlong/nmo97xqr/embedded/result/)
[代码演示 <i class="fa fa-external-link-square"></i>](http://jsfiddle.net/iqszlong/nmo97xqr/)



## list.less

`list.less` 是dl做成的列表。效果基本和tabel一致，宽度多百分比。适用小于10列数据

html代码例子

	
    <div class="list">
        <dl>
          <dt>悬赏任务</dt>
          <dd class="tags">
            <ul>
                <li>悬赏金额</li>
                <li class="w5">任务名称</li>
                <li>浏览|投稿</li>
                <li>任务类型</li>
                <li>结束时间</li>
                <li>任务状态</li>
            </ul>
          </dd>
          <dd class="clearfix">
            <ul>
                <li>￥101.00</li>
                <li class="w5"><a href="#" title="微博任务发布测试">微博任务发布测试...</a></li>
                <li>4|1</li>
                <li>微博任务</li>
                <li>2天7小时</li>
                <li>已结束</li>
            </ul>
          </dd>
        </dl>
    </div>
			            



[效果演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/full/synLD)
[代码演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/pen/synLD)



## nav.less

`nav.less` 导航样式，有两种导航样式top-nav和primary_nav。

	<nav class="top-nav">
        <div  class="container">
                <ul class="menu">
                      <li><a href="home.htm"><i class="fa fa-home"></i> <span>首页</span></a></li>
                      <li class="line"></li>
                      <li><a href="user_index.htm"><span>用户中心</span></a></li>
                      <li class="line"></li>
                      <li><a href="task_list.htm"><span>列表页</span></a></li>
                      <li class="line"></li>
                      <li><a href="task_detail.htm"><span>任务详细页</span></a></li>
                      <li class="line"></li>
                      <li><a href="shop_detail.htm"><span>商品详细页</span></a></li>
                      <li class="line"></li>
                      <li><a href="case.htm"><span>成功案例</span></a></li>
                      <li class="line"></li>
                      <li><a href="im.htm"><i class="fa fa-comments"></i> <span>IM</span></a></li>
                </ul>
        </div>
	</nav>


	<nav class="primary_nav clearfix">
	  <ul>
	    <li><a href="#"><i class="fa fa-tachometer icon32"></i><em>管理面板</em></a></li>
	    <li><a class="selected" href="#"><i class="fa fa-cog icon32"></i> <em>个人设置</em></a></li>
	    <li><a href="#"><i class="fa fa-line-chart icon32"></i><em>财务管理</em></a></li>
	    <li><a href="#"><i class="fa fa-shopping-cart icon32"></i><em>雇主|买家</em></a></li>
	    <li><a href="#"><i class="fa fa-suitcase icon32"></i><em>威客|卖家</em></a></li>
	    <li><a href="#"><i class="fa fa-shield icon32"></i><em>安全设置</em></a></li>
	    <li><a href="#"><i class="fa fa-envelope icon32"></i><em>信息中心</em><strong class="badge">12</strong></a></li>
	    <li><a href="#"><i class="fa fa-heart icon32"></i><em>我的收藏</em></a></li>
	  </ul>
	</nav>


[效果演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/full/alxBd/)
[代码演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/pen/alxBd)


## tab.less

选项卡效果

	<div class="tab">
	  <a href="###" id="tab_tab_1" class="selected">选项卡1<b class="arrow arrow_b"></b></a>
	  <a href="###" id="tab_tab_2">选项卡2<b class="arrow arrow_b"></b></a>
	</div>

	<div class="tab_detail">
	      <div id="div_tab_1" class="tabdetail">选项卡1内容</div>
	      <div id="div_tab_2" class="tabdetail hidden">选项卡2内容</div>
	</div>

[效果演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/full/qtdCj)
[代码演示 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/pen/qtdCj)



## wallpaper.less

把图片转换成字符存为变量，转换网站 [查看  <i class="fa fa-external-link-square"></i>](http://www.base64-image.de/)

目前这个文件只是暂存，实际开发中可以程序自动生成字符文字。

[查看例子 <i class="fa fa-external-link-square"></i>](http://codepen.io/iqszlong/pen/djzBm)
	
