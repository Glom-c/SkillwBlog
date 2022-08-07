# 条件

## 介绍

**AttributeSystem** 中 **条件** 负责控制 一组/一行字符串 中的**属性读取与否**

## 使用

请看上一节 [条件用法](https://blog.skillw.com/#sort=attsystem&doc=%E8%A3%85%E5%A4%87%E6%A0%8F%E7%B3%BB%E7%BB%9F/%E6%9D%A1%E4%BB%B6/ConditionUsage.md)

## 声明

```javascript
var Coere = static("Coere");

//@Condition(Level,ALL,Lv\.(?<value>\d+),等级限制: (?<value>\d+))
function level(slot, entity, matcher, text) {
  var hasEntity = entity != "null";
  if (!hasEntity) return true;
  if (!(entity instanceof Player)) {
    return true;
  }
  var level = Coerce.toInteger(matcher.group("value"));
  return entity.level >= level;
}
```

或

```kotlin
@AutoRegister
object LevelCondition : BaseCondition("level", setOf("Lv\\.(?<value>\\d+)", "等级限制: (?<value>\\d+)"), ConditionType.ALL) {
    override fun condition(slot: String?, entity: LivingEntity?, matcher: Matcher, text: String): Boolean {
        entity ?: return true
        if (entity !is Player) return true
        val level = Coerce.toInteger(matcher.group("value"))
        return entity.level >= level
    }
}
```
