# 读取格式拓展

##

```kotlin
@AutoRegister
object MyReadPattern : ReadPattern("my_read_pattern") {
    override fun read(string: String, attribute: Attribute, entity: LivingEntity?, slot: String?): Status? {
        //code
    }

    override fun readNBT(map: Map<String, Any>, attribute: Attribute): Status? {
        //code
    }

    override fun placeholder(key: String, attribute: Attribute, status: Status, entity: LivingEntity?): Any? {
        //code
    }

    override fun stat(attribute: Attribute, status: Status, entity: LivingEntity?): TellrawJson {
        //code
    }
}
```

## JavaScript

```javascript
//@ReadPattern(my_read_pattern)

function read(string, attribute, entity, slot) {
  //code
}

function readNBT(map, attribute) {
  //code
}

function placeholder(key, attribute, status, entity) {
  //code
}

function stat(attribute, status, entity) {
  //code
}
```

## 用法

在**属性声明处**指定**读取格式**

> YAML

```yaml
ExampleAttr:
  priority: 100
  include-entity: true
  names:
    - "示例属性"
  #读取格式
  read-pattern: my_read_pattern
```

或

> JavaScript

```javascript
//@Awake(Active)
function regAtt() {
  var Attribute = find("com.skillw.attsystem.api.attribute.Attribute");
  var ReadPattern = AttributeSystem.readPatternManager.get("my_read_pattern");

  Attribute.createAttribute("example", ReadPattern, (builder) => {
    builder.names.add("示例属性");
  }).register();
}
```

或

> Kotlin

```kotlin
val ReadPattern = AttributeSystem.readPatternManager["my_read_pattern"]
Attribute.createAttribute("example", ReadPattern) {
    names += "示例属性"
}.register()
```
