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
