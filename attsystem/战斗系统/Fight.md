# 战斗机制组

## 介绍

战斗机制组，由 **伤害类型** 及其 **机制组** 构成

## 声明

于 **plugins/AttributeSystem/fight** 文件夹下声明

```yaml
#战斗机制组key
# attack-damage 普通攻击
# skill-api-技能id-标识符 SkillAPI技能
# damage-cause-id小写 伤害事件（会覆盖原版处理机制）
# https://bukkit.windit.net/javadoc/org/bukkit/event/entity/EntityDamageEvent.DamageCause.html
# 这3个是固定的
attack-damage:
  #伤害类型
  Physical:
    #是否启用
    enable: true
    #机制id
    damage:
      #机制数据
      #攻击者变量: {a.PAPI变量/PouPAPI变量}
      #防御者变量: {d.PAPI变量/PouPAPI变量}
      #PouPAPI支持存活实体
      #AS提供的值
      # origin AS处理前的伤害 一般是原版伤害
      # force 蓄力程度  弓箭蓄力程度 或 普攻蓄力程度
      enable: |-
        check random 0 to 1 < calculate '{a.as_att:PhysicalHitChance}-{d.as_att:PhysicalDodgeChance}'
      value: |-
        calculate '{a.as_att:PhysicalDamage}+{origin} * 1- {d.as_att:PhysicalDefense}/ 100+{d.as_att:PhysicalDefense} * {force}'
    #机制从上到下按顺序执行
    crit:
      enable: "check random 0 to 1 < {a.as_att:PhysicalCriticalChance}"
      #下面的机制数据可以调用上面已执行机制的执行结果 格式为{id}
      value: |-
        calculate '{damage} * {a.as_att:PhysicalCriticalDamage}'
    vampire:
      enable: "check random 0 to 1 < calculate {a.as_att:PhysicalVampireChance}"
      value: |-
        calculate '{damage}* {a.as_att:PhysicalVampire_Percent}+{a.as_att:Vampire_Percent} +{a.as_att:PhysicalVampire}+{a.as_att:Vampire}'
  Real:
    enable: true
    damage:
      enable: |-
        check random 0 to 1 < calculate calculate '{a.as_att:PhysicalHitChance}-{d.as_att:PhysicalDodgeChance}'
      value: "{a.as_att:RealDamage}"
```

按照惯例，我们分开来逐一讲解

### 战斗机制组 key [attack-damage]

用于开发人员调用，**AttributeSystem** 默认提供了几个固定触发的:

- attack-damage 普通攻击
- skill-api-技能 id-标识符 SkillAPI 技能
- damage-cause-id 小写 任意伤害事件（会覆盖原版处理机制）
  > https://bukkit.windit.net/javadoc/org/bukkit/event/entity/EntityDamageEvent.DamageCause.html

补充一句，自`1.3.2`支持不同权限不同普攻战斗机制组
见`config.yml`的`options.fight.attack-fight`

### 伤害类型 [Physical / Real]

即伤害类型 id，可以自定义

### 伤害类型启用 [Physical / Real.enable]

固定的，此伤害类型是否启用，支持 **占位符**，**字符串内联函数**

### 机制组 [Physical / Real.damage / crit / vampire]

`damage`,`crit`,`vampire`是机制 id，
这三个是默认提供的，分别用于 `伤害计算` `暴击计算` `吸血`
如果你想实现属于你的伤害逻辑，可以拓展[机制](Mechanic.md)

### 机制参数

每个机制有每个机制的参数，具体由开发者自定义

这里仅列出默认提供的三个机制的参数

#### damage [计算伤害]

| 参数名 |       描述       |                其它                 |
| :----: | :--------------: | :---------------------------------: |
| enable | 是否有伤害(命中) |         若 false 则伤害为 0         |
| value  |      伤害值      | 支持 占位符 字符串内联函数 数字运算 |

#### crit [计算暴击]

| 参数名 |    描述    |                              其它                              |
| :----: | :--------: | :------------------------------------------------------------: |
| enable |  是否暴击  |                    若 false 则跳过暴击计算                     |
| value  | 暴击伤害值 | 会覆盖 damage 计算出的伤害 支持 占位符 字符串内联函数 数字运算 |

#### vampire [吸血]

| 参数名 |   描述   |                其它                 |
| :----: | :------: | :---------------------------------: |
| enable | 是否吸血 |         若 false 则跳过吸血         |
| value  |  吸血值  | 支持 占位符 字符串内联函数 数字运算 |

#### 例子

> 如果有一个机制名 为 `light` (点燃) 参数为 `enable` 是否启用, `time` 持续时间， 我想把它加到普攻 `Physical` 的机制组里，该怎么做？

```yaml
Physical:
  enable: true
  damage:
    enable: |-
      check random 0 to 1 < calculate '{a.as_att:PhysicalHitChance}-{d.as_att:PhysicalDodgeChance}'
    value: |-
      calculate '{a.as_att:PhysicalDamage}+{origin} * 1- {d.as_att:PhysicalDefense}/ 100+{d.as_att:PhysicalDefense} * {force}'
  crit:
    enable: "check random 0 to 1 < {a.as_att:PhysicalCriticalChance}"
    value: |-
      calculate '{damage} * {a.as_att:PhysicalCriticalDamage}'
  vampire:
    enable: "check random 0 to 1 < calculate {a.as_att:PhysicalVampireChance}"
    value: |-
      calculate '{damage}* {a.as_att:PhysicalVampire_Percent}+{a.as_att:Vampire_Percent} +{a.as_att:PhysicalVampire}+{a.as_att:Vampire}'
  light:
    enable: "check random 0 to 1 < {a.as_att:LightChance}"
    time: "{a.as_att:LightTime}"
```

如果你想让 `light`(点燃) 最先执行 那你写到 `damage`(伤害计算) 上方就可以
