# 公式系统

## 介绍

通过**公式系统**，你可以完成各种**复杂的计算**，以带入到各个地方

## 配置文件

> plugins/AttributeSystem/formula.yml

```yaml
attribute-formulas:
  #右值支持以 {id} 的形式带入上面的公式, PAPI/PPAPI 四则运算
  #会影响实体的原版属性 (完全接管)
  max-health: '%as_att:MaxHealth%'
  #实测正常摩擦系数下，与2250做商运算
  #结果可以近似实现 %as_att:MovementSpeed%/100 /s
  movement-speed: '%as_att:MovementSpeed% / 2250'
  #默认每10tick(0.5s)恢复一次生命值
  #为了方便实现 %as_att:HealthRegain% /s 故将值除以二
  health-regain: '%as_att:HealthRegain% / 2'
  knockback-resistance: '%as_att:Resistance%'

  #下面只支持玩家
  #单位为 攻击次数/s
  attack-speed: '%as_att:AttackSpeed%'
  #单位为格
  attack-distance: '%as_att:AttackDistance%'
  luck: '%as_att:Luck%'
  #不可被上面的公式调用
skill-api:
  #1.0.6 后与SKAPI技能冷却挂钩
  skill-speed: '{cooldown} * (1- (%as_att:SkillSpeed%/(100-%as_att:SkillSpeed%)))'

```

## 调用

#### 用户

变量`%as_formula:公式id%`

#### 开发者

```kotlin
AttributeSystem.formulaManager.get(entity,"max-health")
```