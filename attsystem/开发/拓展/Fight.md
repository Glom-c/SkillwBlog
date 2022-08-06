# 触发战斗机制组

见方法[`AttributeSystemAPI.playerAttackCal`](http://doc.skillw.com/attsystem/-attribute-system/com.skillw.attsystem.api/-attribute-system-a-p-i/player-attack-cal.html) / [`AttributeSystemAPI.entityAttackCal`](http://doc.skillw.com/attsystem/-attribute-system/com.skillw.attsystem.api/-attribute-system-a-p-i/entity-attack-cal.html)

前者会解析战斗信息并发送，后者则不会
调用时会运行**机制组**，返回的是**运行结果**(伤害)
之后需要你手动伤害实体（如果机制里有你写的给予伤害就不用）

例:

> JavaScript

```javascript
const result = AttributeSystemAPI.playerAttackCal(
  "test-fight",
  attacker,
  defender,
  function (data) {
    //初始化战斗数据
  }
);
//跳过下次伤害时普攻机制组的运行(因为你想要触发的机制组已经运行过了)
AttributeSystemAPI.skipNextDamageCal();
//造成伤害，如果你是异步，那么记得要同步调用
//同步调用: task(function(t){defender.damage(result,attacker)})
defender.damage(result, attacker);
```

或

> Kotlin

```kotlin
val result = AttributeSystem.attributeSystemAPI.playerAttackCal(
  "test-fight",
  attacker,
  defender
){
    //初始化战斗数据
  }
//跳过下次伤害时普攻机制组的运行(因为你想要触发的机制组已经运行过了)
AttributeSystem.attributeSystemAPI.skipNextDamageCal();
//造成伤害，如果你是异步，那么记得要同步调用
defender.damage(result, attacker);
```
