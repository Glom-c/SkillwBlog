# 伤害类型

## 介绍

**AttributeSystem** 中，**伤害类型** 负责管理 **伤害显示**

## 声明

于 **plugins/AttributeSystem/damage** 文件夹下任意一个**YAML 文件**中声明

```yaml
#伤害类型id
Physical:
  #名称
  name: "物理伤害"
  #伤害显示
  display:
    #攻击者
    attack:
      ##下面是字符串内联函数（非常像kether）
      holo: |-
        set common to if check {result} != 0.0 then '&6{ format {result} #.## }' else '&7&lMISS'
        set crit to if check {crit} != 0.0 then '&4✵' else pass
        set vampire to if check {vampire} != 0.0 then '&a+{ format {vampire} #.## }' else pass
        join [ &crit &common &vampire ] by ''
      chat: |-
        set prefix to '&6{name}&5: '
        set common to if check {result} != 0.0 then '&d{ format {result} #.## }' else '&7&lMISS'
        set crit to if check {crit} != 0.0 then '&4✵' else pass
        set vampire to if check {vampire} != 0.0 then '&a+{ format {vampire} #.## }' else pass
        join [ &prefix &crit &common &vampire ] by ''
      title: |-
        if check {crit} != 0.0 then '&4暴击' else '&4'
      sub-title: |-
        set common to if check {result} != 0.0 then '&6{ format {result} #.## }' else '&7&lMISS'
        set vampire to if check {vampire} != 0.0 then '&a+{ format {vampire} #.## }' else pass
        join [ &common &vampire ] by ''
      action-bar: |-
        set prefix to '&6{name}&5: '
        set common to if check {result} != 0.0 then '&6{ format {result} #.## }' else '&7&lMISS'
        set crit to if check {crit} != 0.0 then '&4✵' else pass
        set vampire to if check {vampire} != 0.0 then '&c吸血&a{ format {vampire} #.## }' else pass
        join [ &prefix &crit &common &vampire ] by ''
    defend:
      holo: |-
        set subtract to '&c- '
        set common to if check {result} != 0 then '&6{format {result} #.##}' else '&7&lMISS'
        set crit to if check {crit} != 0.0 then '&4✵' else pass
        join [ &subtract &crit &common ] by ''
      chat: |-
        set prefix to '&6{name}&5: '
        set common to if check {result} != 0 then '&6{format {result} #.##}' else '&7&lMISS'
        set crit to if check {crit} != 0.0 then '&4✵' else pass
        join [ &prefix &crit &common ] by ''
      title: |-
        if check then {crit} != 0 '&4受到暴击' else '&4'
      sub-title: |-
        set crit to if check {crit} != 0.0 then '&c-&4✵ ' else '&c- '
        set common to if check {result} != 0.0 then '&6{ format {result} #.## }' else '&7&lMISS'
        join [ &crit &common ] by ''
      action-bar: |-
        set prefix to '&6{name}&5: '
        set common to if check {result} != 0.0 then '&6{ format {result} #.## }' else '&7&lMISS'
        set crit to if check {crit} != 0.0 then '&4✵' else pass
        join [ &prefix &crit &common ] by ''
```

你可以通过以下方法使用`kether`

```yaml
Physical:
  name: "物理伤害"
  display:
    attack:
      holo: |-
        kether::
        set common to if check {result} != 0.0 then '&6{ format {result} #.## }' else '&7&lMISS'
        set crit to if check {crit} != 0.0 then '&4✵' else pass
        set vampire to if check {vampire} != 0.0 then '&a+{ format {vampire} #.## }' else pass
        join [ &crit &common &vampire ] by ''
```

> 字符串内联函数和 kether 非常像，这是开发者为了兼容而专门设计的
> 字符串内联函数的性能较高 （但是功能较少）
