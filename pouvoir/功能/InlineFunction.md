# 字符串内联函数

自`1.4.2`后,重构为类似**kether**的**动作系统**

## 为什么不用 kether?

- 性能
- 脚本拓展

## 用法

```
函数名1 参数1 参数2 函数名2 参数1 参数2
```

你可以像这样换行

```
函数名1 参数1 参数2
函数名2 参数1 参数2
```

最后一个函数的返回值就是整段内联函数的返回值

## 字符串

```
'我是 一段 字符串'
```

## 字符串内联

```yaml
calculate '{if check 1 > 2 then 1 else 2} * 2 '
```

将**函数**包在`{}`之间即可
一段文本的内联函数共享一个上下文(变量池)

## 提供了哪些函数?

见下节 [函数列表](Functions.md)

## 拓展

```javascript
var Coerce = static("Coerce");

//@Function(abs)
function example(reader, context) {
  var number = reader.parseDouble(context);
  if (number == null) return null;
  return abs(number);
}
```

亦或者

```kotlin
@AutoRegister
object Abs : PouFunction<Double>("abs") {
    override fun execute(reader: IReader, context: Context): Double? {
        val number = reader.parseDouble(context) ?: return null
        return abs(number)
    }
}
```

使用:

```kotlin
 println("abs(-1)".parse())
```

打印: 1
