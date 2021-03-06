---
layout: post
title: "八种排序算法之3 冒泡排序(Bubble Sort)"
keywords: [""]
description: ""
category: "algorithm"
tags: [bubblesort, sort, algorithm]
---
{% include JB/setup %}

### 一、基本思想
* 由字面意思: 
    * 鱼儿吐泡般，将轻的泡往上浮, i个泡总共需要i-1轮
    * j从len-1(最后一个元素)到每次都有一个相对最轻的泡到相对顶部
    * 这个过程隐含将重的泡往下挤, 直到所有轻的泡都浮在重的泡上面
* 完全相反的方法:
    * 相对于轻的泡上浮，相反的思路是重的泡下沉.

### 二、基础

### 三、解题方法

#### (1)轻泡上浮

```
// 轻泡上浮法
void BubbleSort(int array[], int len) {
    // 总共len个元素，每轮有一个元素到达相对顶部，那么至少冒泡len-1轮
    // i+1正好表示第几轮
    // i+1正好表示冒泡后顶部第i+1个元素a[i], 此时a[i]是相对最小的
    for (int i=0; i<len-1; ++i) {
        // 从当前最后一个元素开始冒泡, 轻泡上浮最上
        // 当前最后一个元素是a[i]=a[j]
        // 然后不断比较j(后)和j-1(前)
        //      如果满足a[j]<a[j-1], 说明后一个元素比前一个元素轻，应该将气泡上浮
        //      否则说明前一个(上面)的气泡更轻，不用移动
        //   然后j=j-1, 即上浮后的元素再跟它前一个元素比较，直到j=i+1, 也即到相对的第一个元素
        //   每一轮都会使一个相对最小的元素上浮到顶部(此时的最顶部是j-1=i)
        // 然后进入下一轮i
        for (int j=len-1; j>i; --j)
            if (array[j] < array[j-1])
                Swap(array[j], array[j-1]);

        cout << "第 " << i+1 << " 轮排序第" << i+1 << "个元素: " << array[i] << endl;
        display(array, len);
    }
}
```

#### (2)重泡下沉

```
// 重泡下沉法
void BubbleSortDown(int array[], int len) {
    // 总共len-1轮
    for (int i=0; i<len-1; ++i) {
        // 该步是和 轻泡上浮法 的关键区别
        // 每一轮有一个最重的泡到相对最底部(与轻泡上浮每次一个最轻到泡到相对最顶部)
        // 每次都是从第一个元素j=0开始，直到j=len-1-i+1, 因为每一步步是j和j+1, 最后异步步j=len-i-1 + 1时, j+1=len-1-i是相对最后一个元素
        for (int j=0; j<len-i-1; ++j) {
            if (array[j] > array[j+1])
                Swap(array[j], array[j+1]);
        }
    }
}
```

### 四、总结 
* `重点理解总共需要len-1轮, 而每一轮是内部全比较(除了上一轮的最轻元素，它已经在最顶部)，浮出相对最轻气泡.`
* 这里所有的｀相对最轻`、`相对最重`、`相对顶部`等里的`相对`
    * 是指: `每一轮和上一轮找到上浮最轻的元素到顶部或者下沉最重的元素到顶部后，剩下的元素之间比较，浮出此时的最轻或下沉此时的最重.`

### 五、参考
* [维基百科-冒泡排序(下沉法)](https://zh.wikipedia.org/wiki/冒泡排序)
