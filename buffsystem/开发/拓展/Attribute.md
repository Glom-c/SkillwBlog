# 兼容属性插件

**JavaScript** 请自力更生

> Kotlin

```kotlin
@AutoRegister("com.skillw.attsystem.api.AttrAPI")
object AttributeSystemHook : AttributeProvider {
    override val key: String = "AttributeSystem"
    override fun addAttribute(entity: LivingEntity, key: String, attributes: List<String>) {
        entity.addAttribute(key,attributes,false)
    }

    override fun removeAttribute(entity: LivingEntity, key: String) {
        entity.removeAttribute(key)
    }
}
```
