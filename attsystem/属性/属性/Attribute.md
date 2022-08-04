# 属性

## 介绍

### 标识符

**属性**本身只是一个**标识符**，用来存取相应的属性数据

<!-- 例:

有一个 名(key)为 `PhysicalDamage` 的属性，

存：属性数据会以 `PhysicalDamage` 为键来存储

取：属性数据要通过 `PhysicalDamage` 来读取

> 就是**映射(mapping)**啦，高中必修一的概念 一个 key 对应一个属性数据 -->

### 功能实现

不同于其它属性插件，**AttributeSystem** 中一个属性 与 其功能的实现 是 **完完全全分开的**

- **读取**&**记录** 通过 **ReadPattern 读取格式** 实现
- 属性具体功能的**实现** 通过 **原版属性公式 / **机制组公式**(战斗公式)** / **脚本监听器** / **机制** / **代码** 实现

## 自定义属性

于 **plugins/AttributeSystem/attributes** 文件夹下任意一个**YAML 文件**中声明你的属性即可

```yaml
MyFirstAttribute:
  #权重
  priority: 100
  #默认为true 是否计入实体属性
  include-entity: true
  #名称
  names:
    - "第一个属性"
    - "第一个属性啊吧吧吧"
  #读取组
  read-pattern: Default
MySecondAttribute:
  priority: 100
  oriented: entity
  names:
    - "第II个属性"
    - "第二个属性啊吧吧吧"
  read-pattern: Default
```

接下来由我将属性的声明逐一拆解进行讲解.

## 键 [key]

属性的唯一标识符，用来存取属性数据
读取 NBT 属性时会通过它来读取

```yaml
ATTRIBUTE_DATA:
  example_data:
    MyFirstAttribute:
      value: 100
```

### 权重 [priority]

用来决定与其它属性间的读取顺序，
如果你在用诸如 **AttributePlus** 类的**属性插件**，
大概会遇到下面这个问题:
当一个属性名为 `伤害`
另一个属性名为 `暴击伤害`
**属性**在读取时会一律把含 `暴击伤害` 的词条读为了 `伤害` 属性，而忽略了 `暴击伤害`
**AttributeSystem** 通过权重解决这一问题

> 一个属性的权重值越小 读取顺序越靠前

```yaml
Crit:
  priority: 2
  names:
    - "暴击"
  read-pattern: Percent
CritDamage:
  priority: 1
  names:
    - "暴击伤害"
  read-pattern: Percent
```

以上配置便能完美地解决读取问题,这也是权重的作用

### 计入实体 [include-entity]

- **true** 会计入实体属性，并能够通过实体占位符获取 (`%as_att:属性id_占位符id%`)
- **false** 不会计入实体属性，能通过物品占位符获取 (`%as_equipment:装备组id_装备id_属性名_占位符id%`)

### 名称 [names]

将会以`<name>`为键带入读取格式，与文本进行匹配

### 读取格式 [read-pattern]

与一个读取格式绑定，读取格式是用来定义属性是如何读取的

<!--
## 声明 (开发者)

构造 [com.skillw.attsystem.api.attribute.Attribute](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/attribute/Attribute.html) 的子类 /   [com.skillw.attsystem.api.attribute.ConfigAttribute](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/attribute/ConfigAttribute.html) 的实例，并调用 **Attribute#register** 以完成注册 -->
