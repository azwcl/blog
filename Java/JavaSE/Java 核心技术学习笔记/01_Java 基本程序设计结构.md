# 1. Java 基础程序设计结构

## 1. 典型 Java 程序

```java
public class JavaDemo {
    public static void main(String[] args) {
        System.out.println(" Hello Java! ");
    }
}
```

-   区分大小写；
-   `main` 方法必须要声明为 `public` ；

## 2. 注释

```java
// 这是一个单行注释

/**
多行内容注释
*/

/**
 * 使用该注释可以用来自动生成文档；文档注释
 */
```

## 3. 数据类型

强类型语言，八种基本类型；4 种整形，2 种浮点型，1 种字符型，1 种布尔型；

### 3.1. 整型

| 类型    | 存储大小 | 取值范围                                   |
| ------- | -------- | ------------------------------------------ |
| `int`   | 4 字节   | -2147483648 ~ 2147483647                   |
| `short` | 2 字节   | -32768 ~ 32767                             |
| `long`  | 8 字节   | -9223372036854775808 ~ 9223372036854775807 |
| `byte`  | 1 字节   | -128 ~ 127                                 |

-   在 `Java` 中，所有平台，其整型范围都一样；与平台无关；
-   长整型 `long` 数值后面有一个后缀 `l` 或者 `L`；十六进制数值有一个前缀 `0x` 或 `0X`；八进制有一个前缀 `0`；`Java 7` 开始，`0b` 或者 `0B` 代表二进制数；同样，`Java 7` 开始，数字可以加下划线区分；方便读写；例如 `1_000_000` (或者 `0b1111_0100`)；`Java` 编译器会自动去除；
-   `Java` 没有任何无符号的形式的整型；如果确实需要无符号的数字；例如 `Byte` 提供了 `toUnsignedInt` 方法得到 `0 ~ 255` 的 `int` 的值；`Integer` 和 `Long` 类都提供了处理无符号出发和求余数的方法；

### 3.2. 浮点型

| 类型     | 存储大小 | 取值范围                                       |
| -------- | -------- | ---------------------------------------------- |
| `float`  | 4 字节   | 大约 ±3.40282347E+38F (有效位数 6 ~ 7 位)      |
| `double` | 8 字节   | 大约 ±1.79769313486231570E+308(有效位数 15 位) |

-   `float` 类型数值需要有后缀 `F` 或者 `f`；无该后缀，则默认为 `double` 类型；当然也可以在其后面添加后缀 `D` 或者 `d`； 
-    可以用十六进制表示浮点数；例如 0.125 = 2^-3 可以表示为 0x1.0P-3；在十六进制表示法中；`p`表示指数；而并非是 `e`； 
-    浮点数值计算遵循 `IEEE 754` 标准；有三个特殊值：正无穷大 ( `Double.POSITIVE_INFINITY` )，负无穷大 ( `Double.NEGATIVE_INFINITY` )，`NaN` ( `Double.NaN` )( `float` 同)； 
-    浮点数值不适合金融计算；因为其无法表示精确值；就像十进制数字无法表示 `1/3` 一样；二进制数字也无法表示 `1/10` ； 

### 3.3. char 类型

-   原本用来表示单个字符；不过现在 一些 `Unicode` 字符也可以用一个 `char` 值来进行描述；另外一些 `Unicode` 字符则需要两个 `char` 值； 
-    范围 `\u0000` ~ `\uFFFF` 
-    `Unicode` 转移序列会在解析代码前进行处理；最隐秘的就是；一定要注意注释的 `\u`；

```java
public class Main {
    public static void main(String[] args) {
//        \u000A is a newlink
        // 上面的注释会报错；因为 \u000A 会被替换为换行符；
        // look c:\users
        // 上面的也会报错；因为他后面没有跟着4个十六进制数字；所以需要注意；
        return;
    }
}
```

-    在 `Java` 中，`char` 类型描述的是 `UTF-16` 编码中的一个代码单元； 

### 3.4. 码点和代码单元

