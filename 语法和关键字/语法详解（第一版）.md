$$
fa语言中有许多关键字和语法，本文档将会介绍他们的功能以及如何使用
$$



### 第一章：关键字

### 第二章：对象

### 第三章：类型

### 第四章：语法详解

------

------



## 第一章：关键字

### 第一节：基本关键字

#### 第一小节：if的用法

if在fa里有两种用法：语句和表达式

#### 1.在语句中的使用示例：

```
use fa;

class Program {
	public static void Main () {
		int n = 10;
		if n == 7 {
			Console.Write (""error"");
		} else {
			if n == 10 {
				Console.Write (""TestIf1"");
			} else {
				Console.Write (""error"");
			}
		}
	}
}
```



if当语句用时，block处写语句，满足条件即可执行

#### 2.在表达式中的使用示例：

```
use fa;

class Program {
	public static void Main () {
		int n = 10;
		string _s = if n == 7 {
			""error""
		} else {
			if n == 10 {
				""TestIf4""
			} else {
				""error""
			}
		};
		Console.Write (_s);
	}
}
```

if当表达式用时，block处写表达式，满足条件即给_s变量赋值

------

#### 第二小节：switch 的用法

switch在fa里有三种用法：语句——switch when(类似于很多语言的switch case)，枚举，表达式

#### 1.switch when的用法示例

使用switch when时，需要给定when一个判断条件，且可以选择要命中when或跳过when。

switch当语句用时，可选择跳过when，满足条件即可执行：

```
use fa;

class Program {
	public static void Main () {
		int n = 10, o = 12;
		switch n {
			3              => Console.Write (""error"");
			10 when o == 7 => Console.Write (""error"");
			10             => Console.Write (""TestSwitch1"");
			_              => Console.Write (""error"");
		}
	}
}
```

也可以选择命中when，满足条件继续执行：

```
use fa;

class Program {
	public static void Main () {
		int n = 10, o = 12;
		switch n {
			3               => Console.Write (""error"");
			10 when o == 12 => Console.Write (""TestSwitch2"");
			10              => Console.Write (""error"");
			_               => Console.Write (""error"");
		}
	}
}
```

使用单个变量命中when的示例：

```
use fa;

class Program {
	public static void Main () {
		int o = 12;
		switch {
			when o == 7  => Console.Write (""error"");
			when o == 12 => Console.Write (""TestSwitch7"");
			when o == 15 => Console.Write (""error"");
			_            => Console.Write (""error"");
		}
	}
}
```

未命中时的示例：

```
use fa;

class Program {
	public static void Main () {
		int n = 10, o = 12;
		switch n {
			3              => Console.Write (""error"");
			10 when o == 7 => Console.Write (""error"");
			11             => Console.Write (""error"");
			_              => Console.Write (""TestSwitch3"");
		}
	}
}
```



#### 2.switch在表达式中的用法示例

switch 表达式，命中when	

```
use fa;

class Program {
	public static void Main () {
		int o = 12;
		string k = switch {
			when o == 7  => ""error"",
			when o == 12 => ""TestSwitch9"",
			when o == 15 => ""error"",
			_            => ""error"",
		};
		Console.Write (k);
	}
}
```

switch在表达式中的语法同样是switch when（可选择命中或不命中），由表达式中的变量接收返回值。

switch表达式，未命中when

```
use fa;

class Program {
	public static void Main () {
		int o = 12;
		string k = switch {
			when o == 7  => ""error"",
			when o == 11 => ""error"",
			when o == 15 => ""error"",
			_            => ""TestSwitch10"",
		};
		Console.Write (k);
	}
}
```

在这里如果when没有被命中（为空），则继续执行，返回switch的类型

#### 3.switch枚举的用法示例

使用switch做枚举时，需要给定变量一个枚举成员，然后switch检测该变量.

switch枚举值变量的示例：

```
use fa;

enum TestEnum { A, B, C }

class Program {
	public static void Main () {
		TestEnum e = TestEnum.B;
		switch e {
			TestEnum.A => Console.Write (""error"");
			TestEnum.B => Console.Write (""TestSwitch11"");
			TestEnum.C => Console.Write (""error"");
		}
	}
}
```

Switch语句解构带参数枚举示例:

```
use fa;

enum TestEnum { A, B (int), C }

class Program {
	public static void Main () {
		TestEnum e = TestEnum.B (12);
		switch e {
			TestEnum.A        => Console.Write (""error1"");
			TestEnum.B (_var) => Console.Write (""TestSwitch{0}"".Format (_var));
			TestEnum.C        => Console.Write (""error3"");
		}
	}
}
```

在此示例中，此枚举数共有A，B，C三种可能，B可携带一个int参数。构造e对象时，指定e=TestEnum.B，并附带12这个int类型数字，然后交由switch解析。如果结果正确（对象e等于枚举值B，_var为携带的参数），那么继续执行，返回switch的类型（testswitch{0}）和携带的参数(var)

switch 表达式解构带参数枚举示例（1）：

```
use fa;

enum TestEnum { A, B (int), C, D (string) }

class Program {
	public static void Main () {
		TestEnum e = D (""err1"");
		e = TestEnum.B (13);
		string s = switch e {
			TestEnum.A        => ""error"",
			TestEnum.B (_var) => ""TestSwitch{0}"".Format (_var),
			C                 => ""error"",
			D (_val)          => _val,
			_                 => ""error"",
		};
		Console.Write (s);
	}
}
```

