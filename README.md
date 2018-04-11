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
