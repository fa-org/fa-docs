# 关键字

## 基本关键字

### if的用法

if 在 Fa 语言里有两种用法：语句和表达式

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

> if当语句用时，block处写语句，满足条件即可执行

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

> if当表达式用时，block处写表达式，满足条件即给_s变量赋值

### switch 的用法

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

### return的用法



return在fa中可以用来返回值，也可以终止函数



1.终止函数的例子：

```
use fa;

class progam{
  public static void Main (){

  Console.Write ("这是一个无返回值函数，在这里return用来终止函数");
  return;
  }
  
}
```

2.返回值的例子：

```
use fa;

class progam{
  public static void Main (a,b){
	c = a+b
  Console.Write ("这是一个有返回值函数，在这里return用来终止函数并返回值");
  return c ;
  }
  
}
```



------

## 循环关键字

for在fa里有两种用法：

### while 的用法（循环）

while在fa里有两种用法：while循环，whlie ture循环，while do循环

#### 1.whlie循环的示例：

```
use fa;
class Program {
int n = 45
while int a = 0; a < n; ++a{
				break;
			}
}
```

#### 2.whlie ture循环的示例：

```
use fa;
class Program {
while true {
				break;
			}
}
```

#### 3.while do循环的示例：

```
use fa;
class Program {
while do {
				break;
			}
}
```

### for的用法（循环）

while在fa里有两种用法：for循环

#### 1.for循环的示例：

```
use fa;

public static void Main () {
		int n = 10;
		for int a = 0; a < n.Length; ++a {
			Console.Write ("hello");
		}
	}
```

### Break的用法（循环）

Break在fa里有两种用法：跳出循环

#### 1.Break在while ture循环中跳出的示例：

```
use fa;
class Program {
while true {
				break;
			}
}
```

### continue的用法（循环）

continue在fa里有两种用法：继续循环

### return的用法（循环）

return在循环里有两种用法：跳出循环并返回指定的值