[转向专题](https://blog.azwcl.com/archives/1734136785011) https://blog.azwcl.com/archives/1734136785011

### 3.5. 布尔类型

-   两个值：`false` 和 `true` ；整型与布尔值之间不能相互转换；在《Java编程思想》特别指出：其类型所占用存储空间并没有明确指定；
-   在栈帧中以局部变量的方式存在就占用4个字节，在堆中就占用1个字节即可

## 4. 变量与常量

### 4.1. 声明变量

```java
double monry;
int days;
```

-   变量必须是一个字母开头，并且由字母或者数组构成的；但是字母和数字范围很大，字母表示的是在某个语言中表示字母的任何 `Unicode` 字符；数字也是在某个语言中表示数字的任何 `Unicode` 字符；
-   大小写敏感，变量名长度基本无限制；空格不行，例如 `+` 等符号不可出现；
-   Java 9 开始， 单下划线不可作为变量名；

### 4.2. 变量初始化

-   声明变量后；需要用赋值语句进行显式初始化；不可使用未初始化的变量；否则编译错误；

### 4.3. 常量

-   利用 `final` 关键字修饰常量；只能被赋值一次，且不能够再更改了；习惯上，常量名用全大写；
-   类常量(`class constant`)：利用关键字：`static final` 设置类常量；

### 4.4. 枚举类型

-   `enum` 关键字；

## 5. 运算符

### 5.1. 算术运算符

```java
+,-,*,/,%
```

-   整数被 0 除会产生一个异常；浮点数被 0 除会得到无穷大或者 `NaN` 结果；

>   因为可移植性的问题；无论在哪个虚拟机上运行同一运算都应该得到一样的结果；但是对于浮点数的算术运算，实现这样的可移植性是非常难的；double 类型采用 64 位存储；但是有些处理器则使用了 80 位浮点寄存器；这些寄存器增加了中间过程的计算精度；
>
>   例如：double w = x * y / z;
>
>   很多 Inter 的处理器都会计算 x * y ，将结果存储在 80 位的寄存器中，再进行除以 z 将结果截断为 64 位；从而得到一个更加精确的结果，且避免指数溢出；但是这样结果可能与 64 位计算结果不一样；故在最初的时候，Java 虚拟机规定所有的中间计算结果都要进行截断；但被反对，因为截断需要时间，而且可能导致溢出；
>
>   Java 承认了最有性能与理想的可再生性之间存在的冲突，并且给予了改进；在默认情况之下，虚拟机设计者允许对中间计算结果采用扩展的精度；但是如果使用 `strictfp` 关键字标注的方法，则必须使用严格的浮点计算来生成可再生结果；
>
>   如果一个类标记为 `strictfp`；则其中类的所有方法都要使用严格的浮点运算；
>
>   具体的计算细节取决于 Intel 处理器的行为，默认情况之下，中间结果允许使用扩展的指数，不允许使用扩展的尾数（ Intel 芯片支持截断尾数时并不损失性能）；因此，两种方式的区别仅仅是采用默认方式不会产生溢出；但实际上也不是啥大问题，大多数程序来说，浮点溢出小问题；

### 5.2. 数学函数与常量

-   `Math` 类中含有各种的数学函数；可以加以利用；
-   `Math` 为了达到最佳性能；都是使用计算机浮点单元中的例程；如果得到一个完全可预测的结果比性能重要，应该使用 `StrictMath` 类；实现了可自由分发的数学库的算法，确保所有平台得到相同结果；
-   `Math` 类提供了一些方法，使得运算更具有安全性；例如 10 亿 乘以 3 计算结果溢出为：-12...；悄无声息，且不报错；但是如果使用 `Math.multiplyExact(1000000000, 3)`; 则是产生一个异常；

### 5.3. 数值类型之间的转换

![000001-003.png](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2024/12/1734175989f1cead.png)

-   实线箭头为无信息丢失；虚线代表可能存在精度丢失；

    ```java
    int n = 123456789;
    float f = n; // f is 1.23456792E8
    ```

### 5.4. 强制类型转换

-   可能会丢失精度；
-   必须显式；

### 5.5. 结合赋值和运算符

-   `x += 4` ==> `x = x + 4`；同理： `*=`... 等；

### 5.6. 自增自减运算符

-   `++` 与 `--` ；

### 5.7. 关系和布尔运算符

-   `==`;`!=`;`<`;`>`;`<=`;`>=`;`&&`;`||`;`? :`；

### 5.8. 位运算符

-   `&`;`|`;`^`;`~`;`<<`;`>>`;

### 5.9. 括号与运算符级别

-   不使用括号，按照运算符优先级次序进行计算，同一级别从左到右；

## 6. 字符串

### 6.1. 子串

-   `substring` 可以从较大字符串提取出一个子串；

### 6.2. 拼接

-   允许 + 号拼接两个字符串；
-   一个字符串与非字符串的值进行拼接时，后者会转换成字符串；
-   使用 `String.join` 方法；
-   使用 `repeat` 方法；

### 6.3. 不可变字符串

-   `String` 类对象是不可变的；

>   原因：Java 设计者认为共享带来的高效率远远胜于提取子串、拼接字符串的低效率；

### 6.4. 检测字符串是否相等

-   `equals` 方法；
-   `equalsIgnoreCase` 忽略大小写；

### 6.5. 空串与 `Null` 串

-   空串是长度为 0 的字符串；
-   `null` 串就是 `null`；

### 6.6. 码点与代码单元

-    `Java` 字符串由 `char` 值序列组成；`char` 数据类型是一个采用 `UTF-16` 编码表示 `Unicode` 码点的代码单元； 
-    `length` 方法将返回采用 `UTF-16` 编码表示给定字符串所需要的代码单元数量； 
-    要想得到实际的长度，即码点数量，需要`codePointCount(0, str.length())`； 

```java
String str = "🍺";
System.out.println(str.length()); // 2
System.out.println(str.codePointCount(0, str.length())); // 1
```

-   `charAt(n)` 将返回特定位置 `n` 上的代码单元； `n` 介于 `0 ~ s.length() - 1` 之间； 

-    如果说要得到第 i 个码点： 

    -   ```java
        int index = str.offsetByCodePoints(0, i);
        int cp = str.codePointAt(index);
        ```

-   如果遍历码点最容易的采用 `codePoints` 方法：

    -   ```java
        int[] codes = str.codePoints().toArray();
        ```

-   反之，如果将一个码点数组转换成一个字符串，可以采用构造器：

    -   ```java
        String str = new String(codes, 0, codes.length);
        ```

-   所以为了避免这个问题，我们应该尽量避免使用 `char` 类型；使用的时候需要注意；

### 6.7. String API

-   https://docs.oracle.com/en/java/javase/11/docs/api/index.html

### 6.9. 构建字符串

-   `StringBuilder` 构建；
-   `StringBuilder` 从 `Java 5` 中引入；前身为 `StringBuffer` ，效率稍低，但是允许采用多线程方式添加和删除；两个类的 `API` 一样的；

## 7. 输入与输出

### 7.1. 读取输入

```java
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        String str = in.nextLine(); // 读取一行；next()；遇到空格就停止；...诸如还有 nextInt...
        System.out.println(str);
    }
}
```

>   输入可见；故 Scanner 类不适合读取密码； Java 6 引入 Console 类实现；

>   由于字符串是不可变的，所以不能更改字符串的内容，因为任何更改都会产生新的字符串，而如果你使用 `char[]` ，你就可以将所有元素设置为空白或零。 因此，在字符数组中存储密码可以明显降低窃取密码的安全风险

```java
import java.io.Console;

public class Main {
    public static void main(String[] args) {
        Console console = System.console();
        String username = console.readLine("username:");
        char[] pwd = console.readPassword("password:");
        System.out.println(username);
        for (char s : pwd) {
            System.out.print(s);
        }
    }
}
// 这个需要用 javac 编译后采用 java 运行；常见 idea 运行会报错；因为没有控制台；
// https://stackoverflow.com/questions/4203646/system-console-returns-null
```

### 7.2. 格式化输出

-    早起的 Java ，格式化数值曾经引起过争议；但是，`Java 5` 沿用了 C 语言中的函数库中的 `printf` 方法； 

-    可以为 `printf` 提供多个参数； 

    -   ```java
        System.out.printf("Hello, %s. Next year, you will be %d", name, age);
        ```
    
    -   ![000001-004.png](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2024/12/17341767700d0f11.png)
    
    -   ![000001-005.png](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2024/12/17341767805dd3fd.png)
    
    -   ```java
        public class Main {
            public static void main(String[] args) {
                System.out.printf("%,.2f\n", 10000/3.0);//3,333.33
                System.out.printf("%.2f\n", 10000/3.0);//3333.33
                System.out.printf("%08d\n", 10000/3); //00003333
            }
        }
        ```

-   亦可以用 `String.format` 方法；
-   也可以格式化时间，以 t 开始；

    ```java
    public class Main {
        public static void main(String[] args) {
            System.out.printf("%tc%n", new Date()); //周二 1月 03 21:44:28 CST 2023
            System.out.printf("%tT%n", new Date()); //21:44:28
        }
    }
    ```

    

![000001-006.png](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2024/12/173417685254f782.png)

-   可以用一个格式字符串指示需要格式化的参数索引；索引必须要紧跟在 % 之后，$ 结束； 

    ```java
    //time is : 2023-01-03 21:51:21
    System.out.printf("%1$s %2$tY-%2$tm-%2$td %2$tT","time is :", new Date()); 
    ```

    -   参数索引值从 1 开始；`%1$`... 对第一个参数进行格式化；


![000001-007.png](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2024/12/1734176925803a43.png)

-   数字和日期的格式化规则是特定于本地化环境的；

### 7.3. 文件输入与输出

-   读取文件，需要构造一个 `Scanner` 对象：

    ```java
    Scanner in = new Scanner(Path.of("text.txt"), StandardCharsets.UTF_8); // 指定 UTF-8 字符编码;如果省略，则会以默认编码，会导致不同机器上运行，可能会有不同的表现；
    ```

-   写入文件，需要构造一个 `PrintWriter`  对象：

    ```java
    PrintWriter out = new PrintWriter("text.txt", StandardCharsets.UTF_8);	
    ```

-   文件如果不存在，则会创建文件；

-   可以构造一个带有字符串参数的 `Scanner` ，但是这个会把字符串解释为数据，而并非文件名；

    ```java
    Scanner inScn = new Scanner("text.txt");
    while (inScn.hasNext()) {
    	System.out.println(inScn.next()); // 只输出了 text.txt
    }
    ```

-    同样，如果用一个不存在的文件构造一个 `Scanner` ，或者用一个无法创建的文件名构造一个 `PrintWriter` ；则会抛出异常；在 Java 中，该异常会被视为比 “被零除” 还要严重； 

## 8. 控制流程

>   Java 没有 `goto` 语句，但是 `break` 语句可以带标签；

### 8.1. 块作用域

-   块（`block`): 指的是若干条 Java 语句组成的语句，并且用一堆打括号括起来；
-   块确定了变量的作用域，一个块可以嵌套在另外一个块之中；

