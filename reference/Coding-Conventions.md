原文 http://www.kotlinlang.org/docs/reference/coding-conventions.html

## 代码规范约定
此页面包含了kotlin当前的编码风格。

### 命名风格
默认使用java的编码风格，例如:   
&#151;  使用驼峰命名法(尽量不要用下划线)   
&#151;  类名开头大写   
&#151;  方法和属性开头小写   
&#151;  使用4个空格来缩进   
&#151;  public 功能应该有文档注释   

### 冒号
冒号分隔的类型和父类有空格，冒号分隔实例和类型前的冒号有空格:
```kotlin
interface Foo<out T : Any> : Bar {
    fun foo(a: Int): T
}
```


### Lambdas 表达式
在lambdas中大括号内两边应该有空格，还有参数箭头两边，一个lambdas表达式尽可能的从外面括号传入:
```kotlin
list.filter { it > 10 }.map { element -> element * 2 }
```
Lambda表达应该简短并且不要嵌套，推荐显式的声明参数，如果有嵌套的lambda表达式，应该明确声明参数。

### Unit
如果函数没有返回值，返回类型应该被忽略:
```kotlin
fun foo() { // ": Unit" 在这里可以省略

}
```
