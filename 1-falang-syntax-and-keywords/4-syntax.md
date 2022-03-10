# 语法


## 注释

### 单行注释

如果要添加单行注释，在要注释的文字或语句前添加 `//` 即可，**编译器在编译时会忽略所有被注释的内容**

添加单行注释的示例：

```
use fa;

//我是单行注释
class Program {
	public static void Main () {
		//Console.Write ("hello");
	}
}
```

### 多行注释

如果要添加多行行注释，在要注释的开头和结尾添加 `/*` 和 `*/` 即可，**编译器在编译时会忽略所有被注释的内容**

```
use fa;

/*
我是多行注释开头
class Program {
	public static void Main () {
	    Console.Write ("hello"); 我是多行注释中间 
	}
}
我是多行注释结尾
*/
```

## 语句

### 语句语法

#### 结束符

在编写fa时，需要在语句的末尾写上`;`结束符表示此语句结束

```
use fa;

class Program {
	public static void Main () {
	    Console.Write ("hello"); //我是结束符 
	}
}
```

如果使用for循环，if等语句，也需要使用到`;`。用于在其条件表达式隔断条件，和在其代码块末尾表示结束。

```
use fa;
class Program {
int n = 45
//表达式表示隔断
while int a = 0; a < n; ++a{
		break;
	}
}
```

##### 在if中的使用示例：

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
		};//在其代码块末尾表示结束
		Console.Write (_s);
	}
}
```

#### 包裹符

在编写类，函数，等需要标明作用域的功能时，需要用`{}`来依次包裹，推荐使用缩进来优化代码可读性

```
use fa;

class Program {
	public static void Main () {
	    Console.Write ("hello");  
	}//我包裹着Main函数
}//我包裹着Program类
```

### 函数

在编写函数时，需要使用`()`来包裹参数，要是用`()`也有表示函数的作用

```
use fa;

class progam{
	//参数a,b被"()"包裹在函数里
    public static void Main (a,b){
		c = a+b
		Console.Write ("这是一个有返回值函数，在这里return用来终止函数并返回值");
		return c ;
  }
  
}
```

`.`用来调用类中的方法函数

```
use fa;

class progam{
  public static void Main (){
	Console.Write ('这里使用 "." 调用了Console类的Write函数，并在"()"里传入了一串字符串给参数  ');
	return c ;
  }

}
```

### 表达式

fa中的数学符号表达式有：

`=` 赋值

`<`大于

`>`小于

`=>`小于等于

`<=`大于等于

`==`全等

`!=`不等于

**它们会返回一个布尔值，当条件成立则返回`True`，不成立返回`False`**

数学运算表达式：

`+`加

`-`减

`*`乘

`/`除

`%`模

`^`幕

`+=`加等于（赋值）

`-=`减等于（赋值）

`++`自增（+1）

`--`自减（-1）

**它们用于进行数学运算，并返回得到的值**
