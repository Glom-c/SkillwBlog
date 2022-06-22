# 条件

## 介绍

**AttributeSystem** 中 **条件** 负责控制 一组/一行字符串 中的**属性读取与否**

## 使用

#### 单行

> 这里的 / 与 , 均可在config中配置

> 攻击力: 100/Lv.10,职业限制: 战士

若实体等级未到10 或 职业不是战士

就不会读取**此行**属性

#### 多行

> Lv.100
> 
> 攻击力: 100
> 
> 生命值: 1000

若实体等级未到100

就不会读取**这些**属性

## 声明(用户)

于 **plugins/Attributes/conditions** 文件夹下任意一个**YAML文件**中声明

```yaml
#id
test-level:
  # line / strings / all
  type: all
  #名称
  names:
    - 'Lv\.(?<value>\d+)'
    - '等级限制: (?<value>\d+)'
  #脚本
  #可填 js / groovy / 脚本路径::函数名(单行)
  #变量:     entity : LivingEntity?,     text : String,      name : String
  #含义:          实体                      本行文本             名称
  #返回值为 Boolean ， 是否读取此行属性
  #condition中的level函数
  script: 'condition.js::level'
```

> AttributeSystem/scripts/condition.js

```javascript
function level() {
    var hasEntity = entity != "null"
    if (!hasEntity) return true
    if (!(entity instanceof Player)) {
        return true
    }
    var level = Coerce.toInteger(matcher.group("value"))
    return entity.level >= level
}
```

## 声明(开发者)

### JavaScript / Groovy

```groovy
//@Condition(class,all,职业限制: (<?classes.*>))
def clazz() {
    def hasEntity = entity != "null"
    if (!hasEntity) return true
    if (!(entity instanceof Player)) return true
    def classes = matcher.group("classes").replace(" ", "").split("/")
    if (classes.length == 0) return true
    def stream = Arrays.stream(classes)
    def isSkillAPI = ASConfig.INSTANCE.getSkillAPI()
    if (isSkillAPI) {
        var SkillAPI = ScriptTool.staticClass("com.sucy.skill.SkillAPI")
        return stream.anyMatch { SkillAPI.getPlayerData(entity).isClass(SkillAPI.getClass(it)) }
    } else {
        return stream.anyMatch { entity.hasPermission("as.class.$it") }
    }
}
```

通过注解注册 js同理

### Java/Kotlin

编写[com.skillw.attsystem.api.condition.Condition](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/condition/Condition.html) 的实例，并调用 **Condition#register** 以完成注册

> Kotlin

```kotlin
object : Condition("test",setOf("Test: <?value.*>"),Condition.ConditionType.ALL){
  override fun condition(livingEntity: LivingEntity?, matcher: Matcher, text: String): Boolean{
    return matcher.group("value") == "test"
  }
}.register()
```

Java同理
