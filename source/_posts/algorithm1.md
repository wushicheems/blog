---
title: algorithm1
date: 2025-08-14 18:03:59
tags: teach-algorithm
excerpt: 算法第一课：冒泡排序
comments: true
categories: teach-algorithm
---

# 欢迎来到算法基础课程

## 第一课：冒泡排序

### 算法原理

1. **核心思想**：
   - 通过相邻元素的比较和交换
   - 使较大元素逐渐"浮"到数组末端

2. **C++实现**：
```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
```

3. 时间复杂度：
   - [ ] 最好情况： `O(n)` （已排序数组，优化版）
   - [ ] 最坏情况： `O(n^2)` （完全逆序数组）
   - [ ] 平均情况： `O(n^2)` 

4. 空间复杂度：
   - [ ]  `O(1)` （原地排序，仅需常数额外空间）

5. 作业：
   自主实现优化版
   提示: 有`flag`标记
   当循环一轮不交换后直接退出
   输入样例数组`[7,9,8,10,5]`
   
**谢谢大家的观看**
有问题可联系**手机-微信:18372735812**