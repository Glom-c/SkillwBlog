# Buff

## 自定义

于 **plugins/BuffSystem/buff** 文件夹下任意一个**YAML 文件**

```yaml
#Buff key (id)
example:
  name: "示例Buff"
  #条件
  conditions:
    - "time"
  #效果
  effects:
    - "example-attribute"
```

## 使用

指令`/buff add Glom_ 任意key example {duration:-1}`
亦或者[**MM 机制**](../其它/MythicMobs.md)
