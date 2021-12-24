**test中含有了许多关键字的特殊和详细用法，本文档将会介绍他们的功能以及如何使用**

### 第一章：if

### 第二章: switch

### 第三章：object

### 第四章：Algorithm

------

------



## 第一章：if 的用法

if在fa里有两种用法：语句和表达式

#### 1.在语句中的使用示例：

![img_test_if01](./testimgs/img_test_if01.png)

if当语句用时，block处写语句，满足条件即可执行

#### 2.在表达式中的使用示例：

![img_test_if02](./testimgs/img_test_if02.png)

if当表达式用时，block处写表达式，满足条件即给_s变量赋值

------

## 第二章：switch 的用法

switch在fa里有三种用法：语句——switch when(类似于很多语言的switch case)，枚举，表达式

#### 1.switch when的用法示例

使用switch when时，需要给定when一个判断条件，且可以选择要命中when或跳过when。

switch当语句用时，可选择跳过when，满足条件即可执行：

![img_test_if03](./testimgs/img_test_switch01.png)



也可以选择命中when，满足条件继续执行：![img_test_if04](./testimgs/img_test_switch02.png)

使用单个变量命中when的示例：

![img_test_if07](./testimgs/img_test_switch03.png)

未命中时的示例：

![img_test_if07](./testimgs/img_test_if07.png)

#### 2.switch在表达式中的用法示例

switch 表达式，命中when	![img_test_switch13](/Users/wuzitong/Desktop/programming/fa/fa_Docs/test文档/testimgs/img_test_switch13.png)

switch在表达式中的语法同样是switch when（可选择命中或不命中），由表达式中的变量接收返回值。

switch表达式，未命中when

![img_test_switch14](/Users/wuzitong/Desktop/programming/fa/fa_Docs/test文档/testimgs/img_test_switch14.png)

在这里如果when没有被命中（为空），则继续执行，返回switch的类型

#### 3.枚举的用法示例

使用switch做枚举时，需要给定变量一个枚举成员，然后switch检测该变量.

switch枚举值变量的示例：

![img_test_switch09](./testimgs/img_test_switch09.png)



Switch语句解构带参数枚举示例:

![img_test_switch10](/Users/wuzitong/Desktop/programming/fa/fa_Docs/test文档/testimgs/img_test_switch10.png)

在此示例中，此枚举数共有A，B，C三种可能，B可携带一个int参数。构造e对象时，指定e=TestEnum.B，并附带12这个int类型数字，然后交由switch解析。如果结果正确（对象e等于枚举值B，_var为携带的参数），那么继续执行，返回switch的类型（testswitch{0}）和携带的参数(var)

switch 表达式解构带参数枚举示例（1）：

![img_test_switch11](/Users/wuzitong/Desktop/programming/fa/fa_Docs/test文档/testimgs/img_test_switch11.png)

e在这里被赋值了两次，第一次值为D，第二次为B。switch在此示例中会解构变量中的枚举数值，然后表达式中的变量接收返回的结果，在本案例中只返回一个值。如你所见，A,B是标注了类型名的，而C,D则是**省略了类型名**的

switch 表达式解构带参数枚举示例（2）：

![img_test_switch12](/Users/wuzitong/Desktop/programming/fa/fa_Docs/test文档/testimgs/img_test_switch12.png)

在这里e被直接赋值了一个类型中的成员，且**不携带任何给定的参数**

### 第三章：Dic的用法



