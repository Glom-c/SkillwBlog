# 字符串

## 格式

以默认提供的`YourReadGroup`读取组为例

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

属性名: 属性值(%) 属性值-> percent
属性名: 属性值 属性值-> value

> 字符串中的属性，需要符合此属性读取组的格式
