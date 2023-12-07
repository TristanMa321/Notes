## 数组

Java数组是一种基本的数据结构，用于存储固定数量的同类型元素。在Java中，数组被视为对象，因此它们可以存储基本数据类型（如`int`、`char`等）或对象（如字符串、对象等）。以下是关于Java数组的一些详细点：

1. **声明数组**：
   - 可以使用方括号`[]`来声明数组。例如，`int[] myArray;`声明了一个整数类型的数组。
   - 也可以在变量名之后放置方括号，例如`int myArray[];`，但这种方式不太推荐。

2. **创建数组**：
   - 使用`new`关键字来创建数组的实例。例如，`myArray = new int[10];`创建了一个可以存储10个整数的数组。
   - 在数组创建时，必须指定数组的大小。

3. **初始化数组**：
   - 在声明数组时可以同时进行初始化，例如`int[] myArray = {1, 2, 3, 4, 5};`。
   - 也可以在创建数组后逐个设置元素的值，例如`myArray[0] = 1; myArray[1] = 2;`等。

4. **数组长度**：
   - 使用`length`属性来获取数组的长度，例如`int arrayLength = myArray.length;`。

5. **遍历数组**：
   - 可以使用循环（如for循环或增强型for循环）来遍历数组的元素。

6. **多维数组**：
   - Java支持多维数组，例如二维数组。声明方式类似于`int[][] my2DArray = new int[10][20];`，其中10和20分别表示行和列的数量。

7. **数组的限制**：
   - 数组的大小一旦定义，就无法更改。如果需要动态大小的数组，可以考虑使用`ArrayList`等集合类。
   - 数组只能存储同一类型的数据。

8. **数组与内存**：
   - 数组在内存中是连续存储的。
   - 对于基本类型的数组，直接存储值；对于对象数组，存储的是对象的引用。

### 对象数组

- 对象数组存储对象的引用，而不是对象本身。
- 例如：`String[] names = new String[10];` 创建了一个可以存储10个字符串引用的数组。
- 对于自定义类，例如`Book`，数组`Book[] books = new Book[4];`创建了一个可以存储4个`Book`对象引用的数组。

# 多态（poly）

1.方法或对象具有多种形态



# 接口（implements）

```java
package interface_;

public interface Usb {
    public int n1 = 10;
    //接口的相关方法
    public void start();
    public void stop();
    //jdk8后，可以用默认实现方法，需要使用default关键字修饰
    default public void ok() {
        System.out.println("ok");
    }
}

```

## 1.细节

1.接口不能被实例化

2.接口所有方法都是public方法，接口中抽象方法，可以不用abstract修饰

3.一个普通类实现接口，必须把接口的所有方法都实现（抽象类除外）

4.一个类可以同时实现多个接口

5.接口的属性，默认用public static final修饰（final： 属性不可改变）

6.接口不能继承其他的类，但是可以继承多个别的接口

## 2.思考题

<img src="E:\笔记Note\JavaNote_MD\imgs\image-20231123105940588.png" style="zoom:50%;" />

答案：对对对，都可以使用

## 3.理解接口

1.当子类继承了父类，自动拥有父类的工能

2.如果子类需要扩展功能，可以通过实现接口的方式扩展

3.可以理解 实现接口 是对java 单继承机制的一种补充

## 4.其他

### 1)多态传递

```java
public class InterfacePolyPass {
    public static void main(String[] args) {
        //接口类型的变量可以指向，实现了该接口的类对象实例
        IG ig = new Teacher();
        //多态传递现象
        IH ih = new Teacher();
    }
}

interface IH{}
interface IG extends IH{}
class Teacher implements IG{}
```

# 内部类

## 1.定义

嵌套关系

![](E:\笔记Note\JavaNote_MD\imgs\image-20231123141325524.png)

## 2.分类

### 1)定义在外部类局部位置（比如在方法内）

#### 	1.局部内部类（有类名）

​	 

