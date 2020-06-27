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

## #1

Given a list of numbers and a number `k`, return whether any two numbers from the list add up to `k`.

For example, given `[10, 15, 3, 7]` and `k` of `17`, return true since `10 + 7` is `17`.



**Solution:**

```python
numbers=input()
numlist=numbers.split(" ")
numlist = [int(numlist[i]) for i in range(len(numlist))] #for循环，把每个字符转成int值
k=int(input())
for i in range(0,len(numlist)):
    j=i+1
    for j in range(j,len(numlist)):
        if numlist[i]+numlist[j]==k:
            print("true,"+"since"+str(numlist[i])+"+"+str(numlist[j])+"="+str(k))
    break
```

**Result:**

![](https://raw.githubusercontent.com/Jialong-c/images/master/Blog/coding/#1.png)