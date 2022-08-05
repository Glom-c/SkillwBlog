# 机制

## 介绍

**机制** 是 **AttributeSystem** 的一大特色，你可以通过编写**机制**并在**战斗机制组**中使用来操纵**战斗过程**

## 声明

#### 配置

于 **plugins/Attributes/mechanics** 文件夹下任意一个**YAML 文件**中声明

```yaml
# damage 计算伤害值
damage:
  script: "mechanics.groovy::damage"
# crit 计算暴击值
#用js或groovy都能写
crit:
  script: "mechanics.js::crit"
vampire:
  script: "mechanics.groovy::vampire"
```

#### 代码

编写 [com.skillw.attsystem.api.mechanic.Mechanic](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/mechanic/Mechanic.html) 的子类，并调用 **Mechanic#register** 以完成注册

```kotlin
object: Mechanic("fire"){
   override fun apply(fightData: FightData, context: Map<String, Any>, damageType: DamageType): Any?{
        if (context["enable"] != "true") return null
        val defender = fightData.defender
        val time = Coerce.toInteger(context["time"])
        defender.fireTicks = time
        return time
   }
}.register()
```
