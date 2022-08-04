# AttributeSystem

## 1.0.0 2022 年 2 月 20 日

插件发布

## 1.0.1 2022 年 2 月 20 日

更新了 Book 式的属性统计

## 1.0.2 2022 年 2 月 21 日

兼容了 DragonCore 的装备栏，key 为 Dragon-Core
支持了原版属性开关，将 formula 中的值设为-1 即可关闭

## 1.0.3 2022 年 2 月 21 日

更好地兼容了 DragonCore 的装备栏，key 为 Dragon-Core 子 key 为槽位 id (将槽位 attribute 设为 true 即可)

## 1.0.4 2022 年 2 月 21 日

兼容了萌芽的装备栏，key 为 Germ-Equipment 子 key 为槽位 id (AS 配置 slot.yml 中 germ-slots 节点下添加槽位)

## 1.0.5 2022 年 2 月 23 日

更好地兼容了萌芽&龙核的装备栏
兼容了部分 AP2/3 附属 (请把那些附属 jar 包内的 plugin.yml 中 AttributePlus 改为 AttributeSystem 方可正常使用)
兼容/修复了龙时的 RGB 颜色读不到属性的问题
修复了 PAPI 变量标识符为"asys"的问题(现在改为"as")
修改了读取组的默认配置(旧版的 placeholder valueMax 的值笔误成了 valueMin)
使恢复全息在恢复值为 0 时不显示

## 1.0.6 2022 年 2 月 24 日

添加了针对物品的条件（见配置）
兼容了 SKAPI 技能冷却 与 skill-speed 挂钩（请更新 formula.yml）
优化了龙核的装备栏兼容

## 1.0.7 2022 年 2 月 25 日

添加了针对多行字符串的条件（详见配置）
添加了 bstats 统计
兼容了 MM 怪属性，在怪物配置下加节点"Attributes"

## 1.0.8 2022 年 2 月 26 日

修改条件配置(原配置转义错误)
优化 API

## 1.0.9 2022 年 2 月 26 日

优化 API 添加了条件解析事件

## 1.1.0 2022 年 3 月 6 日

添加了战斗状态
添加了标签系统(基于属性)
修复了高精度数字显示
兼容了 mod 物品
重构了条件系统
将公式配置移动至单独文件
删除了对 NBT 属性的支持
删除了信息栏系统

## 1.1.1 2022 年 3 月 6 日

修复了部分信息显示错误的 bug
生命恢复可关闭(formula 里设为-1)

## 1.1.2 2022 年 3 月 11 日

修改变量获取失败时返回值 "N/A" -> "0.0"
修复 mod 物品材质报错问题
再兼容了物品的 NBT 属性数据的序列化与反序列化
新增指令 itemstats 查看装备栏内任意槽位的装备属性统计
新增变量 %as*formulastr*公式 id% 返回 公式的原始字符串
新增读取组数乘模式的读取变量
修改最大生命值属性添加方式 -> 已兼容其它插件/mod
修复了可能会内存泄漏的问题 （快用 paper）

## 1.1.3 2022 年 3 月 12 日

修复了可能会读到空气装备的情况（）
添加了捕获组运算符 （*无*敌\*）
添加了指令 entitystats 查看实体属性统计

## 1.1.4 2022 年 3 月 20 日

修复了 1.12 不存在 getLore 方法问题
兼容了 1.18
添加了 debug

## 1.1.5 2022 年 3 月 21 日

修复了读取组捕获组 id 报错
更好地兼容了 1.18
属性统计可自定义
优化用户体验

## 1.1.6 2022 年 3 月 22 日

修复抛射物伤害 MISS 问题
兼容 CrashShot (options.fight.skip-crash-shot 为是否跳过伤害计算)

## 1.2.0 2022 年 4 月 4 日

分开三个模块，重构部分代码并开源
此版之后支持字符串属性（开发者）

## 1.2.1 2022 年 5 月 8 日

合并三个模块，优化代码

## 1.2.2 2022 年 6 月 12 日

修复 personal 指令不管用 bug
修复怪物属性 重载时会刷新
修复条件不起效果 bug
兼容 Pouvoir 1.3.0

## 1.2.3 2022 年 6 月 21 日

新增几个简写函数
AttributeDataCompound#getAttributeStatus(String) -> AttributeDataCompound#getStatus(String)
AttributeDataCompound#getAttributeStatus(Attribute) -> AttributeDataCompound#getStatus(Attribute)

## 1.2.3-fix 2022 年 6 月 22 日

kotlin 版本退到 1610

## 1.2.4 2022 年 6 月 26 日

增加生命恢复事件（我怎么妄加了）
增加 config 中 disable-regain-on-fight 是否在战斗中暂停生命恢复

## 1.3.0 2022 年 7 月 15 日

优化战斗系统（快的一批）
优化调度器系统
增加指令 report / clear 用来 查看 /清除 耗时数据
兼容 MythicMobs 5 & MythicMobs 4 技能伤害公式 （机制 att-damage{key="战斗组 id"}）
不再兼容 OriginSkill (会做 Planners 兼容)
删除 TriggerManager TriggerHolderManager
修复了卸载 AS 攻击速度异常 （详细修复见 FAQ）
更优雅的代码（）
API 变动，具体看 javadoc

## 1.3.1 2022 年 7 月 25 日

## 新增

物品 NBT 属性条件

禁攻材质权限 (as.damage_type.{小写材质 id})
更多的 Status ( NormalStatus(String to Any) ， StringStatus(String to String) )

支持 Planners Kether AttDamage 动作
支持 脚本注解注册 机制 条件 读取格式 Operation
支持 Kether 编辑判断流程(见 damage 与 fight)

FightDataHandleEvent
ItemNBTReadEvent

## 修复

'options.fight.damage-any-time' 不奏效
生命恢复时报错
MM 怪属性重载时刷新

## 1.3.2 2022 年 7 月 31 日

### 新增

不同权限攻击触发不同战斗组
指令 info 查看插件信息
指令 disable 用于卸载插件

### 优化

## 1.3.3 2022 年 8 月 4 日

用户体验

### 新增

MessageBuilderManager
你可以拓展伤害显示的方式了(来个大佬帮我写萌芽/龙核附属)

### 支持

Pouvoir 重构后的字符串内联函数 (性能很棒的说)

### 修复

禁普攻材质不起效
距离攻击不起效
