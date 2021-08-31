---
title: 【LeetCode】9. Palindrome Number
categories:
  - 算法与数据结构
  - LeetCode
description: 9.回文数。主题：数学，难度：容易
abbrlink: 7f748733
date: 2019-08-02 10:45:01
tags:
keywords:
---

## 1.题目描述

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**Example 1:**

> Input: 121
> Output: true

**Example 2:**

> Input: -121
> Output: false
> Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

**Example 3:**

> Input: 10
> Output: false
> Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

**Follow up:**

Coud you solve it without converting the integer to a string?

你能不将整数转为字符串来解决这个问题吗？

## 2.Solutions

~~~java
public static boolean isPalindrome(int x) {
    if(x < 0) return false;
    int y = x;
    int res = 0;
    while(y != 0) {
        res = res * 10 + y % 10;
        y /= 10;
    }
    return x == res;
}
~~~

Scala版

~~~scala
object Solution {
    def isPalindrome(x: Int): Boolean = {
        if(x < 0)
          return false
        var y = x
        var result = 0
        while(y != 0){
          result = result * 10 + y%10
          y /= 10
        }
        result == x
    }
}
~~~

<center><font style="font-weight:bold">（完）</font></center>