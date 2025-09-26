---
title: algorithm4
date: 2025-09-26 18:32:39
tags: teach-algorithm
excerpt: 算法第四课：高精度算法
comments: true
categories: teach-algorithm
---
# 欢迎来到算法基础课程

## 第四课：高精度算法

### 算法原理

- **核心思想**：
  - 使用数组或字符串存储大整数，每一位数字单独存放
  - 模拟人工计算过程，实现加、减、乘、除等运算

- **适用场景**：
  - 处理超出基本数据类型范围的大整数运算（如1000位数字）
  - 需要精确计算，避免浮点数精度误差

### C++实现

#### 高精度加法

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

vector<int> add(vector<int>& A, vector<int>& B) {
    vector<int> C;
    int t = 0; // 进位
    for (int i = 0; i < A.size() || i < B.size(); i++) {
        if (i < A.size()) t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }
    if (t) C.push_back(1); // 处理最高位进位
    return C;
}

int main() {
    string a, b;
    cin >> a >> b;
    
    vector<int> A, B;
    for (int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i--) B.push_back(b[i] - '0');
    
    vector<int> C = add(A, B);
    
    for (int i = C.size() - 1; i >= 0; i--) cout << C[i];
    return 0;
}
```

#### 高精度减法

```cpp
#include <iostream>
#include <vector>
using namespace std;

// 判断A是否大于等于B
bool cmp(vector<int>& A, vector<int>& B) {
    if (A.size() != B.size()) return A.size() > B.size();
    for (int i = A.size() - 1; i >= 0; i--) {
        if (A[i] != B[i]) return A[i] > B[i];
    }
    return true;
}

vector<int> sub(vector<int>& A, vector<int>& B) {
    vector<int> C;
    int t = 0; // 借位
    for (int i = 0; i < A.size(); i++) {
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if (t < 0) t = 1;
        else t = 0;
    }
    while (C.size() > 1 && C.back() == 0) C.pop_back(); // 去除前导0
    return C;
}

int main() {
    string a, b;
    cin >> a >> b;
    
    vector<int> A, B;
    for (int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i--) B.push_back(b[i] - '0');
    
    if (cmp(A, B)) {
        vector<int> C = sub(A, B);
        for (int i = C.size() - 1; i >= 0; i--) cout << C[i];
    } else {
        vector<int> C = sub(B, A);
        cout << "-";
        for (int i = C.size() - 1; i >= 0; i--) cout << C[i];
    }
    return 0;
}
```

#### 高精度乘法

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> mul(vector<int>& A, vector<int>& B) {
    vector<int> C(A.size() + B.size(), 0);
    
    for (int i = 0; i < A.size(); i++) {
        for (int j = 0; j < B.size(); j++) {
            C[i + j] += A[i] * B[j];
        }
    }
    
    // 处理进位
    for (int i = 0; i < C.size() - 1; i++) {
        C[i + 1] += C[i] / 10;
        C[i] %= 10;
    }
    
    while (C.size() > 1 && C.back() == 0) C.pop_back(); // 去除前导0
    return C;
}

int main() {
    string a, b;
    cin >> a >> b;
    
    vector<int> A, B;
    for (int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i--) B.push_back(b[i] - '0');
    
    vector<int> C = mul(A, B);
    
    for (int i = C.size() - 1; i >= 0; i--) cout << C[i];
    return 0;
}
```

#### 高精度除法

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// 比较两个大数的大小
bool cmp(vector<int>& A, vector<int>& B) {
    if (A.size() != B.size()) return A.size() > B.size();
    for (int i = A.size() - 1; i >= 0; i--) {
        if (A[i] != B[i]) return A[i] > B[i];
    }
    return true;
}

// 减法函数
vector<int> sub(vector<int>& A, vector<int>& B) {
    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i++) {
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if (t < 0) t = 1;
        else t = 0;
    }
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}

// 大数除法
vector<int> div(vector<int>& A, vector<int>& B, vector<int>& r) {
    vector<int> C;
    r.clear();
    
    for (int i = A.size() - 1; i >= 0; i--) {
        r.insert(r.begin(), A[i]);
        while (r.size() > 1 && r.back() == 0) r.pop_back();
        
        int quotient = 0;
        while (cmp(r, B)) {
            r = sub(r, B);
            quotient++;
        }
        C.push_back(quotient);
    }
    
    reverse(C.begin(), C.end());
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}

int main() {
    string a, b;
    cin >> a >> b;
    
    vector<int> A, B;
    for (int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i--) B.push_back(b[i] - '0');
    
    vector<int> remainder;
    vector<int> quotient = div(A, B, remainder);
    
    cout << "商：";
    for (int i = quotient.size() - 1; i >= 0; i--) cout << quotient[i];
    cout << endl << "余数：";
    for (int i = remainder.size() - 1; i >= 0; i--) cout << remainder[i];
    
    return 0;
}
```

### 算法性能

- 时间复杂度:
  - 加法：O(n)
  - 减法：O(n)
  - 乘法：O(n²)
  - 除法：O(n²)

- 空间复杂度:
  - O(n) (需要存储每一位数字)

- 算法特点:
  - 可以处理任意位数的大整数运算
  - 计算结果精确无误
  - 代码实现相对简单，但需要注意细节处理（如进位、借位、前导0等）

### 应用场景

- 大数计算（如阶乘、斐波那契数列等）
- 密码学中的大数运算
- 科学计算和金融计算中的精确计算
- 竞赛编程中的高精度题目

### 课程结束

- 作业:
  - 实现高精度阶乘计算
  - 以下是测试用例
  ```cpp
  #测试用例1
  n1=1000;
  #测试用例2
  n2=9392
  ```
  - 输出结果并用计算器验证是否正确

**谢谢大家的观看**
有问题可联系**手机-微信:18372735812**
