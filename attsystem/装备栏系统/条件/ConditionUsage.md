# 条件的使用

## 字符串中的条件

### 单行

> 这里的 `/` 与 `,` 均可在 config 中配置
>
> 攻击力: 100/Lv.10,职业限制: 战士

若实体等级未到 10 或 职业不是战士

就不会读取**此行**属性

### 多行

> Lv.100
> 攻击力: 100
> 生命值: 1000

若实体等级未到 100

就不会读取**这些**属性

## NBT 中的条件

格式:

```yaml
CONDITION_DATA:
  #路径中的 "." 要用 "$" 替代
  属性数据路径: "条件1,条件2"
```

非常容易理解，给个例子都会了

某个物品的 NBT:

```yaml
ATTRIBUTE_DATA:
  example-att-data:
    PhysicalDamage:
      value: 100
    MovementSpeed:
      value: 1000
    PhysicalDefense:
      percent: 20
    Luck:
      value: 10
      percent: -20
CONDITION_DATA:
  example-att-data: "Lv.50"
  example-att-data$MovementSpeed: "Lv.100"
  example-att-data$PhysicalDefense: "Lv.120,职业: 肉盾"
  example-att-data$Luck$percent: "职业: 枪兵"
```

如此一来，玩家装备此物品时：
当玩家`等级>50`时，`example-att-data` 属性组才生效
当玩家`等级>100`时，`MovementSpeed` 属性才生效
当玩家`等级>120` 且 `职业是肉盾` 时，`PhysicalDefense` 属性才生效
当玩家`职业是枪兵` 时，`Luck` 属性的 `percent: -20` 才生效
