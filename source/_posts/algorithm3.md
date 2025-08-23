---
title: algorithm3
date: 2025-08-23 18:59:28
tags: teach-algorithm
excerpt: 算法第三课：归并排序
comments: true
categories: teach-algorithm
---
# 欢迎来到算法基础课程

## 第三课：归并排序

### 算法原理

- **核心思想**：
  - **分治法**：将数组递归地分成两半，直到每个子数组只有一个元素
  - **合并**：将两个已排序的子数组合并成一个有序数组

- **算法步骤**：
  - 分割：将数组从中间分成左右两个子数组
  - 递归：对左右子数组分别进行归并排序
  - 合并：将两个有序子数组合并成一个有序数组

### C++实现

#### 递归版本

```cpp
#include <vector>
using namespace std;

void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    
    vector<int> L(n1), R(n2);
    
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    
    int i = 0, j = 0, k = left;
    
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        
        merge(arr, left, mid, right);
    }
}
```

#### 迭代版本（非递归）

```cpp
#include <vector>
#include <algorithm>
using namespace std;

void mergeSortIterative(int arr[], int n) {
    for (int curr_size = 1; curr_size <= n-1; curr_size = 2*curr_size) {
        for (int left_start = 0; left_start < n-1; left_start += 2*curr_size) {
            int mid = min(left_start + curr_size - 1, n-1);
            int right_end = min(left_start + 2*curr_size - 1, n-1);
            
            int n1 = mid - left_start + 1;
            int n2 = right_end - mid;
            
            vector<int> L(n1), R(n2);
            
            for (int i = 0; i < n1; i++)
                L[i] = arr[left_start + i];
            for (int j = 0; j < n2; j++)
                R[j] = arr[mid + 1 + j];
            
            int i = 0, j = 0, k = left_start;
            
            while (i < n1 && j < n2) {
                if (L[i] <= R[j]) {
                    arr[k] = L[i];
                    i++;
                } else {
                    arr[k] = R[j];
                    j++;
                }
                k++;
            }
            
            while (i < n1) {
                arr[k] = L[i];
                i++;
                k++;
            }
            
            while (j < n2) {
                arr[k] = R[j];
                j++;
                k++;
            }
        }
    }
}
```

#### 使用示例

```cpp
int main() {
    int text[] = {4, 6, 8, 7, 2, 3};
    int n = sizeof(text) / sizeof(int);
    
    mergeSort(text, 0, n - 1);
    // 或者使用迭代版本: mergeSortIterative(text, n);
    
    // 排序后数组为 [2, 3, 4, 6, 7, 8]
    return 0;
}
```

### 算法性能

- 时间复杂度:
  - 最好情况： `O(n log n)`
  - 最坏情况： `O(n log n)`
  - 平均情况： `O(n log n)`
  - 归并排序的时间复杂度稳定，不受输入数据的影响

- 空间复杂度:
  - `O(n)` (需要额外的临时数组空间)

- 算法特点:
  - 稳定排序算法（相等元素的相对位置不变）
  - 适合链表排序（不需要随机访问）
  - 适合外部排序（大数据量无法全部装入内存的情况）
  - 需要额外的存储空间

### 与快速排序对比

| 特性 | 归并排序 | 快速排序 |
|------|----------|----------|
| 时间复杂度 | 稳定 O(n log n) | 平均 O(n log n)，最坏 O(n²) |
| 空间复杂度 | O(n) | O(log n) |
| 稳定性 | 稳定 | 不稳定 |
| 适用场景 | 链表、外部排序 | 数组、内存排序 |

### 课程结束

- 作业:
  - 实现递归和迭代两种版本的归并排序
  - 测试以下数组的性能:
  ```cpp
  // 测试用例
  int arr1[] = {8, 6, 7, 4, 6, 3};  // 随机数组
  int arr2[] = {1, 3, 4, 5, 7, 8};  // 升序数组 
  int arr3[] = {9, 6, 5, 3, 2, 1};  // 降序数组
  ```
  - 比较归并排序和快速排序在不同数据分布下的性能差异

**谢谢大家的观看**
有问题可联系**手机-微信:18372735812**