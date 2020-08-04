+++
author = "John Doe"
categories = ["SEO Learning"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-3.jpg"
title = "My awesome blog post"
type = "post"

+++
### 问题

数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

### 示例

输入：n = 3

输出：\[

"((()))",

"(()())",

"(())()",

"()(())",

"()()()"

\]

### 解析

使用递归方式，设置条件 left == n && right == n ，当条件满足时，跳出递归。在设置正确性验证方法，left < n 控制 ‘(’ 递归，left > right 控制 ‘)’ 递归，同时降低递归次数。

    func generateParenthesis(_ n: Int) -> [String] {
        var result: [String] = []
        generate(n, left: 0, right: 0, current: "", result: &result)
        return result
      }
    
      private func generate(_ n: Int, left: Int, right: Int, current: String, result: inout [String]) {
        if left == n && right == n {
          result.append(current)
          return
        }
    
        if left < n {
          generate(n, left: left + 1, right: right, current: current + "(", result: &result)
        }
    
        if left > right {
          generate(n, left: left, right: right + 1, current: current + ")", result: &result)
        }
    }

### 代码

简单介绍：对上面代码进行修整，最终得到如下代码：

> 时间复杂度：O(n²)

    class Solution {
        var ans = [String]()
        
        func generateParenthesis(_ n: Int) -> [String] {
            fork(left: n, right: n, current: "")
            return ans
        }
        
        func fork(left: Int, right: Int, current: String) {
            if right > 0 {
                if left > 0 {
                    fork(left: left - 1, right: right, current: current + "(")
                }
                if right > left {
                    fork(left: left, right: right - 1, current: current + ")")
                }
            } else {
                ans.append(current)
            }
        }
    }