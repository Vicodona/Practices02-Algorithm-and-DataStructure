### 1.2 Python 插入排序算法
#### 1.2.1 概述
插入排序是一种简单的排序算法，其工作方式跟扑克牌排序类似。

#### 1.2.2 算法描述
```text
    //对 n 大小的数组进行排序
    insertionSort(arr,n)
    Loop from i= 1 to n-1
    选择元素 arr[i] 并将其插入到排序序列 arr[0...i-1] 中
```

#### 1.2.3 语言描述
```text
直接插入排序的核心思想就是：将数组中的所有元素依次跟前面已经排好的元素相比较，如果选择的元素比已排序的元素小，则交换，直到全部元素都比较过。
因此，从上面的描述中我们可以发现，直接插入排序可以用两个循环完成：

    第一层循环：遍历待比较的所有数组元素
    第二层循环：将本轮选择的元素(selected)与已经排好序的元素(ordered)相比较。
    如果：selected > ordered，那么将二者交换
```
#### 1.2.4 Example
    
##### 插入排序图示
![insertion_sort1](../images/insertionsort.png)

##### 动态图描述
![insertion_sort2](../images/Insertion-sort-example.gif)
##### 语言描述

有一未排序的数组：（12 11 13 5 6)，从 i = 1 (数组第二个数) 循环到 i = 5。

1. 当 i = 1 时，因为 11 比 12 小，往后移动 12 并在 12 之前插入 11

（**11** **12** 13 5 6）

2. 当 i = 2 时，13 比所有 [0,i-1] 的元素都要大，所以 13 保持不移动

（**11** **12** **13** 5 6）

3. 当 i = 3 时，5 比 [0,i-1] 的元素都要小，故将 5 移至数组开头，原 [0,i-1] 的元素都将移动到 [1,i] 的对应位置

（**5** **11** **12** **13** 6）

4. 当 i = 4 时，6 被插入到 5 之后，11、12、13 向后移动一个位置
（**5** **6** **11** **12** **13**）

#### 1.2.4 插入算法的递归实现

##### 递归实现
保持已处理元素的顺序，并将新元素插入插入排序序列

##### 递归思想
    1.基本情况：数组大小为 1 或更小，返回
    2.递归排序 n-1 个元素
    3.在已排好序的数组中在其对应位置插入最后一个元素

#### 1.2.5 算法实现

python 实现

```python
#!/usr/bin/env python
# Python 实现插入排序

# 直接插入排序
"""
时间复杂度：O(n**2)
空间复杂度：O（1）
稳定性：稳定
思想：先将前两个元素排序，将第三个元素插入前面已经排好序的序列，后面的元素依次插入前面已经排好的序列。

"""


def basic_insertion(arr):
    n = len(arr)
    if n <= 1:
        return
    for i in range(1, len(arr)):
        # key（本轮所选择的元素） 指向尚未排序好的元素(从第二个开始)
        key = arr[i]
        # j 指向下一个元素下标
        j = i-1
        # key 与前一个元素比较，若 key 较小，则前一个元素后移，j自减，继续比较
        while j >= 0 and key < arr[j]:
            arr[j+1] = arr[j]
            j -=1
        # key 指向元素的最终位置
        arr[j+1] = key
    return arr


# 递归插入排序
def recursive_insertion(arr, n):
    # base case
    if n <=1:
        return
    # 对 n-1 个元素进行递归排序
    recursive_insertion(arr, n-1)
    # 将最后一个元素插入到已排序序列对应位置
    last = arr[n-1]
    j = n-2
    # 移动比 key大的 arr[0...i-1] 中的元素到后一个位置
    while j >= 0 and arr[j] > last:
        arr[j+1] = arr[j]
        j = j-1
    arr[j+1] = last
    return arr

```

c++ 实现

```c++
void insertionSort(T arr[], int n){
    for(int i=1; i<n ; i++){
	    for(int j=i; j>0; j--){
		    if(arr[j] < arr[j-1]){
			    swap(arr[j], arr[j-1]);
			}
		}
	}
}
```

【推荐视频】[Recursive Insertion Sort | GeeksforGeeks](https://www.youtube.com/watch?v=wObxd4Kx8sE)