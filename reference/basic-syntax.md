原文 https://kotlinlang.org/docs/reference/basic-syntax.html

##基本语法


### 声明包名
包名应该在源文件顶部
```java
package my.demo

import java.util.*

// ...
```
包名不要求和必须和文件夹相同的目录，比如一个kotlin源文件路径为src/main/java/com/demo/test.kt，那么包名可以是`com.demo.test1` 也可以是任意其他的，这点和java不同，java包名必须和代码相对目录相同。
详情 <a href="https://kotlinlang.org/docs/reference/packages.html" target= "_blank">Packages</a>。

### 定义函数
下面这个函数有2个`Int`类型的参数和`Int`类型的返回值:
```kotlin
fun sum(a: Int, b: Int): Int {
  return a + b
}
```
函数表达式自动推断返回类型:
```kotlin
fun sum(a: Int, b: Int) = a + b
```
函数没有返回值(java语法里面的`void`方法):
```kotlin
fun printSum(a: Int, b: Int): Unit {
  print(a + b)
}
```
`Unit` 也返回类型可以省略:
```kotlin
public fun printSum(a: Int, b: Int) {
  print(a + b)
}
```
详情 <a href="https://kotlinlang.org/docs/reference/functions.html" target= "_blank">Functions</a>。


### 定义局部变量
赋值一次(只读，类似java语法中`final`修饰的变量)的变量:
```kotlin
val a: Int = 1
val b = 1   // 自动推断为 Int 类型
val c: Int  // 如果没有初始化需要提供类型
c = 1       // 明确的赋值
c = 2       // 会编译出错，val修饰的变量只能赋值一次!
```
可变变量:
```
var x = 5 
x += 1
```
详情 <a href="https://kotlinlang.org/docs/reference/properties.html" target= "_blank">Properties And Fields</a>。


### String 模板
```kotlin
fun main(args: Array<String>) {
  if (args.size() == 0) return

  print("First argument: ${args[0]}")
}
```
详情 <a href="https://kotlinlang.org/docs/reference/basic-types.html#string-templates" target= "_blank"> String templates</a>。

### 条件表达式
```kotlin
fun max(a: Int, b: Int): Int {
  if (a > b)
    return a
  else
    return b
}
```
使用`if` 表达式
```kotlin
fun max(a: Int, b: Int) = if (a > b) a else b
```
详情 <a href="https://kotlinlang.org/docs/reference/control-flow.html#if-expression" target= "_blank">if-expressions</a>。

### 使用null和检查null
一个引用必须明确可以为`null`时才有可能为`null`(如果没有明确声明可以为null，那么强行赋值为null会编译出错！)

如果不能转换成`Int` 可能返回`null`:
```kotlin
fun parseInt(str: String): Int? {
  // ...
}
```
调用可能返回`null`的函数:
```kotlin
fun main(args: Array<String>) {
  if (args.size() < 2) {
    print("Two integers expected")
    return
  }

  val x = parseInt(args[0])
  val y = parseInt(args[1])

  //输出 `x * y` 可能会抛出异常，因为x、y可能为null
  if (x != null && y != null) {
    //x和y都经过了非null检查
    print(x * y)
  }
}
```
或者
```kotlin
// ...
  if (x == null) {
    print("Wrong number format in '${args[0]}'")
    return
  }
  if (y == null) {
    print("Wrong number format in '${args[1]}'")
    return
  }

  // ...
  print(x * y)
```
详情 <a href="https://kotlinlang.org/docs/reference/null-safety.html" target= "_blank">Null-safety</a>。

### 类型检测和自动类型转换
`is` 关键字检测是否类型相同，如果要检测一个只读的局部变量或属性的特定类型，没有必要明确地强制转换:
```kotlin
fun getStringLength(obj: Any): Int? {
  if (obj is String) {
    // 在这个if范围内`obj` 自动转换为 `string` 类型
    return obj.length
  }

  // 在外面`obj` 还是`Any`类型
  return null
}
```
或者
```kotlin
fun getStringLength(obj: Any): Int? {
  if (obj !is String)
    return null

  // 这里 `obj` 自动转换成 `String` 类型
  return obj.length
}
```
甚至
```kotlin
fun getStringLength(obj: Any): Int? {
  // 在`&&`后面`obj` 将自动转换成 `String` 类型
  if (obj is String && obj.length > 0)
    return obj.length

  return null
}
```
详情 <a href="https://kotlinlang.org/docs/reference/classes.html" target= "_blank">Classes</a>和<a href="https://kotlinlang.org/docs/reference/typecasts.html" target= "_blank">Type casts</a>。


### for 循环
```kotlin
fun main(args: Array<String>) {
  for (arg in args)
    print(arg)
}
```
或者
```kotlin
for (i in args.indices)
  print(args[i])
```
详情 <a href="https://kotlinlang.org/docs/reference/control-flow.html#for-loops" target= "_blank">for loop</a>。


### while 循环
```kotlin
fun main(args: Array<String>) {
  var i = 0
  while (i < args.size())
    print(args[i++])
}
```
详情 <a href="https://kotlinlang.org/docs/reference/control-flow.html#while-loops" target= "_blank">while loop</a>。


### when 表达式
```kotlin
fun cases(obj: Any) {
  when (obj) {
    1          -> print("One")
    "Hello"    -> print("Greeting")
    is Long    -> print("Long")
    !is String -> print("Not a string")
    else       -> print("Unknown")
  }
}
```
详情 <a href="https://kotlinlang.org/docs/reference/control-flow.html#when-expression" target= "_blank">when expression</a>。


### ranges
检查一个数字在某个范围内使用`in` 操作符:
```kotlin
if (x in 1..y-1)
  print("OK")
```
检查一个数字不在某个范围内:
```kotlin
if (x !in 0..array.lastIndex)
  print("Out")
```
遍历ranges:
```kotlin
for (x in 1..5)
  print(x)
```
详情 <a href="https://kotlinlang.org/docs/reference/ranges.html" target= "_blank">Ranges</a>。


### 集合
遍历集合:
```kotlin
for (name in names)
  println(name)
```
检查集合里是否包含某个对象用`in` 操作符:
```kotlin
if (text in names) // 和names.contains(text)一样
  print("Yes")
```
集合高阶函数使用:
```kotlin
names
    .filter { it.startsWith("A") }
    .sortedBy { it }
    .map { it.toUpperCase() }
    .forEach { print(it) }
```
详情 <a href="Higher-order functions and Lambdas" target= "_blank">Higher-order functions and Lambdas</a>。




