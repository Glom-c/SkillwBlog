# NBT

## 格式

```yaml
ATTRIBUTE_DATA:
  AttributeData_key:
    #属性(状态)key
    Attribute_key:
      #属性状态的具体内容
      Matcher_key: value
```

若一个 key 为`ExampleAtt`的属性，其读取组为`YourReadGroup`

```yaml
ExampleAtt:
  priority: 1
  names:
    - "暴击"
  read-pattern: YourReadGroup
```

```yaml
YourReadGroup:
  total: "<value> * (1 + (<percent>/100) )"
  patterns:
    - "<name>: <percent>\(%\)"
    - "<name>: <value>"
  placeholder:
    total: <total>
    value: <value>
    percent: <percent>/100
```

在 **NBT** 中，需要像这样书写属性数据:

```yaml
ATTRIBUTE_DATA:
  #这里写什么都行，别重复
  example-key:
    ExampleAtt:
      value: 100
      percent: 10
```
