title: 几种排序算法总结
date: 2014-10-20 13:50:15
categories: Coding
tags: [Algorithm,Java] 
---

常用的几种排序算法应该是编程最基础的技能了，虽然曾经写过N次，但是每隔一段时间重新再写一次，经常还是不能一次完全写对，因此有必要系统的整理一下，对比总结一下各自的特点，便于理解记忆。
<!-- more -->
<br>
## 选择排序

### 简单选择排序
选择排序的算法思想很简单，先找出最小的数放在左侧第一位，再从剩下n-1个数中找到最小的数放在左侧第二位，以此类推；该排序法不稳定(例如序列5 8 5 2 9，第一次选择后第一个5会被交换到第二个5之后)；时间复杂度O(n^2) 。
<br>
### Java示例代码
```
	static void selectSort(int a[]){
		int i,j,minIndex,temp;  
		for(i=0;i<a.length;i++){
		    minIndex = i;
			for(j=i+1;j<a.length;j++){
				if(a[j]<a[minIndex]){
					minIndex = j;
				}
			}
			temp = a[i];
			a[i] = a[minIndex];
			a[minIndex] = temp;
		}
	}
```

## 插入排序

### 直接插入排序法
将待排序的记录逐个插入到已经排好序的序列的适当位置，直到全部插入完为止。一般认为第一个值已排好序，从第二个值开始向其中插入；时间复杂度O(n^2)；空间复杂度O(1)，因为只使用了一个temp临时变量的辅助空间。
<br>
### Java示例代码
```
	static void insertSort(int a[]){
		int i,j,temp;
		for(i=1;i<a.length;i++){
			j=i-1;
			temp = a[i];  //这里必须用一个临时变量存储arr[i],因为后面的while会改变其值
			while(j>=0&&a[j]>temp){
				a[j+1] = a[j];
				j--;
			}
			a[j+1] = temp;
		}
	}
```
## 交换排序

### 冒泡排序
冒泡排序属于最基础也是接触最早的排序算法这里就不多介绍了，其时间复杂度O(n^2)；空间复杂度O(1)。
<br>
### Java示例代码
```
	static void maopaoSort(int a[]){
		int i,j,temp;
		for(i=0;i<a.length-1;i++){    //最后一个数不用比，比到倒数第二个数即可，所以是a.length-1
			for(j=0;j<a.length-i-1;j++){   //第一个数比较n-1次，因为是n个数，两两作比较
				if(a[j]>a[j+1]){
					temp = a[j];
					a[j] = a[j+1];
					a[j+1] = temp;
				}
			}
		}
	}
```
<br>
### 快速排序
快速排序可以说是面试笔试最喜欢考的题目，较之其他排序算法也是略微复杂了点，因此需要重点掌握。
排序算法不稳定，是冒泡排序的一种改进，由于从两端向中间比较，且每次移动的距离较远，因此可以减少移动次数，所以比较快；
原理：先对某个元素（一般选第一个元素）和所有数据比较，小于该元素的数值放其左侧，大于的放其右侧，然后对左右两侧分别重复该过程；
时间复杂度为O(n*log2(n)),由于使用递归方法，因此需要一个O(log2(n))的栈空间。
<br>
### Java示例代码
```
	static void quickSort(int a[],int low,int high){  //这里其实low = 0；high = r.length-1;但是后面要用递归，需要指定不同的边界
		int i,j,temp;   //temp用于保存基准元素
		if(low<high){   //这里确保待比较的元素个数大于1
			i = low;
			j = high;
			temp = a[i];  //令第一次数据为基准
			while(i<j){
				while(i<j&&a[j]>=temp) j--; //从数组的右端向左依次和基准比较，直到遇到小于基准的数或者比较完依然没遇到。
				              //注意，相等的时候也要换过去，这也造成快排不具有稳定性
				if(i<j){    //如果在没比较完之前遇到，则：
					a[i] = a[j]; i++;  //右侧较小的数挪到数组左侧去，注意这里不用交换，因为基准数已经保存在变量temp里了
				}
				while(i<j&&a[i]<=temp) i++; //然后又从左侧向右开始和基准比较
				if(i<j){
					a[j] = a[i]; j--;   //直到遇到大于基准的数，将其挪到数组右侧去
				}
			}
			a[i] = temp; //直到i和j相遇时第一圈比完，这个位置就应该是基准在数组排序中的位置，且此时i=j
			if(low<i-1) quickSort(a,low,i-1); //最后对基准左侧和右侧的数据不断重复上述过程
			if(high>j+1) quickSort(a,j+1,high); //注意if里的判断条件,因为此时r[i] or r[j]已经不需要再比较
		}

	}
```

## 总结
除了选择排序多一个最小下标的辅助参量minIndex，其他排序都是用到i, j, temp这三个辅助量；很容易理解选择排序和冒泡排序都是两重循环，而插入排序则使用while为待插入元素腾位置，快速排序则要用递归；其中选择排序和快速排序不稳定，而冒泡和插入则是稳定排序。

先写这么多，后面用到再补充！

<br><br>
