原文 http://www.kotlinlang.org/docs/reference/idioms.html

## 习惯语法
>(语法糖？)   

常用的kotlin习语，如果你有更好的语法习惯，可以提交pull request贡献出来。

### 创建DTO’s (POJO’s/POCO’s)
```kotlin
data class Customer(val name: String, val email: String)
```
`Customer` 默认提供了以下函数:   
&#151;  所有属性都具有 getter (var声明的还有setter) 方法   
&#151;  `equals()`   
&#151;  `hashCode()`   
&#151;  `toString()`   
&#151;  `copy()`    
&#151;  `component1()` ,`component2()` 所有属性都有(详情 <a href="http://www.kotlinlang.org/docs/reference/data-classes.html" target= "_blank">Data classes</a>)



### 函数的默认参数
```kotlin
fun foo(a: Int = 0, b: String = "") { ... }
```

### 过滤list集合:
```kotlin
val positives = list.filter { x -> x > 0 }
```
或者更简短的:
```kotlin
val positives = list.filter { it > 0 }
```


### String 插入
```kotlin
println("Name $name")
```


### 类型检查
```kotlin
when (x) {
    is Foo -> ...
    is Bar -> ...
    else   -> ...
}
```

### 遍历list/map键值对
```kotlin
val list =arrayListOf("a","b","c")
for (v in list) {
    println("$v")
}

val map=hashMapOf(Pair("a",1), Pair("b","cd"))
for ((k, v) in map) {
    println("$k -> $v")
}
```
`k`,`v` 可以任意使用


### 使用 ranges
```kotlin
for (i in 1..100) { ... }
for (x in 2..10) { ... }
```

### 不可变 list
```kotlin
val list = listOf("a", "b", "c")
```


### 不可变 map
```kotlin
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
```


### 访问读取 map
```kotlin
println(map["key"])
map["key"] = value
```

### Lazy property
> 懒属性?

```kotlin
val p: String by lazy {
    // compute the string
}
```


### 扩展函数
```kotlin
fun String.spaceToCamelCase() { ... }

"Convert this to camelcase".spaceToCamelCase()
```


### 创建单例
> 常量

```kotlin
object Resource {
    val name = "Name"
}
println(Resource.name)
```

### 安全调用对象
```kotlin
val files = File("Test").listFiles()

println(files?.size) //如果files为null也不会抛出异常
```

### 为null时else块
```kotlin
val files = File("Test").listFiles()

println(files?.size ?: "empty")
```

### 如果为null的执行
```kotlin
val data = ...
val email = data["email"] ?: throw IllegalStateException("Email is missing!")
```

### 执行不为null的代码块
```kotlin
val data = ...

data?.let {
    ... // 如果不为null会执行这里的代码
}
```

### 返回when声明
```kotlin
fun transform(color: String): Int {
    return when (color) {
        "Red" -> 0
        "Green" -> 1
        "Blue" -> 2
        else -> throw IllegalArgumentException("Invalid color param value")
    }
}
```

### ‘try/catch’ 块
```kotlin
fun test() {
    val result = try {
        count()
    } catch (e: ArithmeticException) {
        throw IllegalStateException(e)
    }

    // Working with result
}
```

### if 表达式
```kotlin
fun foo(param: Int) {
    val result = if (param == 1) {
        "one"
    } else if (param == 2) {
        "two"
    } else {
        "three"
    }
}
```

### 返回方法生成器
```kotlin
fun arrayOfMinusOnes(size: Int): IntArray {
    return IntArray(size).apply { fill(-1) }
}
```

### 单个的函数返回值表达式
```kotlin
fun theAnswer() = 42
```
这相当于:
```kotlin
fun theAnswer(): Int {
    return 42
}
```
这可以与其它特有语法有效地结合起来，从而使用更简短的代码。例如使用`when` 表达式:
```kotlin
fun transform(color: String): Int = when (color) {
    "Red" -> 0
    "Green" -> 1
    "Blue" -> 2
    else -> throw IllegalArgumentException("Invalid color param value")
}
```


### 使用`wich`串联调用对象的多个方法
```kotlin
class Turtle {
    fun penDown()
    fun penUp()
    fun turn(degrees: Double)
    fun forward(pixels: Double)
}

val myTurtle = Turtle()
with(myTurtle) { //draw a 100 pix square
    penDown()
    for(i in 1..4) {
        forward(100.0)
        turn(90.0)
    }
    penUp()
}
```

Java 7 的`try` 块自动释放资源
```kotlin
val stream = Files.newInputStream(Paths.get("/some/file.txt"))
stream.buffered().reader().use { reader ->
    println(reader.readText())
}
```