### 8.2. 条件语句

```java
if (condition)
    statement
    
if (condition)
    statement1
else 
    statement2
    
if (condition1)
    statement1
else if (condition2) 
    statement2
else 
    statement3
```

### 8.3. 循环

```java
while (condition)
    statement

do 
    statement
while (condition)
```

### 8.4. 确定循环

```java
for (int i = 0; i < 10; i++){
    ...
}

while(i > 10) {
    i++;
    ...
}
```

### 8.5. 多重选择：switch 语句

```java
switch (choice) {
    case 1:
        ...;
        break;
    case 2:
        ...;
        break;
    default:
		...
        break;
}
```

```java
switch (choice) {
    case 1:
        ...;
        break;
    case 2:
        ...;
        break;
    default:
		...
        break;
}
```

-    `switch` 为贯穿结构；如果没有 `break` ，则很危险； 

-    编译代码的时候 `javac -Xlint:fallthrough Test.java` 则如果某分支少一个 `break` 语句，编译器则会给出一个警告消息； 

    -    如果想要使用贯穿，则可以在外围方法加一个 `@SuppressWarnings("fallthrough")`； 

    -    `case` 标签可以是： 

        -   类型为 `char`,`byte`,`short`,`int`的常量表达式；

        -   枚举常量

        -   从 Java 7 开始，还可以是字符串字面量；

