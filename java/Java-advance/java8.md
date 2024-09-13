# java8



类型推断

- 在Lambda表达式中可以省去标注的参数类型
- 当Lambda仅有一个类型需要推断的参数时，参数名称两边的括号也可以省略





方法引用：让你重复使用现有方法定义并像lambda一样传递她们

基本思想，如果一个Lambda表达式代表的只是直接调用这个方法，那最好还是用名称来调用它

lambda表达式的快捷写法



方法引用的分类

- 静态方法的方法引用
- 指向任意类型实例方法
- 对象的实例方法



特殊的方法引用

构造函数

数组构造函数

父类调用

方法应用的签名必须和上下文类型匹配



构造函数引用

语法：

ClassName：：new；



```
Supplier<Apple> c1 = () -> new Apple();
Apple a1 = c1.get();

Supplier<Apple> c1 = Apple::new
Apple a1 = c1.get();

Function<Integer,Apple> c2 = (weight) -> new Apple(weight);
Apple a2 = c2.apply(2);

Function<Integer,Apple> c2 = Apple::new;
Apple a2 = 

```





比较器链

Comparator

reversed（）

thenComparing();

谓词符合

Predicate

negate()

and()

or()

函数符合

Function

andThen

compose