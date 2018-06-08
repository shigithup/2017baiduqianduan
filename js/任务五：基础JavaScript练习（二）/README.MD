# 由js taskfive引起的

# 1.盒子的摆放

默认

![mark](http://myphoto.shigaozhen.cn/myselfhexo/20180604/192653531.png)

* 方法一：把`li`设置`vertical-align：bottom`
* 方法二：在父元素`ul`设置`display: flex;  align-items: flex-end; `

![mark](http://myphoto.shigaozhen.cn/myselfhexo/20180604/192704730.png)

# 2.已知类数组，如何获得真数组

* 1. 第一种方法，创建一个新数组来，通过for循环来获得数组项

     ```js
     var liItems=document.getElementsByTagName('li');
     var newArr =[];
     for (var i = 0; i < liItems.length; i++) {
          newArr.push(liItems[i].innerHTML);
          }
     ```

* 2. 第二种方法通过直接对li的NodeList进行转化来获得数组。

     ```js
     var allli= numul.getElementsByTagName('li');
     var allli_arr=Array.prototype.slice.call(allli,0);
     ```

     更多请阅读原代码文件

# 3.将数组排序

## 通过`sort()`

```js
newArr.sort( function (value1, value2) {
	      return value1 - value2;
	    	});
```



## 冒泡排序

冒泡排序对一个需要进行排序的数组进行以下操作:

1. 比较第一项和第二项;
2. 如果第一项应该排在第二项之后, 那么两者交换顺序;
3. 比较第二项和第三项;
4. 如果第二项应该排在第三项之后, 那么两者交换顺序;
5. 以此类推直到完成排序;

```js
function bubbleSort() {
	    	    for (var i = 0; i < newArr.length; i++) {
	    	        for (var j = 0; j < newArr.length - 1 - i; j++) {
	    	            if (newArr[j] > newArr[j+1]) {        //相邻元素两两对比
	    	                var temp = newArr[j+1];        //元素交换
	    	                newArr[j+1] = newArr[j];
	    	                newArr[j] = temp;
	    	            }
	    	        }
	    	    }
	    	    return newArr;
	    	};
```

外层的循环决定需要进行多少次遍历, 内层的循环负责数组内各项的比较, 还通过外层循环的次数和数组长度决定何时停止比较.

冒泡排序极其低效, 因为处理数据的步骤太多, 对于数组中的每`n`项, 都需要`n^2`次操作来实现该算法(实际比n^2略小, 但可以忽略, 具体原因见⤵️), 即时间复杂度为`O(n^2)`.

> 对于含有n个元素的数组, 需要进行`(n-1)+(n-2)+...+1`次操作, 而`(n-1)+(n-2)+...+1 = n(n-1)/2 = n^2/2 - n/2`, 如果n趋于无限大, 那么n/2的大小对于整个算式的结果影响可以忽略, 因此最终的时间复杂度用`O(n^2)`表示

## 选择排序

选择排序对一个需要进行排序的数组进行以下操作:

1. 假定数组中的第一项为最小值(min);
2. 比较第一项和第二项的值;
3. 若第二项比第一项小, 则假定第二项为最小值;
4. 以此类推直到排序完成.

```js
function selectionSort(arr) {
    var len = arr.length;
    var minIndex, temp;
    for (var i = 0; i < len - 1; i++) {
        minIndex = i;
        for (var j = i + 1; j < len; j++) {
            if (arr[j] < arr[minIndex]) {     //寻找最小的数
                minIndex = j;                 //将最小数的索引保存
            }
        }
        temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
    return arr;
}
```

外层循环决定每次遍历的初始位置, 从数组的第一项开始直到最后一项. 内层循环决定哪一项元素被比较.

选择排序的时间复杂度为`O(n^2) `. 



## 插入排序

与上述两种排序算法不同, 插入排序是稳定排序算法(stable sort algorithm), 稳定排序算法指不改变列表中相同元素的位置, 冒泡排序和选择排序不是稳定排序算法, 因为排序过程中有可能会改变相同元素位置. 对简单的值(数字或字符串)排序时, 相同元素位置改变与否影响不是很大. 而当列表中的元素是对象, 根据对象的某个属性对列表进行排序时, 使用稳定排序算法就很有必要了.

一旦算法包含交换(swap)这个步骤, 就不可能是稳定的排序算法. 列表内元素不断交换, 无法保证先前的元素排列为止一直保持原样. 而插入排序的实现过程不包含交换, 而是提取某个元素将其插入数组中正确位置.

**实例说明:**

现在需要将数组`var items = [5, 2, 6, 1, 3, 9];`进行插入排序:

1. 5属于已完成部分, 余下元素为未完成部分. 接下来提取出2, 因为5比2大, 于是5被移至靠右一个位置, 覆盖2, 占用2原本存在的位置. 这样本来存放5的位置(已完成部分的首个位置)就被空出, 而2在比5小, 因此将2置于这个位置, 此时结果为[2, 5, 6, 1, 3, 9];
2. 接下来提取出6, 因为6比5大, 所以不操作提取出1, 1与已完成部分各个元素(2, 5, 6)进行比较, 应该在2之前, 因此2, 5, 6各向右移一位, 1置于已完成部分首位, 此时结果为[1, 2, 5, 6, 3, 9];
3. 对余下未完成元素进行类似操作, 最后得出结果[1, 2, 3, 5, 6, 9];

代码实现:

```js
function insertionSort(items) {
  let len = items.length, value, i, j;
  for (i = 0; i < len; i++) {
    value = items[i];
    for (j = i-1; j > -1 && items[j] > value; j--) {
      items[j+1] = items[j];
    }
    items[j+1] = value;
  }
  return items;
};
```


外层循环的遍历顺序是从数组的第一位到最后一位, 内层循环的遍历则是从后往前, 内层循环同时负责元素的移位.

插入排序的时间复杂度为O(n^2)

以上三种排序算法都十分低效, 因此实际应用中不要使用这三种算法, 遇到需要排序的问题, 应该首先使用JavaScript内置的方法Array.prototype.sort();

参考：

[三种基础的排序算法](http://ife.baidu.com/2017/note/detail/id/762)

[[JS的十大经典算法排序](https://www.cnblogs.com/dushao/p/6004883.html)](http://ife.baidu.com/2017/note/detail/id/762)

[算法小白——基本排序算法入门](http://ife.baidu.com/2017/note/detail/id/1079)