```java
public class LocalInnerClass {
    public static void main(String[] args) {
        //调用方法，品味其中的过程
        outer02 outer02 = new outer02();
        outer02.m1();
    }
}

class outer02{
    private int n1 = 100;
    public void m1() {
        //不能添加访问修饰符，但可以使用final修饰(final修饰class: 不能被继承)
        //作用域：仅仅在定义它的方法或代码快中
        final class Inner02 {
            //可以直接访问外部类的所有成员，包含私有的
            public void f1(){
                System.out.println(n1);
            }
        }
        //在外部类的方法中， 可以创建内部类对象
        Inner02 inner02 = new Inner02();
        inner02.f1();
    }
}
```

​	其他细节：a.外部其他类 不能访问 局部内部类（因为相当于一个局部变量）

​			  b.如果外部类和局部类的成员重名是，默认遵循就近原则，

​			     如果想访问外部类的成员，则可以使用（外部类型.this.成员）

#### 	2.匿名内部类（无类名）

匿名内部类是Java中的一个概念，它允许你在创建对象的同时定义一个类。这种类没有显式地命名，因此称为“匿名”。通常，匿名内部类用于创建只需在一个地方使用的简单类或接口实例。

这个概念经常与接口一起使用。例如，如果你需要实现一个接口，但只需要在某个特定的地方使用一次，你可以使用匿名内部类来实现这个接口，而不必创建一个单独的类。这样可以减少代码量并使代码更加紧凑。

示例代码可能如下所示：

```java
interface MyInterface {
    void doSomething();
}

public class MyClass {
    public void performAction() {
        // 使用匿名内部类实现接口
        MyInterface myObject = new MyInterface() {
            @Override
            public void doSomething() {
                System.out.println("Doing something!");
            }
        };

        // 调用方法
        myObject.doSomething();
    }
}

```



其他细节

```java
public class AnonymosInnerClassDetail {
    public static void main(String[] args) {
        outer outer = new outer();
        outer.f1();
    }
}

class outer{
    public void f1() {
        person person = new person(){
            @Override
            public void test() {
                System.out.println("内部类");
            }
        };
        person.test();

        new person(){
            @Override
            public void test() {
                System.out.println("第二种方法");
            }
        }.test();
    }
}

class person{
    public void test(){
        System.out.println("test");
    }
}
```



## 使用场景

1.匿名类直接作为方法参数传入

```java
public class InnerClassExercise01 {
    public static void main(String[] args) {
        f1(new AA() {
            @Override
            public void cry() {
                System.out.println("我在哭");
            }
        });
    }
    public static void f1(AA aa) {
        aa.cry();
    }
}

interface AA{
    public void cry();
}
```

2.如果用传统方法

```java
public class InnerClassExercise01 {
    public static void main(String[] args) {
        f1(new I());
    }
    public static void f1(AAA aaa) {
        aaa.cry();
    }
}

class I implements AAA{
    @Override
    public void cry() {
        System.out.println("我在哭");
    }
}
interface AAA{
    public void cry();
}
```



再来一个案例

```java
public class InnerClassExercise02 {
    public static void main(String[] args) {
        CellPhone cellPhone = new CellPhone();
        cellPhone.alarmclock(new Bell() {
            @Override
            public void ring() {
                System.out.println("懒猪起床了");
            }
        });
        cellPhone.alarmclock(new Bell() {
            @Override
            public void ring() {
                System.out.println("小伙伴上课了");
            }
        });
    }
}

interface Bell{
    void ring();
}
class CellPhone{
    public void alarmclock(Bell bell){
        bell.ring();
    }
}
```



### 2)定义在外部类的成员位置上

​	1.成员内部类（不用static修饰）

​	2.静态内部类（使用static修饰）



# 代码块

## 1.定义（构造器的补充）

作用：主要是初始化操作

类似于方法，将逻辑语句封装在方法体中，通过{}包围起来。

但和方法不同，没有方法名，没有返回，没有参数，只有方法体，而且不用通过对象或类显式调用，而是加载类时，或创建对象时隐式调用。

分类:使用static 修饰的叫静态代码块，没有static修饰的，叫普通代码块

## 2.细节

1.静态代码块，作用就是对类进行初始化，而且它随着类的加载而执行，并且只会执行一次。

   如果是普通代码块，每创建一个对象，就执行。如果只是使用类的静态成员时，普通代码块并不会执行

2.静态代码块只能调用静态成员，普通代码块可以调用所有

调用顺序:

