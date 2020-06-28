---
layout:          post
title:               Daily Coding Problem
subtitle:         Daily Coding Problem
date:              2020-06-27
author:          Jialong
header-img:  
catalog:          true
---

># Daily Coding Problem

## Problem #1 [Easy]

Given a list of numbers and a number `k`, return whether any two numbers from the list add up to `k`.

For example, given `[10, 15, 3, 7]` and `k` of `17`, return true since `10 + 7` is `17`.



**Solution:**

```python
numbers = input()
numlist = numbers.split(" ")
numlist = [int(numlist[i]) for i in range(len(numlist))]  # for循环，把每个字符转成int值
k = int(input())
for i in range(0, len(numlist)):
    j = i + 1
    for j in range(j, len(numlist)):
        if numlist[i] + numlist[j] == k:
            print("true," + "since" + str(numlist[i]) + "+" + str(numlist[j]) + "=" + str(k))
    break

```

**Result:**

![](https://raw.githubusercontent.com/Jialong-c/images/master/Blog/coding/problem1.png)



## Problem #2 [Hard]

Given an array of integers, return a new array such that each element at index `i` of the new array is the product of all the numbers in the original array except the one at `i`.

For example, if our input was `[1, 2, 3, 4, 5]`, the expected output would be `[120, 60, 40, 30, 24]`. If our input was `[3, 2, 1]`, the expected output would be `[2, 3, 6]`.



**Solution:**

```python
numbers = input()
numlist = numbers.split(" ")
numlist = [int(numlist[i]) for i in range(len(numlist))]
numlist_result = []
#分别取出列表各值进行运算，并保存到列表numlist_result
for i in range(len(numlist)):
    temp = numlist.pop(i)
    sum = 1
    for j in range(len(numlist)):
        sum = numlist[j] * sum
    numlist_result.append(sum)
    numlist.insert(i, temp)
print(numlist_result)
```

**Result:**

![](https://raw.githubusercontent.com/Jialong-c/images/master/Blog/coding/problem2_1.png)

![](https://raw.githubusercontent.com/Jialong-c/images/master/Blog/coding/problem2_2.png)