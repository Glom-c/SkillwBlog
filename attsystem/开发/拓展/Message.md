# 战斗信息显示方式

```kotlin
@AutoRegister
object ExampleMessageBuilder : MessageBuilder {

    override val key: String = "example"

    override fun register() {
        AttributeSystem.messageBuilderManager.attack.register(this)
        AttributeSystem.messageBuilderManager.defend.register(this)
    }

    override fun build(damageType: DamageType, fightData: FightData, first: Boolean, type: Message.Type): Message {
        //这里要返回你的Message实现类
    }
}

```
