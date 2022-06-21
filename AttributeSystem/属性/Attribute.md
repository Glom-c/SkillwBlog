# 属性

## 介绍

### 标识符

**属性**本身只是一个**标识符**，用来存取相应的属性数据

例:

有一个 名(key)为 `PhysicalDamage` 的属性，有名

存：属性数据会以 `PhysicalDamage` 为键来存储

取：属性数据要通过 `PhysicalDamage` 来读取

> 就是**映射(mapping)**啦，高中必修一的概念 一个key对应一个属性数据

### 功能实现

不同于其它属性插件，一个属性 与 其功能的实现 是 **完完全全分开的**

- **读取**&**记录** 通过  **ReadPattern 读取格式** 实现
- 属性具体功能的**实现** 通过  **原版属性公式  / **机制组公式**(战斗公式)** / **脚本监听器** / **机制** / **代码**  实现

 [功能实现](http://blog.skillw.com/#sort=attributesystem&doc=属性/Realise.md) 会涉及到，慢慢看吧。

## 声明 (用户)

于 **plugins/AttributeSystem/attributes** 文件夹下任意一个**YAML文件**中声明

```yaml
MyFirstAttribute:
  #权重
  priority: 100
  #可选:                       entity / item  /  all
  #针对                         实体     物品    都针对
  #是否会计算到实体属性上           是      否       是
  #注：一般只用到实体属性， 物品属性会用在特定武器特定属性上，比如说 价值
  oriented: entity
  #名称
  names:
    - '第一个属性'
    - '第一个属性啊吧吧吧'
  #读取组
  read-group: Default
```

## 声明 (开发者)

构造 [com.skillw.attsystem.api.attribute.Attribute](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/attribute/Attribute.html) 的子类 /   [com.skillw.attsystem.api.attribute.ConfigAttribute](http://book.skillw.com/attrsystem/doc/com/skillw/attsystem/api/attribute/ConfigAttribute.html) 的实例，并调用 **Attribute#register** 以完成注册
