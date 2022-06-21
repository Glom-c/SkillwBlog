# 战斗机制组

## 介绍

战斗机制组，由 **触发器** 与 **伤害类型机制组** 构成

## 声明

于 **plugins/Attributes/fight** 文件夹下声明

```yaml
#公式组ID
attack-damage:
  #触发器
  # attack 普通攻击
  # skill-api-技能id-标识符 SkillAPI技能
  # mythic-mobs-伤害标签 MM技能
  # origin-skill-伤害标签
  trigger: attack
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
      # origin AS处理前的伤害(一般是原版伤害)
      # force 蓄力程度( 弓箭蓄力程度 或 普攻蓄力程度 )
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalHitChance}-{d.as_att:PhysicalDodgeChance}),true,false)'
      value: '(({a.as_att:PhysicalDamage}+{origin})*(1-({d.as_att:PhysicalDefense}/(100+{d.as_att:PhysicalDefense})))) * {force}'
    #机制从上到下按顺序执行
    crit:
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalCriticalChance}),true,false)'
      #下面的机制数据可以调用上面已执行机制的执行结果 格式为{id}
      value: '{damage}*(2+{a.as_att:PhysicalCriticalMultiple})'
    vampire:
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalVampireChance}),true,false)'
      value: '{damage}*({a.as_att:PhysicalVampire_Percent}+{a.as_att:Vampire_Percent})+{a.as_att:PhysicalVampire}+{a.as_att:Vampire}'
  Real:
    enable: true
    damage:
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalHitChance}-{d.as_att:PhysicalDodgeChance}),true,false)'
      value: '{a.as_att:RealDamage}'
```

#### 触发器

- attack 普通攻击
- skill-api-技能id-标识符 SkillAPI技能
- mythic-mobs-伤害标签 MM技能
- origin-skill-伤害标签

#### 伤害类型机制组

```yaml
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
      # origin AS处理前的伤害(一般是原版伤害)
      # force 蓄力程度( 弓箭蓄力程度 或 普攻蓄力程度 )
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalHitChance}-{d.as_att:PhysicalDodgeChance}),true,false)'
      value: '(({a.as_att:PhysicalDamage}+{origin})*(1-({d.as_att:PhysicalDefense}/(100+{d.as_att:PhysicalDefense})))) * {force}'
    #机制从上到下按顺序执行
    crit:
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalCriticalChance}),true,false)'
      #下面的机制数据可以调用上面已执行机制的执行结果 格式为{id}
      value: '{damage}*(2+{a.as_att:PhysicalCriticalMultiple})'
    vampire:
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalVampireChance}),true,false)'
      value: '{damage}*({a.as_att:PhysicalVampire_Percent}+{a.as_att:Vampire_Percent})+{a.as_att:PhysicalVampire}+{a.as_att:Vampire}'
```

> 如果有一个机制id为 "light" 参数为 enable 是否启用, time 持续时间， 我想把它加到普攻里，该怎么做？

```yaml
  Physical:
    enable: true
    damage:
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalHitChance}-{d.as_att:PhysicalDodgeChance}),true,false)'
      value: '(({a.as_att:PhysicalDamage}+{origin})*(1-({d.as_att:PhysicalDefense}/(100+{d.as_att:PhysicalDefense})))) * {force}'
    crit:
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalCriticalChance}),true,false)'
      value: '{damage}*(2+{a.as_att:PhysicalCriticalMultiple})'
    vampire:
      enable: 'if(random(0,1),<,calculate({a.as_att:PhysicalVampireChance}),true,false)'
      value: '{damage}*({a.as_att:PhysicalVampire_Percent}+{a.as_att:Vampire_Percent})+{a.as_att:PhysicalVampire}+{a.as_att:Vampire}'
    light:
      enable: 'if(random(0,1),<,calculate({a.as_att:LightChance}),true,false)'
      time: '{a.as_att:LightTime}'
```

你想让light最先执行 那你写到damage上方也可以