e在这里被赋值了两次，第一次值为D，第二次为B。switch在此示例中会解构变量中的枚举数值，然后表达式中的变量接收返回的结果，在本案例中只返回一个值。如你所见，A,B是标注了类型名的，而C,D则是**省略了类型名**的

switch 表达式解构带参数枚举示例（2）：

```
use fa;

enum TestEnum { A, B (int), C, D (string) }

class Program {
	public static void Main () {
		TestEnum e = C;
		e = TestEnum.A;
		string s = switch e {
			TestEnum.A        => ""TestSwitch14"",
			TestEnum.B (_var) => ""error{0}"".Format (_var),
			C                 => ""error"",
			D (_val)          => _val,
			_                 => ""error"",
		};
		Console.Write (s);
	}
}
```

在这里e被直接赋值了一个类型中的成员，且**不携带任何给定的参数**

#### 第三小节：return的用法

------

### 第三节：循环关键字

for在fa里有两种用法：

#### 第一小节：while的用法（循环）

while在fa里有两种用法：while循环，whlie ture循环，while do循环



1.whlie循环的示例：

```
use fa;
class Program {
int n = 45
while int a = 0; a < n; ++a{
				break;
			}
}
```

2.whlie ture循环的示例：

```
use fa;
class Program {
while true {
				break;
			}
}
```

3.while do循环的示例：

```
use fa;
class Program {
while do {
				break;
			}
}
```

------



#### 第二小节：for的用法（循环）

while在fa里有两种用法：for循环



1.for循环的示例：

```
use fa;

public static void Main () {
		int n = 10;
		for int a = 0; a < n.Length; ++a {
			Console.Write ("hello");
		}
	}
```



<u></u>

#### 第三小节：Break的用法（循环）

Break在fa里有两种用法：跳出循环

1.Break在while ture循环中跳出的示例：

```
use fa;
class Program {
while true {
				break;
			}
}
```



#### 第四小节：continue的用法（循环）

continue在fa里有两种用法：继续循环

#### 第五小节：return的用法（循环）

return在循环里有两种用法：跳出循环并返回指定的值



------

## 第二章：对象

> fa语言是一个面向对象的语言，在这一章将会介绍一些基本的对象语法

### 第一节：类

在fa语言中创建一个类需要使用`class`关键字，简单使用示例如下：

```
use fa;

class Dic0 {
	public string s;
}
```

在这个示例里，使用`class`关键字定义了一个名为`Dic0`的类。在类里有一个公共`public`的字符串型`string`变量，变量名为`s`

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

在这个示例里，使用`class`关键字定义了一个名为`program`的类，在类中定义了一个公共`public`的静态`static`函数`void`，函数名为`Main()`，也就是主函数。

在fa中，类的成员可以有这么几种属性：

1.公共的`public`

2.私有的`private`

------

## 第三章：类型

> 在fa中有许多不同种类的类型，在本章中将会分类并逐个讲述每种类型

### 第一节：内置类型

在fa中，有以下内置类型：

1. `string`字符串类型
2. `int`整数类型
3. `void`函数类型

#### 第一小节：string字符串类型

`string`字符串类型使用示例：

```
string n = "hello,str!你好,我是str!"
```

详解：在这里我们定义了一个名为n的变量，指定为字符串类型`string n`，并赋值`= "hello,str!你好,我是str!"`

#### 第二小节:`int`整数类型

`int`整数类型使用示例：

```
int n = 114514
```

详解：在这里我们定义了一个名为n的变量，指定为字符串类型`int n`，并赋值`= 114514`

#### 第三小节:`void`函数类型

`void`函数类型使用示例：

```
use fa;

class Program {
	public static void Main () {
		string a = "hello,str!"
		int b = 114514
	}
	
	void hellofunc(){
	
	}
```

详解：

在这里，我们定义了一个main函数和一个hellofunc函数，在fa中，**main函数是程序的入口**，程序会从这开始执行。hellfunc函数则是一个普通函数。

要定义一个函数，需要使用void关键字，简单使用示例：

```
void funcname()
{

}
void hellofunc(){

}
```

在fa中，函数可以有这么几种属性：

1.公共的`public`

2.私有的`private`

### 第二节：可选类型

`void?`函数可选类型

`int?`整数可选类型

### 第三节：数组类型

`int[]`列表数组类型



1.int[]数组类型示例：

```
use fa;

class Program {
	public static void Main () {
		int[] n = [45, 4123, 213, 42];
		n [3] = 1234;
	}
```

详解：在此示例中，先是定义了一个名为n的数组类型，赋值`int[] n = [45, 4123, 213, 42];`。然后将n中索引为3的值（42）赋值为1234	`n [3] = 1234;`。现在n的值为：`45,4123,213,1234`

<u></u>

## 第四章：语法详解

### 第一节：注释

#### 第一小节：单行注释

要在fa中添加多行注释，需要使用`//`关键字

添加单行注释的示例：

```
use fa;

//我是单行注释
class Program {
	public static void Main () {
		//Console.Write ("hello");
	}
```

详解：如果要添加单行注释，在要注释的文字或语句前添加`//`即可，**编译器在编译时会忽略所有被注释的内容**

#### 第二小节：多行注释

要在fa中添加多行注释,需要使用`/* */`关键字

添加多行注释的示例：

```
use fa;

/*我是多行注释开头
class Program {
	public static void Main () {
		我是多行注释中间Console.Write ("hello");
	}
	我是多行注释结尾*/
```



### 第二节：计算符

#### 第一小节：基本计算符

fa中所有的计算符



