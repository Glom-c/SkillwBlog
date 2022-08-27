# 拓展物品元

拓展的物品元与普通物品元的使用无异

需要用到 [Memory](https://doc.skillw.com/itemsystem/com/skillw/itemsystem/api/meta/data/Memory.html)

## JavaScript

```javascript
//@Meta(custom-meta)
function customMeta(memory) {
  //获取str参数
  const str = memory.getString("str");
  memory.builder.lore.add("来自CustomMeta: " + str);
}
```

## Kotlin

你可以去[**Github**](https://github.com/Glom-c/ItemSystem)借鉴源码

```kotlin
@AutoRegister
object MetaDamage : BaseMeta("damage") {

    override fun invoke(memory: Memory) {
        with(memory) {
            builder.damage = getInt("damage")
        }
    }

    override fun loadData(data: ItemData): Any {
        data.itemTag.remove("Damage")
        return data.builder.damage
    }

}
```
