# 字符串内联函数

均支持

- 代入 PAPI / PouPAPI 变量
- 嵌套

## abs

#### 参数

1. 数字

#### 作用

取绝对值

#### 例子

`abs -100`

返回 100

## calculate

#### 参数

1. 公式
2. 参数.... (可选)

#### 作用

计算公式

#### 例子

`calculate '10+20'`

返回 30

## ceil

#### 参数

1. 数字

#### 作用

向上取整

#### 例子

`ceil 0.1 `

返回 1

## floor

#### 参数

1. 数字

#### 作用

向下取整

#### 例子

`floor 1.1 `

返回 1

## format

#### 参数

1. 数字
2. 格式

#### 作用

格式化数字

#### 例子

`format 1.12312 #.## `

返回 1.12

附:

![num_format.png](images/num_format.png)

## if

#### 参数

不使用短路与/短路或

1. bool 值 (true / false)
2. then + 真值
3. else + 假值

使用

1. bool 值 (true / false)
2. || 或 &&
3. bool 值 (true / false)
4. then + 真值
5. else + 假值

#### 作用

逻辑判断

#### 例子

`if check %player_name% == 'Neige' && check %player_level% == 0 then '太菜了,菜!' else '菜'`

若为 玩家 Neige 且等级为 0

返回 太菜了,菜!

否则

返回 菜

## max

#### 参数

1. 数字 1
2. 数字 2

#### 作用

取两者最大值

#### 例子

`max -100 100 `

返回 100

## min

#### 参数

1. 数字 1
2. 数字 2

#### 作用

取两者最小值

#### 例子

`min -100 100 `

返回 -100

## random

#### 参数

1. 最小值
2. 最大值
3. 数字格式(可选)

#### 作用

返回区间内随机小数

#### 例子

`random 0 1`

返回 0.66

(format 参数默认为 #.## )

## randomInt

#### 参数

1. 最小整数
2. 最大整数

#### 作用

返回两整数区间内的随机整数

#### 例子

`randomInt 1 4 `

返回 2

## round

#### 参数

1. 数字

#### 作用

四舍五入

#### 例子

`round 1.233 `

返回 1

## weight

#### 参数

1. 权重(整数) to 任意对象 ...

#### 作用

返回权重随机结果

#### 例子

`weight [ 1 to a , 2 to b]`

大概率返回 b

小概率返回 a

## set

#### 参数

1. 变量名
2. to 值(可以填函数)

#### 作用

赋值变量

#### 例子

`set a to check 1 == 2`

a 赋值为 false
并返回 false

## &

#### 参数

1. 变量名

#### 作用

取变量

#### 例子

`&a`
若 a 有值，则返回 a 变量的值
否则返回 '&a'

## analysis

#### 参数

1. 字符串

#### 作用

解析字符串

#### 例子

```
set name to 'Neige'
analysis 'hi! i'm a { if check &name == Neige then Neige else Human } !'
```

返回`hi! i'm a Neige`
