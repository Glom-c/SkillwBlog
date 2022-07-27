# 单例模式

在程序运行中，保证某一个类，有且只有一个实例

## 饿汉式

```java
class LazyManSingle {
    private static final LazyManSingle INSTANCE = new LazyManSingle();

    private LazyManSingle(){

    }

    public static LazyManSingle getInstance() {
        return INSTANCE;
    }

}
```

缺点：

单例在类初始化时就实例化了，但客户可能不会用这个单例，就造成了资源的浪费。

解决办法即 懒汉式(Lazy) 或 内部静态类 或 枚举

## 懒汉式

```java
class LazyManSingle {
    private static LazyManSingle instance;

    private LazyManSingle(){

    }

    public static LazyManSingle getInstance() {
        if (instance == null) {
            instance = new LazyManSingle();
        }
        return instance;
    }
}
```

缺点：

不是线程安全的

如果有个客户多线程调用，那就会寄

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            new Thread(() -> {
                LazyManSingle single = LazyManSingle.getInstance();
                single.print();
            }).start();
        }
    }
}

class LazyManSingle {
    private static LazyManSingle instance;

    private LazyManSingle(){

    }

    public static LazyManSingle getInstance() {
        if (instance == null) {
            instance = new LazyManSingle();
            System.out.println("Construct!");
        }
        return instance;
    }

    public void print() {
        System.out.println(this.hashCode());
    }
}
```

运行结果如下：

```
Construct!
2069791201
2069791201
2069791201
2069791201
Construct!
2069791201
2069791201
2069791201
2069791201
Construct!
2069791201
2069791201
进程已结束。
```

可以发现，虽然拿到的单例都是同一个，但程序运行过程中实例化了 3 次，浪费了内存。

所以为了防止有客户这样做，我们应该写线程安全的懒汉式单例

## 线程安全的懒汉式

即用即造，造完之后直接用

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            new Thread(() -> {
                LazyManSingle single = LazyManSingle.getInstance();
                single.print();
            }).start();
        }
    }
}

class LazyManSingle {
    private static volatile LazyManSingle instance;

    private LazyManSingle(){

    }

    public static LazyManSingle getInstance() {
        if (instance == null) {
            synchronized (LazyManSingle.class) {
                if (instance == null) {
                    instance = new LazyManSingle();
                    System.out.println("Construct!");
                }
            }
        }
        return instance;
    }

    public void print() {
        System.out.println(this.hashCode());
    }
}
```

使用同步锁：防止多个线程同时执行

双重判断：让在赋值后的线程直接返回，而不是进锁

volatile：避免[指令重排](https://baijiahao.baidu.com/s?id=1701616903992143186&wfr=spider&for=pc)

运行结果如下：

```
Construct!
2069791201
2069791201
2069791201
2069791201
2069791201
2069791201
2069791201
2069791201
2069791201
2069791201
```

如此这般，我们便得到了一个 线程安全的懒汉式单例

此外，还有一种方法实现单例，即内部静态类

## 内部静态类

也可以实现懒加载

```java
public class Main {
    public static void main(String[] args) {
        LazyManSingle single = LazyManSingle.getSingle();
        single.print();
    }
}

class LazyManSingle {
    public static LazyManSingle getSingle() {
      //执行这一行时才会实例化
        return Inner.single;
    }

    private LazyManSingle(){

    }

    public void print() {
        System.out.println(this.hashCode());
    }

    public static class Inner {
        private static final LazyManSingle single = new LazyManSingle();
    }
}
```

但是！由于 java 中有反射 API 这种变态的存在，以上所有的私有构造方法在反射面前都是毛毛雨。

```java
Constructor<?> constructor = LazyManSingle.class.getDeclaredConstructors()[0];
constructor.setAccessible(true);
Object o = constructor.newInstance();
```

可谓防君子不防小人，所以我们要用到 枚举式

## 枚举式

```java
public enum LazyManSingle {
    INSTANCE;
    public void print(){
        System.out.println(this.hashCode());
    }
}
```

## 总结

饿汉式：如果一定会用这个单例，就用饿汉式

懒汉式： 单线程应用

线程安全的懒汉式：多线程应用

枚举式：仅限 java，完美解决
