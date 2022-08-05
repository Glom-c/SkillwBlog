# 读取组

###### ReadPattern 子类，用于读取数字属性

## 介绍

**AttributeSystem** 中，**读取组**负责**数字属性**的**属性**的 **读取** **记录** **获取**

> 你可以通过编写 **ReadPattern** 子类来实现自定义读取格式（字符串属性/其它属性）

下面来介绍一下 **读取组** 的功能^(不是读取格式，是读取组!)^

## 读取 & 记录(ReadGroup & NumberStatus)

即读取 `字符串 & NBT` 中的**数字属性**(理解为读取格式是**读取组**的属性)

例如: `攻击力: 100`

```yaml
ATTRIBUTE_DATA:
  example_data:
    PhysicalDamage:
      value: 100
```

如果 `攻击力[PhysicalDamage]` 的**读取格式**是**读取组** (AS 默认带的就是)
那么这些 `字符串 & NBT` 都会作为参数传入对应的读取组，由**读取组**进行**数字属性**的读取
读取之后，读取组会将**捕获组**与**其捕获到的值**存入**属性状态** (后面会讲)

## 获取

通过变量`%as_att:属性ID_占位符id%`获取值

> 这个占位符适用于所有属性，不仅仅是"读取组的属性"

<!-- ### 开发者

详见: [ReadGroup](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/read/ReadGroup.html) & [NumberStatus](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/status/NumberStatus.html)

捕获组值

```kotlin
//这里的属性需是 ConfigAttribute 的子类
(AttributeSystem.attributeDataManager[uuid].getStatus("属性id") as NumberStatus).get("捕获组id")
```

变量值

```kotlin
//这里的属性需是 ConfigAttribute 的子类
val attribute = AttributeSystem.attributeManager["属性id"]
val readGroup = attribute.readGroup
val status = AttributeSystem.attributeDataManager[uuid].getStatus(attribute)
val value = readGroup.placeholder("占位符ID",attribute,status,livingEntity)
``` -->

## 自定义读取组

于 **plugins/AttributeSystem/read** 文件夹下任意一个**YAML 文件**中声明

```yaml
YourReadGroup:
  #总值公式，简单实现一个基本读取功能
  total: "<value> * (1 + (<percent>/100) )"
  #匹配格式(正则)
  #除"<name>"代表属性名外，其它由"<>"围起来的是捕获组
  #从上到下先后匹配，直到匹配到为止
  patterns:
    # 攻击力: 10(%)
    - '<name>: <percent>\(%\)'
    # 攻击力: 100
    - "<name>: <value>"
  #自定义变量(PAPI / PouPAPI)
  #调用变量格式: %as_att:属性ID_下面的id%
  placeholder:
    #占位符id
    #可带入上面patterns中的捕获组
    total: <total>
    value: <value>
    percent: <percent>/100
```

让我们拆开来分析 **读取组**.

### 键 [key]

读取组唯一标识符，(填到属性的`read-pattern`)

### 总值公式 [total]

总值公式支持所有**占位符**，**字符串内联函数**，**数字运算**
可以用 `<捕获组id>` 来带入**捕获组**捕获到的值

一般用于通过`%as_att:属性id%`获取**数字属性总值**

> 如果`%as_att:属性id_占位符id%`不填写`占位符id`则默认获取总值

### 匹配格式 [patterns]

- `<name>` 属性名 读取时会被属性名替换
- `<捕获组id>` 捕获组 读取时会被 (?<捕获组 id>(\+|\-)?(\d+(?:(\.\d+))?)) 替换
  (下节会详细讲)

### 占位符公式 [placeholder]

用于自定义占位符
支持所有**占位符**，**字符串内联函数**，**数字运算**
可以用 `<捕获组id>` 来带入**捕获组**捕获到的值
可以通过 `%as_att:属性ID_下面的id%` 获取

## 例子

目标：

让读取格式读取`攻击力: 100(+10)`格式的属性

```yaml
Add:
  total: "<value> * (1 + (<percent>/100) ) + <value2>   "
  patterns:
    # 攻击力: 10(%)
    - '<name>: <percent>\(%\)'
    # 攻击力: 100(+100)
    - "<name>: <value> (\\+<value2>)"
    # 攻击力: 100
    - "<name>: <value>"
  #变量(PAPI / PouPAPI)
  #调用变量格式: %as_att:属性ID_下面的id%
  placeholder:
    #占位符id
    #可带入上面patterns中获取到的值
    total: <total>
    value: <value>
    percent: <percent>/100
```

应该都能看懂吧

<!-- ## 声明(ReadPattern -> 开发者)

实现[**ReadPattern**](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/read/ReadPattern.html)并注册至[**ReadPatternManager**](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/manager/ReadPatternManager.html)即可

使用时的属性不能是**ConfigAttribute**，需要自己实现一个**Attribute** (因为**ConfigAttribute**参数是**ReadGroup**) -->
