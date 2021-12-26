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
