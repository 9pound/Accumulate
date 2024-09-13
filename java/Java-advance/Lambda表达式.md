# Lambda表达式

Lambda表达式是函数式接口的实例，是函数式接口的一个具体实现（匿名函数）

语法： 

- 参数列表

- 箭头
- lambda 主体

```
(parameters) -> expression
(parameters) -> { statements; }
```

**函数式接口**：只定义一个抽象方法的接口

- 即使接口有很多默认方法，只要接口只定义了一个抽象方法，它就任然是一个函数式接口

**函数描述符**：函数式接口中的抽象方法的签名

@FunctionalInterface：函数式接口的注解

### 常用的函数式接口

**Predicate<T>**

(T) -> boolean

**Consumer<T>**

(T)->void

**Function<T,R>**

(T)->R

**Supplier<T>**

()->T

**UnaryOperator<T>**

(T)->T

**BinaryOperator<T>**

(T,T)->T

**BiPredicate<L,R>**

(L,R)->boolean

**BiConsumer<T,U>**

(T,U)->void

**BiFunction<T,U,R>**

(T,U)->R

问题：任何函数式接口都不允许抛出受检测异常（checked exception）,如果lambda表达式需要抛出异常怎么办？

1. 定义自己的函数式接口，并声明受检测异常。
2. 把lambda表达式包含在try/catch块中