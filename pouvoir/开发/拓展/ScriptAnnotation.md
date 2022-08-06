# 脚本注解

需要用到 [`ScriptAnnotationData`](http://doc.skillw.com/pouvoir/-pouvoir/com.skillw.pouvoir.api.script.annotation/-script-annotation-data/index.html)

```kotlin
object : ScriptAnnotation(key) {
    override fun handle(data: ScriptAnnotationData) {
        //code
    }
}.register()
```

或

```javascript
//@Annotation
function exampleAnnotation(data) {
  //code
}
```
