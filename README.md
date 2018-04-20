### 任务四知识点总结
#### 水平垂直居中
#####  方法一：
	.box {
		width: 400px;
		height: 200px;
		background-color: #ccc;
		margin: auto;
		position: absolute;
		left:0;
		top:0;
		bottom:0;
		right:0;
	} 
##### 方法二：引入transform
	.box {
		width: 400px;
		height: 200px;
		background-color: #ccc;
		margin: auto;
		position: absolute;      /* 这里要明白绝对定位的50%相对父元素，下面translate50%是盒子box的50% */
		left:50%;
		top:50%;
		transform: translate(-200px, -100px )    /* 宽高的1/2，另外可用transform: translate(-50%, -50%)替换，效果是一样的*/
##### 方法三：与方法二相比用margin取代transform
	.box {
		width: 400px;
		height: 200px;
		background-color: #ccc;
		position: absolute;
		left:50%;
		top:50%;
		margin-left:-200px;     /*这里的-200px不能用-50%所替代*/
		margin-top:-100px;
	}

#####  方法四：弹性布局Flex
	以下放在所要居中的div父元素中，父元素必须有高度
	divpare  {
		height: 800px;
		display: flex;
		justify-content: center;
    	align-items: center;
	}
#### 水平居中
参照水平垂直居中：

	margin：0 auto；
	left:50%; margin-left:-width/2;或者 transform: translateX(-width·/2)


### 任务三

**左右两栏宽度固定，中间主体宽高自适应**

### 通过`margin`1
	#center{
			width:100%;
	}
	#center #c-inner { 
			margin: 0 210px;
			float: left;
		}
	#left{
			width: 200px;
			background-color: orange;
			margin-left: -100%;
			float: left;
		}
	#right{
			width: 200px;
			background-color: purple;
			margin-left: -200px; 
			float: left;
		}

**注意：**

- 盒子的顺序center-left-right
- center的width：100%不可少，否则当文字较少时，便无法撑起盒子#c-inner的横排空间。


###  通过margin2

	#left{
			width: 200px;
			background-color: orange;
			float: left;
		}
	#center{
			width:100%;
			float: left;
			margin:0 -210px 0 -210px;
	}
	#center #c-inner { 
			margin: 0 210px;
		}
	
	#right{
			width: 200px;
			background-color: purple;
			float: left;
		}

**注意：** 

- 盒子顺序：left-center-right

-  盒子默认继承父元素的宽（是整个盒子模型等于父元素的宽，即当padding，margin增加时会挤压内容区），，若指明继承为width：100%。则，盒子的内容区为父元素的宽，也就是说，内容区的宽固定了，在增加padding，只会增大盒子模型而内容区不变，此时，padding的增加是从左向右即padding会造成盒子增大，内容区移动。

### 通过绝对定位

	
	#left{
			width: 200px;
			position: absolute;
			top: 0;
			left: 0;
		}
    #c-inner { 
			margin: 0 210px;
		}
	#right{
			width: 200px;
			position: absolute;
			top: 0;
			right: 0;
		}


**注意：**

父元素高度取决于中间部分的高度，当两侧高度大于中间高度时，则出现高度塌陷，除非指定父元素的高度，当两侧高度小于中间部分时，可以使用。（且塌陷的父元素，无法利用清除浮动撑起来。因为这是定位，不是浮动，无法清除）


###  通过padding

在`margin1`的基础上，去掉#c-inner的margin，在三个盒子的父元素加padding，left和right通过相对定位，移动至padding空白处。
### flex布局