1.调用静态代码块和静态属性初始化时，静态代码块和静态属性初始化调用的优先值一样，看定义顺序即可

2.调用普通代码块和普通属性的初始化时，同样看定义顺序

3.

### 补充-类什么时候被加载

  1.创建对象实例时（new）

  2.创建子类对象实例，父类也会被加载

  3.使用类的静态成员时（静态属性，静态方法）

## 饿汉式VS懒汉式

1.二者最主要的区别在于创建对象的时机不同：饿汉式是在类加载就创建了对象实例，而懒汉式是在使用时才创建。

2饿汉式不存在线程安全问题，懒汉式存在线程安全问题.

3.饿汉式存在浪费资源的可能。因为如果程序员一个对象实例都没有使用，那么饿汉式创建的对象就浪费了，懒汉式是使用时才创建，就不存在这个问题。

4.在我们javaSE标准类中，java.lang.Runtime就是经典的单例模式。

```java
public class SingleDesignForm {
    public static void main(String[] args) {
        System.out.println(Girlfriend.getInstance());
    }
}
//单例模式，一个类只能有一个实例
//GirlFriend类只能有一个女朋友对象
class Girlfriend {
    private String name;
    //步骤[单例模式-饿汉式]
    //1.将构造器私有化
    //2.在类的内部直接创建对象（static）
    //3.提供一个公共的static对象，返回对象
    private static Girlfriend gf = new Girlfriend("lili");
    private Girlfriend(String name) {
        this.name = name;
    }
    public static Girlfriend getInstance(){
        return gf;
    }

    @Override
    public String toString() {
        return "Girlfriend{" +
                "name='" + name + '\'' +
                '}';
    }
}
```

 

```java
//懒汉式
class Girlfriend02{
    private String name;
    //步骤
    //1.构造器私有化
    //2.定义一个static静态属性对象
    //3.提供一个 public static方法，可以返回对象
    //4.只有当用户使用getInstance时，才返回对象，后面再次调用的时候，会返回上次创建的对象
    private static Girlfriend02 gir;

    private Girlfriend02(String name) {
        this.name = name;
    }
    public static Girlfriend02 getInstance(){
        if (gir == null){
            gir = new Girlfriend02("lili");
        }
        return gir;
    }

    @Override
    public String toString() {
        return "Girlfriend02{" +
                "name='" + name + '\'' +
                '}';
    }
}
```



## Final关键词

final 中文意思：最后的，最终的

final 可以修饰类、属性、方法和局部变量。表示不能修改

### 细节

1.final修饰的属性又叫常量，一般用XX_XX命名

2. final修饰的属性在定义时，必须赋初值，并且以后不能再修改，赋值可以在如下位置之一【选择一个位置赋初值即可】：
   1. ﻿定义时：如 public final double TAX_RATE=0.08；
   2. ﻿在构造器中
   3. ﻿在代码块中

## 抽象类

### 定义

当父类的某些方法，需要声明，但是又不确定如何实现时，可以将其声明为抽象方法，那么这个类也必须声明为抽象类

### 细节

1） 抽象类不能被实例化

2）抽象类不一定要包含abstract方法。也就是说，抽象类可以没有abstract方法

3） 一旦类包含了abstract方法，则这个类必须声明为abstract

4） abstract只能修饰类和方法，不能修饰属性和其它的

5）如果一个类继承了抽象类，则它必须实现抽象类的所有抽象方法，除非它自己也声明为abstract类。

6）抽象方法不能使用private、final 和 static来修饰，因为这些关键字都是和重写相违背的

### 实践-模版设计模式

```java
public class TestTemplate{
    public static void main(String[] args) {
        AA aa = new AA();
        aa.caleTimes();
        BB bb = new BB();
        bb.caleTimes();
    }
}
abstract class Template {
    public abstract void job();
    public void caleTimes(){
        double start = System.currentTimeMillis();
        job();
        double end = System.currentTimeMillis();
        System.out.println("耗时："+(end - start));
    }
}
class AA extends Template{
    @Override
    public void job() {
        for (int i = 0; i < 1000000000; i++) {
            i += i;
        }
    }
}
class BB extends Template{

    @Override
    public void job() {
        for (int i = 0; i < 1000000000; i++) {
            i *= i;
        }
    }
}
```

