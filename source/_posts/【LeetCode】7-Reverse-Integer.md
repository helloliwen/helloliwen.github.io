---
title: 【LeetCode】7.Reverse Integer
categories:
  - 算法与数据结构
  - LeetCode
description: 7. 整数反转，主题：数学，难度：容易
abbrlink: 787344f6
date: 2020-07-31 22:30:34
tags:
keywords:
---

## 1.题目描述

Given a 32-bit signed integer, reverse digits of an integer.

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

**Example 1:**

```
Input: 123
Output: 321
```

**Example 2:**

```
Input: -123
Output: -321
```

**Example 3:**

```
Input: 120
Output: 21
```

**Note:**
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2<sup>31</sup>, 2<sup>31</sup> − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−2<sup>31</sup>, 2<sup>31</sup> − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

## 2.Solutions

~~~scala
object Solution {
    def reverse(x: Int): Int = {
        if(!isValidInteger(x))
          return 0

        if(x < 0)
          return -reverseUtil(-x)

        return reverseUtil(x)
    }
    
    def reverseUtil(x: Int): Int = {
        var result: Long = 0
        var vx = x
		//类似于9. Palindrome Number
        while (vx != 0) {
          result = result * 10 + vx % 10
          if(!isValidInteger(result))
            return 0
          vx /= 10
        }

        result.toInt
      }

      // Check if x is a valid integer.
      def isValidInteger(x: Long): Boolean = {
        if(x > Int.MaxValue || x < Int.MinValue)
          return false
        true
      }
}
~~~

<center><font style="font-weight:bold">（完）</font></center>

