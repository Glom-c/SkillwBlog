# 效果类型

**BuffSystem**默认提供了 **3** 种**效果类型**

- attribute **属性**
- potion **原版药水**
- permissions **权限**

你可以通过编写 **脚本**/**代码** 拓展效果类型

## 拓展

需要用到 [`BuffData`](http://doc.skillw.com/buffsystem/-buff-system/com.skillw.buffsystem.api.data/-buff-data/index.html)

> JavaScript

```javascript
//@EffectType(attribute)
//文件注解顶头写

function getSource(data, sourceKey) {
  if (!data.containsKey(sourceKey))
    data.put(sourceKey, "${data.buffKey}:$key:${UUID.randomUUID()}");
  return data.get(sourceKey);
}

function getAttrProvider() {
  const attrProvider = static("BuffSystem").attributeManager.attrProvider;
  if (attrProvider == null) {
    warning("No attribute plugin!");
    return null;
  }
  return attrProvider;
}

function realize(entity, data, section) {
  //实现效果
  if (!section.contains("attributes")) return;
  const key = section.name;
  const sourceKey = "attribute-effect-" + key + "-source";
  const source = getSource(data, sourceKey);
  const attrProvider = getAttrProvider();
  const attributes = data
    .replace(section.get("attributes"))
    .stream()
    .map(function (it) {
      placeholder([it, entity]);
    });
  attrProvider.addAttribute(entity, source, attributes);
}

function unrealize(entity, data, section) {
  //消除效果
  const key = section.name;
  const sourceKey = "attribute-effect-" + key + "-source";
  const source = getSource(data, sourceKey);
  const attrProvider = getAttrProvider();
  attrProvider.removeAttribute(entity, source);
}
```

> Kotlin

```kotlin
class AttributeEffect(override val key: String, val attributes: List<String>) : BaseEffect(),
    ConfigurationSerializable {

    //Key to get the source from BuffMemory
    private val sourceKey = "attribute-effect-$key-source"

    private fun getSource(data: BuffData): String {
        if (!data.containsKey(sourceKey))
            data[sourceKey] = "${data.buffKey}:$key:${UUID.randomUUID()}"
        return data.getAs<String>(sourceKey).toString()
    }

    override fun realize(entity: LivingEntity, data: BuffData) {
        var attributes = data.replace(this.attributes)
        if (entity is Player) {
            attributes = attributes.map { it.replacePlaceholder(entity) }
        }
        attributes = attributes.map { it.placeholder(entity) }
        attrProvider.addAttribute(entity, getSource(data), attributes)
    }

    override fun unrealize(entity: LivingEntity, data: BuffData) {
        attrProvider.removeAttribute(entity, getSource(data))
    }

    companion object {

        @JvmStatic
        fun deserialize(section: ConfigurationSection): AttributeEffect? {
            try {
                val key = section.name
                if (section["type"].toString().lowercase() != "attribute") return null
                val attributes = section.getStringList("attributes")
                return AttributeEffect(key, attributes).apply { config = true }
            } catch (e: Exception) {
                e.printStackTrace()
            }
            return null
        }

        @SubscribeEvent
        fun load(event: EffectLoadEvent) {
            event.result = deserialize(event.section) ?: return
        }
    }


    override fun serialize(): MutableMap<String, Any> {
        return linkedMapOf("type" to "attribute", "attributes" to attributes)
    }
}
```

## 使用

```yaml
#效果key
example-attribute:
  #效果类型
  type: attribute
  attributes:
  #             字符串内联函数
    - '移动速度: {calculate '1000+100 * {level}'}'
```