>   因为 switch 对应的 JVM 字节码 **lookupswitch、tableswitch** 指令**只支持 int 类型**。long转化成int会丢失精度，导致数据不准确，所以 Java 的 switch 有不允许使用 long 的逻辑规则。

### 8.6. 中断控制流程的雨具

-   尽管说，Java 设计者保留了 `goto` 关键字；但并没打算使用，但是其实无限制使用 `goto` 确实容易导致错误；但是在某些情况下，使用 `goto` 跳出循环，还是非常有意义的；因此  java 中有带标签的 `break` 语句；
-   标签放在希望跳出的最外层循环之前，且必须要紧跟一个冒号；
-   `continue` 略；

## 9. 大数

-   如果基本的整数和浮点数不能满足需求，可以采用 `BigInteger` 和 `BigDecimal` ；他们两个可以完成任意的精度计算；
-   其本质是十进制整数在转化成二进制数时不会有精度问题，那么把十进制小数扩大N倍让它在整数的维度上进行计算，并保留相应的精度信息

## 10. 数组

### 10.1. 声明数组

-   数组是一种数据结构，用来存储同一种类型值的集合；通过整型下标进行随机访问；

    ```java
    int[] a;
    // 也可以使用 
    int a[];
    // 大部分程序员使用第一种，因为可以将类型 int[] 与变量名分开；
    ```

    ```java
    // 创建数组对象并同时提供初始值的简写形式
    int[] a = {1,2,3};
    // 匿名数组
    new int[]{1,2,3};
    // 重新初始化一个数组且无须创建新变量；
    a = new int[]{1,2,3,4};
    // 是下列语句简写
    int[] anon = {1,2,3,4};
    a = anon;
    ```

    >   Java 中，允许长度为 0 的数组；

    ```java
    new elementType[0];
    new elementType[]{};
    ```

