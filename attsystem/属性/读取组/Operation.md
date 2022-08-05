# 运算操作

## 默认

**AttributeSystem** 默认提供了

- **Max** 取最大值
- **Min** 取最小值
- **Plus** 做加法
- **Reduce** 做减法
- **Scalar** 做乘法
  共 5 种**运算操作**，如果不够，你可以通过编写脚本/代码拓展

## 拓展

```javascript
//@Operation(my_operation)
function example(a, b) {
  //↑接收参数a ,b （是数字）
  //↓返回a^b
  return a ^ b;
}
```

```kotlin
@AutoRegister
object MyOperation : BaseOperation("my_operation") {
    override fun operate(a: Number, b: Number): Number {
        return a.toDouble().pow(b.toDouble())
    }
}
```
