# 对象

> fa语言是一个面向对象的语言，在这一章将会介绍一些基本的对象语法

## 类

在fa语言中创建一个类需要使用 `class` 关键字，简单使用示例如下：

```
use fa;

class Dic0 {
	public string s;
}
```

在这个示例里，使用 `class` 关键字定义了一个名为 `Dic0` 的类。在类里有一个公共 (`public`) 的字符串型 (`string`) 变量，变量名为 `s`

类中也可以包含函数，添加一个类并在这个新类中加上函数：

```
use fa;

class Dic0 {
	public string s;
}
class Program {
	public static void Main () {
		Dic0 d = new { s = ""TestObject1"" };
		Console.Write (d.s);
	}
}
```

在这个示例里，使用 `class` 关键字定义了一个名为 `program` 的类，在类中定义了一个公共 (`public`) 的静态 (`static`) 函数，返回值为空 (`void`)，函数名为 `Main()`，也就是主函数。
