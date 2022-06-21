# 伤害类型

## 介绍

**AttributeSystem** 中，**伤害类型** 负责管理 **伤害显示**

## 声明

于 **plugins/Attributes/damage** 文件夹下任意一个**YAML文件**中声明

```yaml
#伤害类型id
Physical:
  #名称
  name: '物理伤害'
  #伤害显示
  display:
    #攻击者
    attack:
      holo: 'if({result},!=,0,if({crit},!=,0,&4✵ format({crit},#.##),&6format({damage},#.##)),&7&lMISS) if({vampire},!=,0,&a+format({vampire},#.##), )'
      chat: '&6{name}&5: if({result},!=,0,&dif({crit},!=,0,&4format({crit},#.##),&dformat({damage},#.##)),&7&lMISS) if({vampire},!=,0,&c吸血&aformat({vampire},#.##), )'
      title: 'if({crit},!=,0,&4暴击,null)'
      sub-title: 'if({result},!=,0,if({crit},!=,0,&4✵ format({crit},#.##),&6format({damage},#.##)),&7&lMISS)'
      action-bar: '&6{name}&5: if({result},!=,0,&dif({crit},!=,0,&4format({crit},#.##),&dformat({damage},#.##)),&7&lMISS) if({vampire},!=,0,&c吸血&aformat({vampire},#.##), )'
    #防御者
    defend:
      holo: 'if({result},!=,0,&c- if({crit},!=,0,&4✵ format({crit},#.##),&6format({damage},#.##)),&7&lMISS)'
      chat: '&6{name}&5: if({result},!=,0,&dif({crit},!=,0,&4format({crit},#.##),&dformat({damage},#.##)),&7&lMISS)'
      title: 'if({crit},!=,0,&4受到暴击,null)'
      sub-title: 'if({result},!=,&c- &6if({crit},!=,0,&4✵ format({crit},#.##),&6format({damage},#.##)),&7&lMISS)'
      action-bar: '&6{name}&5: if({result},!=,0,&dif({crit},!=,0,&4format({crit},#.##),&dformat({damage},#.##)),&7&lMISS)'
```

<br/>

这个真没什么好说的