# "==" 和equal的区别

"=="：

1.既可以判断基本类型，又可以判断引用类型

2.如果判断基本类型，判断值是否相等

3.如果判断引用类型，判断地址是否相等，即判断是不是同一个对象

equal

1.只能用于引用类型

2.特殊：String类重写了equal方法，比的是字符串的值，而不再是地址了

# 常用类

## 1.包装类

### 特点

有了类的特点，可以调用类的方法

### 分类

<img src="E:\笔记Note\JavaNote_MD\imgs\image-20231203184123063.png" alt="image-20231203184123063" style="zoom:50%;" />

​	前两个父类是object,后面父类是Number, Number的父类是object

### 和基本类型的转换

1） jdk5 前的手动装箱和拆箱方式。装箱：基本类型->包装类型，反之，拆箱

2） jdk5 以后（含jdk5）的自动装箱和拆箱方式

3） 自动装箱底层调用的是valueOf方法，比如Integer.valueOf（）

```java
public class Wrapper01 {
    //手动装箱，拆箱
    int a = 1;
    Integer a1 = new Integer(a);
    int a2 = a1.intValue();

    //自动装箱、拆箱
    int b = 1;
    Integer b1 = b;
    int b2 = b1;
}
```



### 和String类型的转换

```java
public class WrapperToString {
    //Integer -> String
    Integer i = 0;
    //method1
    String s1 = i.toString();
    //method2
    String s2 = String.valueOf(i);
    //method3
    String s3 = i + "";
    
    //String -> Integer
    Integer j = new Integer(s1);
    Integer j2 = Integer.valueOf(s1);
}
```



## 2.String类

### 常用方法：

equals

equalsignoreCase 

length 

indexOf：获取字符在字符串中第1次出现的索引.索引从0开始.如果找不到，返回-1

lastIndexOf

substring

trim
 charAt：获取某索引处的字符，注意不能使用Str［index］这种方式

﻿toUpperCase

﻿toLowerCase

﻿concat

﻿﻿compareTo

﻿﻿toCharArray

﻿﻿format

## 3.Arrays类

1.常用方法

.toString

.sort

.toCharArray: 转换成字符数组

.compareTo 比较

源码：

```java
 public int compareTo(String anotherString) {
        int len1 = value.length;
        int len2 = anotherString.value.length;
        int lim = Math.min(len1, len2);
        char v1[] = value;
        char v2[] = anotherString.value;

        int k = 0;
        while (k < lim) {
            char c1 = v1[k];
            char c2 = v2[k];
            if (c1 != c2) {
                return c1 - c2;
            }
            k++;
        }
        return len1 - len2;
    }
```



## StringBuffer

### 1.定义

可变的字符序列，可以对字符串内容进行增删，不改变指向地址

### 2.与String之间转换

1）构造器直接传

2）stringBuffer.append / stringBuffer.toString() 方法

### 3.常用方法

1. append
2. delete
3. replace
4. insert
5. length 
6. indexOf
7. lastIndexOf

## StringBuilder

### 1.定义

一个可变的字符序列，和\



## String Builder Buffer三者使用原则

使用的原则，结论：

如果字符患存在大量的修改操作，一般使用 StringBuffer 或StringBuilder

如果字符串存在大量的修改操作，并在单线程的情况，使用 StringBuilder

如果字符串存在大量的修改操作，并在多线程的情况，使用 StringBuffer

如果我们字符串很少修改，被多个对象引用，使用String，比如配置信息等

### 常用方法

1. binarySearch:通过二分搜索法查找，要求必须排好序

2. copyOf：数据元素的复制

   


   ```java
   Integer[] integers = Arrays.copyOf(arr, arr.length);
   ```

3. fill:

   源码：

   


   ```java
   public static void fill(int[] a, int val) {
           for (int i = 0, len = a.length; i < len; i++)
               a[i] = val;
       }
   ```

4. equals

5. asList

## System类



## BigInteger和BigDecimal类



# 集合

## 特点

1. 可以动态保存任意多个对象

## 分类

双列集合

![image-20231207151440617](E:\笔记Note\JavaNote_MD\assets\image-20231207151440617.png)