### 10.2. 访问数组元素

-   创建一个数字数组时，所有元素初始化为 0； 
-    创建一个 `boolean` 数组时，所有元素初始化为 `false`； 
-    创建一个对象数组时，所有元素初始化为 `null`; 
-    可以通过其下标进行访问； 

### 10.3. for each 循环

```java
for (variable : collection)
    statement;
```

-   `foreach` 循环会遍历数组的每个元素，而非下标志；

### 10.4. 数组拷贝

-   在 Java 中，允许将一个数组变量拷贝到另一个数组变量；这个时候，两个变量将会引用同一个数组； 

    ```java
    int[] copy = source;
    ```

-   如果希望一个数组的所有值拷贝到一个新的数组中去，就需要用 `Arrays` 的 `copyOf` 方法； 

    ```java
    // 第二个参数是新数组长度；如果长于，那么后面就会设置为数组默认值；相反，短的话只拷贝前面的值；
    int[] copy = Arrays.copyOf(source, source.length);
    ```

### 10.5. 命令行参数

```java
public static void main(String[] args) {
    ...
}
// 其中 args 表明 main 方法将接收一个字符串数组；也就是命令行上指定的参数；
// 以 java Demo -g a b;
// args : 0: -g, 1: a, 2: b;
```

### 10.6. 数组排序

-   可以采用 `Arrays.sort`  ；内部使用了优化的快排算法；

### 10.7. 多维数组

-   声明：

    ```java
    double[][] balances;
    ```

-   初始化：

    ```java
    balances = new double[N][N];
    ```

-   简写形式初始化：

    ```java
    int[][] seq = {
        {1,2,3},
        {1,2,3}
    };
    ```

-   亦可以用 `foreach` 循环遍历；

### 10.8. 不规则数组

```java
int[][] odds = new int[M][];
for(int n = 0; n < M; n++) {
    // 分配这些行
    odds[n] = new int[M];
}
```

