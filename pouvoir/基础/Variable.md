###### 本章将会简单地讲解 JavaScript 的语法基础

###### 部分[https://www.runoob.com/js/js-tutorial.html](https://www.runoob.com/js/js-tutorial.html)摘录，如有错误欢迎指正。

# 第一个变量

```javascript
//变量声明方式
var a = "Hello World!";
// 变量名    数据
```

这便是你的第一个变量了，它是用来存放数据的容器。

我们来把上面这个语句拆分来讲

## 变量声明方式

共有四种

- var
- let
- const
- function

这四种声明变量的方式彼此之间的区别体现在：

#### 重复声明

- var 能重复声明，后者覆盖前者
- let 和 const 和 function 则不能重复声明

#### 作用域的范围

- var 的作用域是以函数/整个文件为作用域
- let, function 和 const 是块作用域

#### const 的特殊之处

- 经过 const 方式进行声明，之后赋值完毕，则不可以进行改变。

#### function 的特殊之处

- 与其他三种方式存放数据不同，function 是专门用来声明"函数"的(js 中函数也是变量)
- 不能重复声明

上述四点区别只是概念上的，具体还需你在编写脚本过程中体会

## 变量名

所有 JavaScript 变量必须以唯一的名称的标识。

这些唯一的名称称为标识符。

#### 构造变量名称（唯一标识符）的通用规则是：

- 名称可包含字母、数字、下划线和美元符号
- 名称必须以字母开头
- 名称也可以 $ 和 \_ 开头（但是在本教程中我们不会这么做）
- 名称对大小写敏感（y 和 Y 是不同的变量）
- 保留字（比如 JavaScript 的关键词）无法用作变量名称

> JavaScript 语句和 JavaScript 变量都对大小写敏感。

## 数据类型

变量`a`的类型是 字符串，是**基本类型**之一

有关数据类型，请看 [https://www.runoob.com/js/js-datatypes.html](https://www.runoob.com/js/js-datatypes.html)