单列集合（k,v）

![image-20231207151513937](E:\笔记Note\JavaNote_MD\assets\image-20231207151513937.png)

## Iterator遍历

### Java Iterator 接口概述

- **用途**：`Iterator` 接口提供了一种遍历集合（如`List`、`Set`）元素的标准方式。
- **位置**：位于 `java.util` 包中。

### 主要方法

1. **`hasNext()`**：
   - **类型**：`boolean`
   - **用途**：检查序列中是否还有元素。
   - **返回**：如果迭代有更多的元素，则返回 `true`；否则返回 `false`。

2. **`next()`**：
   - **类型**：`E`（泛型）
   - **用途**：返回迭代中的下一个元素。
   - **返回**：序列中的下一个元素。
   - **注意**：在调用 `next()` 之前应该调用 `hasNext()`，以避免 `NoSuchElementException`。

3. **`remove()`**：
   - **用途**：从集合中移除由 `next()` 方法返回的最后一个元素（可选操作）。
   - **注意**：如果在迭代期间修改集合（除了通过 `Iterator` 自己的 `remove` 方法），通常会导致 `ConcurrentModificationException`。

### 使用示例

假设有一个 `List<String>`，使用 `Iterator` 遍历如下：

```java
List<String> list = Arrays.asList("Apple", "Banana", "Cherry");
Iterator<String> it = list.iterator();

while (it.hasNext()) {
    String item = it.next();
    System.out.println(item);
}
```

### 特点和注意事项

- **通用性**：`Iterator` 是一个通用的遍历接口，适用于所有 `Collection` 实现。
- **单向迭代**：`Iterator` 仅支持向前遍历。
- **安全删除**：通过 `Iterator` 的 `remove()` 方法可以安全地删除元素，而不会引起并发修改异常。
- **无法修改元素**：`Iterator` 只能删除元素，不能修改集合中的元素。
- **并发修改**：在使用迭代器的过程中，如果集合被其他方式修改，可能会抛出 `ConcurrentModificationException`。

## 增强for循环

### Java 增强for循环概述

- **用途**：增强for循环是Java 5引入的一种简化数组和集合遍历的语法。
- **适用范围**：适用于遍历数组或任何实现了 `Iterable` 接口的集合类（如 `List`、`Set`）。

### 基本语法

增强for循环的基本格式如下：

```java
for (声明类型 变量名 : 遍历对象) {
    // 循环体
}
```

其中，“声明类型”是遍历对象中元素的类型，“变量名”是循环中使用的变量名称，而“遍历对象”是要遍历的数组或集合。

### 使用示例

1. **遍历数组**：

    ```java
    int[] numbers = {1, 2, 3, 4, 5};
    for (int num : numbers) {
        System.out.println(num);
    }
    ```

2. **遍历集合**：

    ```java
    List<String> fruits = Arrays.asList("Apple", "Banana", "Cherry");
    for (String fruit : fruits) {
        System.out.println(fruit);
    }
    ```

### 优点

- **简洁性**：相比传统的for循环，增强for循环的代码更简洁、更易读。
- **减少错误**：自动处理索引和迭代，减少了编程错误，如数组越界等。
- **无需迭代器**：不需要显式使用迭代器或索引变量。

### 注意事项

- **单向遍历**：只能进行单向顺序遍历，不能反向遍历或修改遍历顺序。
- **无法修改集合**：不能用来直接添加或删除集合中的元素。
- **局部变量**：循环变量是局部变量，对它的任何修改都不会影响原始集合或数组。
- **并发修改**：在遍历过程中，不能修改集合的结构（添加、删除元素），否则会抛出 `ConcurrentModificationException`。

### 适用场合

增强for循环非常适合在不需要修改集合或数组，只需要读取元素时使用。它使得代码更加简洁，更易于维护。

### 对比传统for循环

- 传统for循环提供更多的控制能力，比如可以控制循环的起始和结束条件，可以逆序遍历，也可以修改集合。
- 增强for循环主要用于简化代码和提高可读性，特别是当遍历顺序和集合/数组本身的修改不是关键因素时。

通过使用增强for循环，你可以有效地减少代码量，并使代码更加清晰易懂。
