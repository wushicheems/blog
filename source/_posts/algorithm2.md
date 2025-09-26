---
title: algorithm2
date: 2025-08-19 14:07:43
tags: teach-algorithm
excerpt: 算法第二课：快速排序
comments: true
categories: teach-algorithm
---
# 欢迎来到算法基础课程

## 第二课：快速排序

### 算法原理

1. **核心思想**：
   - **分治法**：选取**基准（pivot）**，将数组分为小于基准和大于基准的两部分
   - **递归**排序子数组
2. **基准选择策略**：
   - **左基准法**：始终选择最左元素
   - **中基准法**：选择中间元素
   - **右基准法**：始终选择最右元素

### C++实现

#### 中基准法

```cpp
#include <algorithm>
using namespace std;

int partition_mid(int arr[], int low, int high) {
    int mid = low + (high - low) / 2;
    int pivot = arr[mid];
    swap(arr[mid], arr[high]);
    int i = low;
    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            swap(arr[i], arr[j]);
            i++;
        }
    }
    swap(arr[i], arr[high]);
    return i;
}

void quickSort_mid(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition_mid(arr, low, high);
        quickSort_mid(arr, low, pi - 1);
        quickSort_mid(arr, pi + 1, high);
    }
}
```

#### 左基准法

```cpp
#include <algorithm>
using namespace std;

int partition_left(int arr[], int low, int high) {
    int pivot = arr[low];
    int i = low + 1, j = high;
    while (i <= j) {
        while (i <= j && arr[i] <= pivot) i++;
        while (i <= j && arr[j] >= pivot) j--;
        if (i >= j) break;
        swap(arr[i], arr[j]);
    }
    swap(arr[low], arr[j]);
    return j;
}

void quickSort_left(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition_left(arr, low, high);
        quickSort_left(arr, low, pi - 1);
        quickSort_left(arr, pi + 1, high);
    }
}
```

#### 右基准法

```cpp
#include <algorithm>
using namespace std;

void quickSort_right(int arr[], int low, int high) {
    if (low < high) {
        int pivot = arr[high];
        int i = low;
        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                swap(arr[i], arr[j]);
                i++;
            }
        }
        swap(arr[i], arr[high]);
        
        quickSort_right(arr, low, i - 1);
        quickSort_right(arr, i + 1, high);
    }
}
```

#### 使用示例

```cpp
int main(){
	int text[]={4,6,8,7,2,3};
	quickSort(text,0,sizeof(text)/sizeof(int)-1); 
	//函数名和参数自己定,排序后数组为[2,3,4,6,7,8],可以自己输出一下
	return 0;
}
```

#### 算法性能

1. 时间复杂度:
   - [ ] 最好情况： `O(n log n)` （正常情况）
   - [ ] 最坏情况： `O(n^2)` （如已排序数组且选择左/右基准）
   - [ ] 平均情况： `O(n log n)`
   
2. 空间复杂度:
   - [ ] `O(log n)` (递归栈空间)
   
3. 各基准的特点:
   - 中基准:平衡性好,避免最坏情况,适合大多数数据分布
   - 左基准:实现简单,对升序数组性能较差`O(n²)`
   - 右基准:代码更简洁,对降序数组性能较差`O(n²)`

### 课程结束

1. 作业:
   - 实现各种基准的快速排序(中基准,左基准,右基准)
   - 用不同方法测试以下数组性能(测试用例在下):
   ```cpp
   //以下是测试用例
   int arr1[]={8,6,7,4,6,3};  //随机数组
   int arr2[]={1,3,4,5,7,8};  //升序数组 
   int arr3[]={9,6,5,3,2,1};  //降序数组
   ```
	  
**谢谢大家的观看**
有问题可联系**手机-微信:18372735812**