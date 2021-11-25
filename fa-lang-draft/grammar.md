# fa语言草案之语法

## .fa文件组织方式

```fa
// 【可选】use列表
use fa;

// 【可选】引用本地库文件（临时）
@lib "ucrt.lib";

// 【可选】定义引用库文件内的函数声明
@import int32 __cdecl puts (cptr);

// 【可选】重写命名空间
namespace MyProject.Test;

// 【可选】定义类结构
public class MyClass {
    //
}
```

## 命名空间

fa语言项目默认命名空间与源码文件所在位置相关，关系如下：

| 源码文件路径示例 | 默认命名空间 |
| :--- | :--- |
| fa项目名/src/main.fa | fa项目名 |
| fa项目名/src/path/of_dir/test.fa | fa项目名.path.of_dir |

假如上述功能无法满足需要，那么可以在源码文件加入 `namespace` 来覆盖默认命名空间。

### 命名空间的引用

引用列表必须为`项目内部命名空间`、`fa标准库命名空间`或`fa三方库中已定义的命名空间`，用于省略调用时过长的命名空间名称。

## 引用本地库文件

语法为 `@lib "静态库或动态库文件名";`，编译器根据扩展名决定在编译时置入还是在运行时动态加载。

### 调用库文件函数

语法为 `@import 返回类型 调用协定 函数名 (参数列表);`。

调用协定支持三种方式：

- __cdecl
    + C语言通用传参方式
- __fastcall
    + 快速调用传参方式
- __stdcall
    + Win32 API传参方式

## 定义类结构

### 成员变量

成员变量声明示例：

```fa
public class MyClass {
	public static int32 s_value = 123;

	public int32 m_val1;
	public int32 m_val2 = 333;
}

// 上面类有两种构造方式
MyClass _o1 = new MyClass { m_val1 = 12 };                // 后一个MyClass可省略
MyClass _o2 = new MyClass { m_val1 = 12, m_val2 = 345 };  // 后一个MyClass可省略
```

### 构造函数

构造函数分两种，带参数的和不带参数的。示例：

```fa
public class MyClass {
	public int32 m_val1;
	public int32 m_val2 = 333;

	public MyClass () {
		Console.WriteLine ("无参构造");
	}

	public MyClass (int32 n) {
		m_val1 = n; // 构造函数里必须给它赋值
		Console.WriteLine ("带参构造");
	}
}

// 调用以上构造函数方式为：
MyClass _o1 = new MyClass { m_val1 = 12 }; // 调用无参构造，后一个MyClass可省略
MyClass _o2 = new MyClass (33);            // 调用带参构造，后一个MyClass可省略
```

需注意，带初始列表构造或不带参构造，都会调用无参构造函数。

### 析构函数

析构函数示例：

```fa
public class MyClass {
	~MyClass () {
		Console.WriteLine ("对象被析构");
	}
}
```

需注意，析构函数不需要我们自己去调用，对象生命周期也不需要我们自己维护，只要没有代码能访问到这个对象，对象自己就被析构掉了。

遇到new关键字时，fa编译器默认指定对象为栈变量，假如无法满足需求，那么自动转为堆变量、计数变量或跨线程原子计数变量，这个升级过程由编译器自动完成，无需考虑实现。这几种实现方式区别为：

| 变量实现方式 | 特点 |
| :---: | :--- |
| 栈 | 函数结束即被释放 |
| 堆 | 变量可在函数外被访问 |
| 堆计数 | 依赖关系较复杂时，它能准确控制需释放时间点 |
| 堆原子计数 | 相比上者多加了原子功能，可跨线程同时访问 |

另请注意：**fa程序不带GC，变量不被使用时立即释放**

### 成员方法

成员方法示例：

```fa
public class MyClass {
	public static void print1 () {
		Console.WriteLine ("静态方法");
	}

	public void print2 () {
		Console.WriteLine ("动态方法");
	}
}
```

### 成员转换方法

成员转换方法为一种特殊的静态方法，函数名必须为`From`，它可以指定类能由哪些类型通过隐式转换得来。示例：

```fa
public class MyClass {
	public static MyClass From (int32 i) {
		MyClass _cls = new ();
		_cls.m_val = i;
		return _cls;
	}
}

// 调用方式
MyClass val = 12;
```

### 继承

TODO

### 传参

TODO

### 接口

TODO

## 枚举类型

TODO

## 异常处理

允许空值的返回类型代表支持异常处理，遇到异常时，假如用户没做完整的处理，并且出现UB，那么将返回null并且携带错误信息与异常栈。

如果正常的逻辑需要使用到带空的返回类型，那么不识别错误信息与错误栈即可。

示例代码：

```fa
int32? calc_div (int32 a) {
	int32? x = a / 0;                                   // 执行后x的值为null
	int32 y = a / 0 ? 1;                                // 执行后y的值为1
	int32 z = a / 0;                                    // 执行后函数直接返回，返回值为null
	int32 z = (a / 0).unwrap (new DeviceZeroError ());  // 等价上一句
	int32? zz = new DeviceZeroError ();                 // 赋值一个错误（同时指定值为null）
	throw new DeviceZeroError ();                       // 抛异常
}

int32? calc_div_wrap1 (int32 a) {
	return calc_div (a);
}

int32? calc_div_wrap2 (int32 a) {
	int32? b = calc_div_wrap1 (a);

	// 错误处理方式1
	switch b {
		int32 (_b) => Console.WriteLine ("{b}");
		Error (_e) => {
			Console.WriteLine ("遇到异常：{_e.Message}");
			Console.WriteLine ("{_e.Stack}");
		}
	}

	// 错误处理方式2
	if b is valid {
		// 此处b临时升级为int32类型（假如b的值有被修改那么临时升级措施失效）
		Console.WriteLine ("{b}");
	} else {
		// 此处b临时升级为Error类型
		Console.WriteLine ("遇到异常：{b.Message}");
		Console.WriteLine ("{b.Stack}");
	}
}
```

如果某个函数不希望异常传递，那么可以修改返回类型为不可空类型，那么此函数必须能够处理或忽略所有可空的数据，否则将编译报错。
