# Buff 数据

你需要了解一下**BuffSystem**中的**Buff 数据**

## 什么是 Buff 数据[BuffData]?

**BuffSystem** 中，**Buff**生效时的环境(变量存储的地方)

## 为什么要给用户讲?

因为用户需要调用**Buff 数据**中的**变量**来实现功能

## 怎么调用？

通过`{变量id}`来调用变量

## 传递数据

通过 **JSON** 来进行快速传参

### 例子

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

```yaml
#效果key
example-attribute:
  #效果类型
  type: attribute
  attributes:
  #             字符串内联函数
    - '移动速度: {calculate '1000+100 * {level}'}'
```

指令`/buff add Glom_ 任意key example {duration:-1,level:10}`
亦或者[**MM 机制**](../其它/MythicMobs.md)
