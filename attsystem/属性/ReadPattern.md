# 读取格式

## 介绍

**AttributeSystem** 中，**读取格式**负责**属性**的 **读取** **记录** **获取**

## 读取 & 记录(ReadGroup & NumberStatus)

即读取字符串中的属性

例如: 攻击力: 100

逐一尝试所有属性的读取组读取，若有读到则继续

通过正则捕获组捕获到值 并以组key为键缓存值

完成读取

## 获取(ReadGroup & NumberStatus)

### 用户

通过变量`%as_att:属性ID_占位符id%`获取值

### 开发者

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
```

## 声明(ReadGroup -> 用户)

于 **plugins/AttributeSystem/read** 文件夹下任意一个**YAML文件**中声明

```yaml
Default:
  #总值
  total: '(<value> + random(<valueMin>,<valueMax>))*(1+(<percent>/100 + random(<percentMin>,<percentMax>)/100))'
  #读取格式(正则)
  #这里<捕获组id> = (?<name>{config.yml::number_pattern})
  #从上到下先后匹配
  #特殊字符要转义
  patterns:
    # 攻击力: 11-23(%)
    - '<name>: <percentMin>-<percentMax>\(%\)'
    # 攻击力: 10-20
    - '<name>: <valueMin>-<valueMax>'
    # 攻击力: 10(%)
    - '<name>: <percent>\(%\)'
    # 攻击力: 100
    - '<name>: <value>'
  #变量(PAPI / PouPAPI)
  #调用变量格式: %as_att:属性ID_下面的id%
  placeholder:
    #占位符id
    #可带入上面patterns中获取到的值
    total: <total>
    value: <value>
    percent: <percent>/100
    valueMin: <valueMin>
    valueMax: <valueMax>
    percentMin: <percentMin>/100
    percentMax: <percentMax>/100
    valueRandom: <value> + random(<valueMin>,<valueMax>)
    percentRandom: (<percent>/100 + random(<percentMin>,<percentMax>)/100)
```

### 例子

目标： 

让读取格式读取`攻击力: 100(+10)`格式的属性

```yaml
Add:
  #总值
  total: '(<value> + <value2> + random(<valueMin>,<valueMax>))*(1+(<percent>/100 + random(<percentMin>,<percentMax>)/100))'
  #读取格式(正则)
  #从上到下先后匹配
  #特殊字符要转义
  patterns:
    # 攻击力: 11-23(%)
    - '<name>: <percentMin>-<percentMax>\(%\)'
    # 攻击力: 10-20
    - '<name>: <valueMin>-<valueMax>'
    # 攻击力: 10(%)
    - '<name>: <percent>\(%\)'
    # 攻击力: 100(+100)
    - '<name>: <value> (<value2>)'
    # 攻击力: 100
    - '<name>: <value>'
  #变量(PAPI / PouPAPI)
  #调用变量格式: %as_att:属性ID_下面的id%
  placeholder:
    #占位符id
    #可带入上面patterns中获取到的值
    total: <total>
    value: <value>
    percent: <percent>/100
    valueMin: <valueMin>
    valueMax: <valueMax>
    percentMin: <percentMin>/100
    percentMax: <percentMax>/100
    valueRandom: <value> + random(<valueMin>,<valueMax>)
    percentRandom: (<percent>/100 + random(<percentMin>,<percentMax>)/100)
```

应该都能看懂吧

## 声明(ReadPattern -> 开发者)

实现[**ReadPattern**](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/read/ReadPattern.html)并注册至[**ReadPatternManager**](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/manager/ReadPatternManager.html)即可

使用时的属性不能是**ConfigAttribute**，需要自己实现一个**Attribute** (因为**ConfigAttribute**参数是**ReadGroup**)