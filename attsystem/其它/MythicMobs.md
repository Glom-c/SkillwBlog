# MythicMobs

## MM 技能

让**MM 技能伤害**支持 AS 的**战斗机制组**

```yaml
Skills:
  - att-damage{key="战斗机制组id"} @Target
```

## MM 怪属性

让**MM 怪**拥有 AS 的**属性**

```yaml
SkeletalKnight:
  Type: WITHER_SKELETON
  Display: "&aSkeletal Knight"
  Health: 40
  Damage: 8
  Equipment:
    - IRON_HELMET HEAD
    - IRON_CHESTPLATE CHEST
    - IRON_LEGGINGS LEGS
    - IRON_BOOTS FEET
    - IRON_SWORD HAND
    - SHIELD OFFHAND
  Drops:
    - GOLD_NUGGET{display="Gold Coin"} 1to2 0.5
  LevelModifiers:
    - health 5
    - damage 0.5
  Attributes:
    #同样支持条件 乃至单行条件
    - "Lv.100"
    - "移动速度: 100"
#  Options:
#这里的原版属性不能和AS的属性冲突 所以注释掉了
#   MovementSpeed: 0.1
```

配置下加 **Attributes** 节点即可
