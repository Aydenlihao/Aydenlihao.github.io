---
title: JavaScript 报错类型
date: 2020-09-21 17:38:15
tags:
  - JavaScript基础
category: JavaScript
---

# js 报错类型（6 种错误类型）

js 中的控制台的报错信息主要分为两大类，第一类是语法错误，这一类错误在预解析的过程中如果遇到，就会导致整个 JS 文件都无法执行。另一类错误错误统称为异常，这一类的错误出现的那一行之后的代码无法执行，但在那一行之前的代码不会受到影响。

## SyntaxError(语法错误)

```javascript
// SyntaxError: 语法错误
// 1) 变量名不符合规范
var 1       // Uncaught SyntaxError: Unexpected number
var 1a       // Uncaught SyntaxError: Invalid or unexpected token
// 2) 给关键字赋值
function = 5     // Uncaught SyntaxError: Unexpected token =
```

## ReferenceError（引用错误）

## TypeError（类型错误）

## RangError（范围错误）

## URIError（URI 不合法）