### 参考
[http://www.cnblogs.com/ljchow/archive/2010/07/27/1785632.html](http://www.cnblogs.com/ljchow/archive/2010/07/27/1785632.html)

[http://ife.baidu.com/note/detail/id/666](http://ife.baidu.com/note/detail/id/666)


### 任务七

在 HTML 4.01 中，`<a>` 标签可以是超链接或锚。在 HTML5 中，`<a>` 标签始终是超链接，但是如果未设置 href 属性，*则只是超链接的占位符,则不可以使用如下属性：download, hreflang, media, rel, target 以及 type 属性,此时color等无法设置属性值。*<!--more-->
	
	a:link 		/* 未访问的链接 */
    a:visited 	/* 已访问的链接 */
    a:hover 	/* 鼠标移动到链接上   可以用在表格上*/
	a:focus     /*获得焦点状态        可以用在输入框上*/
    a:active 	/* 选定的链接    激活发生在链接被点击时     可以用在提交按钮上*/

上面的次序很重要，否则有些样式会不起作用。次序为：lvhfa。简单记法：Lord Vader Hate Furry Animals。 

### 1. 突出显示不同类型的链接

#### 1.1如图给链接加个小图标
 
![mark](http://myphoto.shigaozhen.cn/myselfhexo/20180415/200156085.png) 

实现方法：

- 1.可用img直接vertical-align：top；
- 在超链接上通过background来实现。

同理，如果想实现在文字的下面加些特殊的下划线，也可通过background把图片定到文字下。

#### 1.2 给链接在`focus`状态下加个下标线

![mark](http://myphoto.shigaozhen.cn/myselfhexo/20180415/203048025.png)

通过
	
	a { text-decoration: none;}
	a:focus{     
		padding-bottom: 22px;
        border-bottom: 2px solid red
		}

**启示：**通过伪类状态的不同属性（link,visited,hover,focus,active）,可以在不同的属性下设置一些不同的样式，比如`focus`时文字背景颜色变为红色
### 2 图像翻转

不同伪类状态属性时文字的背景图片不同，可以营造一种错觉的的图像翻转，就是把文字的背景颜色变为背景图像。

#### 2.1pixy方法

由于这种方法在在第一次加载图像时会有点迟钝，因此我们可以将悬停的图像作为背景应用于父元素，从而预先加载他们。再进一步，可以把多个图像放在一个背景图像的不同位置，因此减少了服务器请求的数量。把所有图像放在同一个位置的方法叫做pixy方法。（pixy是发明者的昵称）

#### 2.2 css精灵
 
多个服务器请求会对站点的性能产生显著的影响，所以在pixy方法的启示下，可以把一个网站的所有图标和，图形等放在一个图像上。这就是**css精灵**。

然而在个人的实践下，这种方法并不好用，对各个图像的位置要求比较大，为此需要的花费好多时间进行调试。所以使用与否看需求了。

#### 2.3 文字图像同时翻转
在这里进行图像翻转的同时，文字是不变的。要想实现文字与背景都改变，需要用到`text-indent`与`position:absloute`，然而这两者会产生放一起会产生奇特的化学反应。即当 父元素的`text-indent`作用于文字时`position:absloute`里的文字会一起移动，`position:absloute`的原位仍在，但对其文字失去控制能力。如下：

	<div  id="hh">   <div id="ff">fdsklfj</div>    我是按钮链接  </div>
	#hh{width:500px; text-align: center;background-color: grey;}
	#ff{  width:100px; position: absolute; top: 0; left: 0; }

 

当对`#hh`添加`text-indent:100px`时,盒子ff的文字会一起移动;

![mark](http://myphoto.shigaozhen.cn/myselfhexo/20180420/100830032.png)

为解决这个问题我们可以使用覆盖的方式。如下两个同级元素，由于盒子hh完全被盒子ff的绝对定位覆盖即盒子ff层次在盒子hh之上，此时位于下面的盒子#hh:hover失效
	
	<div  id="hh"> 我是按钮链接  </div>
	<div id="ff">fdsklfj</div> 
	#hh{width:500px; text-align: center;background-color: grey;   }
	#hh:hover{ text-indent: 1000px;}
	#ff{ width: 500px;  position: absolute; top: 8px; left: 8px; }
	#ff:hover{text-align: center; color:yellow}
 

对#ff:hover添加`background-color:red`

![mark](http://myphoto.shigaozhen.cn/myselfhexo/20180420/112509355.png)


### 3 悬停下拉菜单

![mark](http://myphoto.shigaozhen.cn/myselfhexo/20180420/174030034.png)

 

	<ul id="one">
	 	<li><a href="">Home</a></li>
	 	<li>
	 	  <a href="">Products</a> 
	 	  <ul id="two">
	 		<li><a href="">Home</a></li>
	 		<li><a href="">Services</a></li>
	 		<li><a href="">Contact Us</a></li>
		  </ul>
	 	</li>
	 	<li><a href="">Services</a></li>
	 	<li><a href="">Contact Us</a></li>
	 </ul>



	#one li	{
    	list-style: none; 
    	float: left;  
    	border:1px solid #486b20;background-color: #8bd400; width: 85px;}
    #one li a{text-decoration: none;} 
    #two {position: absolute;   left: -1000px; padding: 0; }
    #one li:hover #two{ left: auto; }
    #two li{   float: none; width: 85px; }


下拉菜单的难点在于`#one li:hover #two{ left: auto; }`,通过父元素的状态来控制子元素。



### 4.锚

锚可以作为内部引用，也可以作为外部链接。

	<a href="#na">one</a>
	<a href=""  id="jump">two</a>
	......
	<a name="na">three</a>
	<a href="#jump">four</a>

点击one会跳到three，点击four会跳到two。 `name`属性在H5中不在支持。
详见 [http://shigaozhen.cn/note/2018/undefined15/59c34dbb.html#more](http://shigaozhen.cn/note/2018/undefined15/59c34dbb.html#more)
