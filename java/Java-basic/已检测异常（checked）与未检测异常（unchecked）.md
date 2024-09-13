### 已检测异常（checked）与未检测异常（unchecked）

- java语言将派生于Error类或RuntimeException类的所有异常称为未检测异常（unchecked）

  所有的其他异常称为已检测异常（checked）。

- 一个方法必须声明所有可能抛出的已检查异常，否则编译器就会报错。

- 而未检查异常要么不可控制（Error），要么就应该避免发生（RuntimeException）。不应该声明从Error或RuntimeException中继承的那些未检测异常。