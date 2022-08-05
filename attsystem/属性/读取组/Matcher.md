# 捕获组

## 什么是捕获组？

```yaml
YourReadGroup:
  total: "<value> * (1 + (<percent>/100) )"
  patterns:
    #<name>是属性名，不是捕获组
    #在读取组中，除<name>外，像 <value> 和 <percent> 这样的都是捕获组
    #且在同一个读取组内唯一
    - '<name>: <percent>\(%\)'
    - "<name>: <value>"
  placeholder:
    total: <total>
    value: <value>
    percent: <percent>/100
```

## 捕获组能干什么？

在**读取组**中，**捕获组**用于捕获字符串中的数字部分，并可以存储它们做运算操作的结果

## 如何获取？

你需要在 总值公式 / 占位符公式 中通过`<捕获组id>`来调用捕获组值，
并通过占位符 `%as_att:属性id_占位符id%` 来获取.

## 我在公式中调用时，获取到的是什么？

是此实体身上所有此捕获组的值在做**相应运算操作**后的结果

## 什么是 “相应运算操作” ？

在**AttributeSystem**中，每个**捕获组**都有一种对应的**运算操作**，默认是 "**加**"(`Plus`)

## 都有哪些运算操作？

**AttributeSystem** 默认提供了

- **Max** 取最大值
- **Min** 取最小值
- **Plus** 做加法
- **Reduce** 做减法
- **Scalar** 做乘法
  共 5 种**运算操作**，如有需要，你可以通过编写脚本/代码拓展

## 如何指定一个捕获组的运算操作？

`<运算操作id:捕获组id>`
例子:

```yaml
YourReadGroup:
  #                                         这里是字符串内嵌函数: 如果<test_scalar>值等于0，则乘1，否则乘<test_scalar>
  total: "(<value> * (1 + (<percent>/100) ) ) * {if check <test_scalar> == 0 then 1 else <test_scalar>} "
  patterns:
    - '<name>: <percent>\(%\)'
    #就像这样
    - "<name>*<scalar:test_scalar>"
    - "<name>: <value>"

  placeholder:
    total: <total>
    value: <value>
    scalar_value: <test_scalar>
    percent: <percent>/100
```

这样一来，`<test_scalar>` 在读取时便会将每个捕获到的值相乘，再存入**属性状态**
