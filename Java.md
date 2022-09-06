![1661847996368](C:\Users\HuiBBao\AppData\Roaming\Typora\typora-user-images\1661847996368.png)

# Java基础

**1. 面向对象的三个基本特征：封装、继承、多态**

- 封装：隐藏部分对象的属性和实现细节，对数据的访问只能通过公开的接口，以防程序中无关的部分意外改变了对象的私有部分。
- 继承：子类继承父类的特征和行为，使子类对象具有父类的实例域和方法。
- 多态：对于同一个行为，不同的子类对象具有不同的表现形式，多态存在的3个条件：继承、重写、父类引用指向子类对象。



**2. JDK和JRE的区别**

- JDK是Java Development Kid的简称，意思是java开发工具包，提供了java的开发环境和运行环境
- JRE是Java Runtime Environment的简称，意思是java的运行环境，为java的运行提供了所需环境
- JDK包含了JRE



**3. 访问修饰符public、private、protected、不写的区别**

   - public：公有类型，修饰的变量在 当前类、同一个包、子类、其他包 都可以访问。
   - protected：保护类型，修饰的变量在 当前类、同一个包、子类 可以访问。
   - 默认（不写）：修饰的变量在 当前类、同一个包 可以访问。
   - private：私有类型，修饰的变量只能在当前类接受访问。



**4. String是基本数据类型吗？**

​       String不是基本数据类型，Java的基本数据类型有byte、short、int、long、char、boolean、float、double，除了这些剩下的都是Java的引用类型。基本类型的数据存储在栈上，而引用类型的数据存储在堆上，栈中只存放引用地址。



**5. 下面两个代码块能正常编译和运行吗？**

```java
// 代码块1
short s1 = 1; s1 = s1 + 1;
// 代码块2
short s1 = 1; s1 += 1;
```

代码块1编译报错，错误原因 不兼容的类型，从int转换到short可能会有损失。

代码块2正常编译和运行。

因为1是int类型，所以和short类型运算结果也应该是int类型，不能直接赋值给short，需要强制类型转换，而s1+=1的底层含有隐式的强制类型转换，相当于s1=（short）s1 + 1。



**6. 指出下面代码的输出结果**

```java
public static void main(String[] args) {
    Integer a = 128, b = 128, c = 127, d = 127;
    System.out.println(a == b);
    System.out.println(c == d);
}
```

第一个输出是false，第二个输出是true。

Integer是包装类，从int类型到包装类的转换称自动装箱，在Integer中引入了IntegerCache来缓存一定范围的值，IntegerCache的范围默认是-128~127，因为a和b没有命中这个范围，所以它们是不同的对象。

```java

public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
```



**7. 用最有效的方法计算5乘以8**

​        5乘以8 相当于 5乘以2的3次方，也相当于将5左移3位，使用二进制移位计算时，左移n位相当于乘以2的n次方，右移n位相当于除以2的n次方，但在实际开发中一般不使用，因为很多编译器会自动帮我们转换为移位计算。



**8. &和&&的区别**

- 单个&符号可用作逻辑与计算和按位与计算，它用作按位与计算时，两个二进制位必须同时为1结果才为1，否则结果为0，用作逻辑与计算时，两边表达式的值应同时为true，结果才为true，否则为false。
- 两个&符号和单个&符号的逻辑与计算用法一样，但它多了短路的功能，当左侧表达式的值为false时，不再去判断右侧表达式的值，直接得到结果false。



**9. == 和 equals 的区别**

- ==符号，当两边都为基本数据类型时，比较他们的值是否相等；当两边为引用时，比较他们的内存地址
- equals函数：在==的基础上，增加了对其引用值的比较，它会首先去比较两个引用的内存地址是否一致，若一致则直接返回true，若不一致，则比较它们的值是否相等



**10. String类可以被继承吗？**

不可以，String类被final修饰，被final关键字修饰的类为最终类，不可以被继承。



**11. final关键字**

- final修饰的类是最终类，不能被继承。
- final修饰的方法不能被重写。
- final修饰的变量为常量，必须初始化。



**12. 两个对象的hashCode()相同，则equals()也一定为true，对吗？**

​        不对，两个对象值相等时，hashCode()必然相等，但反过来，hashCode()相同时，两个对象不一定相等，只能说明这两个对象在散列存储结构中，存放于同一个位置。

- 注：hashCode方法的通用契约，该契约规定相等的对象必须具有相等的哈希码。



**13. hashCode是什么？**

​         每个对象都有一个物理地址，通过这个物理地址得到一个整数，再通过hash函数算法得到hashcode，所以说hashCode就是对象在hash表中对应的位置。



**14. 类中的构造器可以被重写吗？**

不可以，构造器不能被继承，所以不能被重写，但是可以被重载



**15. 重载和重写的区别？**

两个都是实现多态的方式，区别在于重写实现的是运行时的多态性，重载实现的是编译时的多态性

- 重写（override）：重写发生在子类和父类之间，要求子类方法与父类中被重写的方法方法名一致，返回类型一致，子类方法中声明的异常应少于父类。
- 重载（overload）：在一个类中，方法名相同、参数列表不同的两个方法即是重载，参数列表不同指的是参数的类型不同和参数的数量不同，或者两者都不同，只有返回类型不同不能看作重载。



**16. 为什么只有返回类型不同的两个方法不能看作重载？**

因为在单纯的方法调用时，编译器不能区分调用的是哪一个方法。



**17. Java中操作字符串的都有哪些类？它们之间有什么区别？**

Java中操作字符串的类有String、StringBuffer和StringBuilder。

- String和StringBuffer、StringBuilder的区别在于，String声明的是不可变的对象，每一次操作都会产生新的String对象，而StringBuffer和StringBuilder是可以在原有对象的基础上进行操作。
- StringBuffer和StringBuilder最大的区别在于StringBuffer是线程安全的，StringBuilder是非线程安全的，但StringBuilder 的性能高于StringBuffer。所以在单线程中推荐使用StringBuilder，在多线程环境下推挤使用StringBuffer。



**18. Java中的Math.round(-2.6)等于多少？**

等于-3，Math.round方法是在原有数字上加上0.5，然后向下取整，-2.6加上0.5等于-2.1，向下取整即是-3。



**19. 内存中 栈（stack）、堆（heap）和方法区（method area）的用法？**

- 栈：存放对象的引用，每个线程都有自己的栈空间。
- 堆：存放所有通过new关键字或构造器创建的对象，是所有线程共享的内存空间，也是垃圾收集器管理的主要区域。
- 方法区：存放类信息、成员方法，方法区包含常量池，常量池存放字面量和被static修饰的成员。方法区也是所有线程共享的内存空间。



**20. String s = new String("xyz") 创建了几个字符串对象？**

一个或两个

- 当常量池没有"xyz"时，则会创建两个对象，一个是和"xzy"对应的、驻留在字符串常量池中作全局共享的实例，在jdk1.6之前，该实例是创建在字符串常量池中，而在jdk1.7之后，该实例是在堆中，字符串常量池中只放引用。 另一个是通过 new String() 创建并初始化的，内容与"xyz"相同的实例，也是在堆中。 
- 当常量池已经有"xyz"，就只创建通过 new String() 创建并初始化的、内容与"xyz"相同的实例。

注：jdk1.7之后，字符串常量池被单独移到了堆中，而它此前是在方法区中。参考博客： [(54条消息) Java 常量池详解（一）字符串常量池_new hilbert()的博客-CSDN博客_字符串常量池](https://blog.csdn.net/Prior_SX/article/details/123463430?ops_request_misc=%7B%22request%5Fid%22%3A%22166243443716782427412460%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=166243443716782427412460&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-1-123463430-null-null.142^v46^pc_rank_34_queryrelevant25&utm_term=java 字符串常量池和常量池&spm=1018.2226.3001.4187) 



**21. String s = "xyz" 和 String s = new String("xyz") 区别？**

两个语句都会先去字符串常量池中检查是否已经存在 “xyz”，如果有则直接使用，如果没有则会在常量池中创建 “xyz” 对象。

另外，String s = new String("xyz") 还会通过 new String() 在堆里创建一个内容与 "xyz" 相同的对象实例。

所以前者其实理解为被后者的所包含。



**22. 下面代码的输出是？ **

```java
public void func12() {    
    String s1 = "Programming";    
    String s2 = new String("Programming");    
    String s3 = "Program";    
    String s4 = "ming";    
    String s5 = "Program" + "ming";    
    String s6 = s3 + s4;    
    System.out.println(s1 == s2); // false    
    System.out.println(s1 == s5); // true
    System.out.println(s1 == s6); // false
    System.out.println(s1 == s6.intern()); // true    
    System.out.println(s2 == s2.intern()); // false
}
```

从上往下分别是false、true、false、true、false。

首先需要知道java中字符串拼接是如何实现的。有两种情况：

- 若干个字符串常量（比如"a"）或者常量引用（用final修饰的字符串引用，比如final String str = “a”）直接用“+”号进行连接。这种情况是在编译期就会进行优化，比如String s5 = "Program" + "ming"，编译器会直接优化为String s5 = "Programming"；
- 除了第一点以外的其他情况的字符串拼接。其内部的实现原理实际上是先创造一个StringBuilder对象，用于盛装所有我们所需要拼接的字符串，对每个字符串都调用一次append( )方法，最后再调用toString( )方法，生成字符串拼接完成的结果。

例：

String ss = "ok" + s + "xyz" + 5; jad反编译得到：

```java
String ss = (new StringBuilder("ok")).append(s).append("xyz").append(5).toString();
```

String s6 = s3 + s4; jad反编译得到：

```java
String s6 = new StringBuilder(String.valueOf(s3)).append(new StringBuilder(String.valueOf(s4))).toString()
```



其次需要知道 "==" 号两边为引用时，比较的是引用地址是否一致。

最后是String的intern()方法，下面是其底层代码的注释

```java
/**
* When the intern method is invoked, if the pool already contains a string equal to this * String object as determined by the equals(Object) method, then the string from the pool * is returned. Otherwise, this String object is added to the pool and a reference to this * String object is returned
*/
```

意思是：当调用 intern 方法时，如果池中已经包含一个由 equals(Object) 方法确定等于该 String 对象的字符串，则返回池中的字符串。否则，将此 String 对象添加到池中并返回对该 String 对象的引用。

接下来看代码：

- s1 == s2：s1指向常量池中的"Programming"实例，s2指向通过new String()创建出来存放在堆中的"Programming"实例，所以引用地址不一致，输出false。
- s1 == s5：因为s5是若干个字符串常量直接使用"+"号连接，编译器会将其优化，所以与s1一样，都是指向常量池中的"Programming"实例，输出true。
- s1 == s6：由于s6是上述字符串拼接的第二种情况，最后调用的toString()方法return的是一个new String()对象，所以s6指向堆内存中的"Program"实例，而s1指向常量池中"Programming"实例，固输出false。
- s1 = s6.intern()：对于s6.intern()，由于池中已经包含了"Programming"字符串，所以s6.intern()返回的是池中的字符串，而s1也是指向池中的"Programming"字符串，所以输出true。
- s2 = s2.intern()：对于s2.intern()，由于池中已经包含了"Programming"字符串，所以s2.intern()返回的是池中的字符串，而s2是指向堆中的"Programming"字符串，所以输出false。



**23. 如何将字符串反转？**

使用StringBuilder或者StringBuffer的reverse()方法。底层代码：

```java
    public AbstractStringBuilder reverse() {
        boolean hasSurrogates = false;
        int n = count - 1;
        for (int j = (n-1) >> 1; j >= 0; j--) {
            int k = n - j;
            char cj = value[j];
            char ck = value[k];
            value[j] = ck;
            value[k] = cj;
            if (Character.isSurrogate(cj) ||
                Character.isSurrogate(ck)) {
                hasSurrogates = true;
            }
        }
        if (hasSurrogates) {
            reverseAllValidSurrogatePairs();
        }
        return this;
    }
    private void reverseAllValidSurrogatePairs() {
        for (int i = 0; i < count - 1; i++) {
            char c2 = value[i];
            if (Character.isLowSurrogate(c2)) {
                char c1 = value[i + 1];
                if (Character.isHighSurrogate(c1)) {
                    value[i++] = c1;
                    value[i] = c2;
                }
            }
        }
    }
```



**24. String类常用的方法有哪些？**

- indexOf()：返回指定字符的索引。
- charAt()：返回指定索引处的字符。
- replace()：字符串替换。
- trim()：去除字符串两端空白。
- split()：分割字符串，返回一个分割后的字符串数组。
- getBytes()：返回字符串的 byte 类型数组。
- length()：返回字符串长度。
- toLowerCase()：将字符串转成小写字母。
- toUpperCase()：将字符串转成大写字符。
- substring()：截取字符串。
- equals()：字符串比较。



**25. 普通类和抽象类有什么区别？**

- 普通类不能包含抽象方法，抽象类可以包含抽象方法
- 普通类可以直接被实例化，抽象类不能直接实例化



**26. 抽象类可以用final修饰吗？**

不可以，因为抽象类需要被继承，而用final修饰的类是最终类，不能被继承，这样就会产生矛盾。



**27. 接口和抽象类有什么区别？**

- 抽象类的子类使用extends来继承，接口必须使用implements来实现接口。

- 抽象类可以有构造方法，接口不能有。

- 抽象类可以有成员变量，接口只能有常量。

- 一个类可以实现很多个接口，而只能继承一个抽象类。

- 接口中的方法默认使用public修饰（Java9之后可以使用protected），而抽象类可以是任意的访问修饰符。

- 设计思想的区别：

  - 接口是自上而下的抽象过程，接口规范了某些行为，是对某一行为的抽象。我需要这个行为，我就去实现某个接口，但是具体这个行为怎么实现，完全由自己决定。

  - 抽象类是自下而上的抽象过程，抽象类提供了通用实现，是对某一类事物的抽象。我们在写实现类的时候，发现某些实现类具有几乎相同的实现，因此我们将这些相同的实现抽取出来成为抽象类，然后如果有一些差异点，则可以提供抽象方法来支持自定义实现。



**28. 当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递？**

值传递，Java中没有引用传递，对于这个对象参数，值的内容是对象的引用。



**29. Java静态变量和成员变量的区别？**

```java
public class Demo {
    /**
     * 静态变量：又称类变量，static修饰
     */
    public static String STATIC_VARIABLE = "静态变量";
    /**
     * 实例变量：又称成员变量，没有static修饰
     */
    public String INSTANCE_VARIABLE = "实例变量";
}
```

- 成员变量存放在堆中，而静态变量存放在方法区中。
- 成员变量与对象共存亡，随着对象创建而存在，随着对象被回收而释放，所以也成为实例变量；静态变量与类共存亡，随着类的加载而存在，随着类的消失而消失，所以也称为类变量。
- 成员变量只能被对象调用，静态变量可以被对象调用，也可以根据类名调用。



**30. Error和Exception的区别？**

Error 表示系统级的错误和程序不必处理的异常，是恢复不是不可能但很困难的情况下的一种严重问题，比如内存溢出，不可能指望程序能处理这样的情况。

Exception 表示需要捕捉或者需要程序进行处理的异常，是一种设计或实现问题，也就是说，它表示如果程序运行正常，从不会发生的情况。



**31. finally**

finally 是对 Java 异常处理机制的最佳补充，通常配合 try、catch 使用，用于存放那些无论是否出现异常都一定会执行的代码。在实际使用中，通常用于释放锁、数据库连接等资源，把资源释放方法放到 finally 中，可以大大降低程序出错的几率。 



**32. try、catch、finally考察1，指出下面代码的运行结果**

```java
public class TryDemo {
    public static void main(String[] args) {
        System.out.println(test());
    }
    public static int test() {
        try {
            return 1;
        } catch (Exception e) {
            return 2;
        } finally {
            System.out.print("3");
        }
    }
}
```

输出31，在 return 前会先执行 finally 语句块，所以是先输出 finally 里的 3，再输出 return 的 1。 



**33. try、catch、finally考察2，指出下面代码的运行结果**

```java
public class TryDemo {
    public static void main(String[] args) {
        System.out.println(test1());
    }
    public static int test1() {
        int i = 0;
        try {
            i = 2;
            return i;
        } finally {
            i = 3;
        }
    }
}
```

输出2，在执行 finally 之前，JVM 会先将 i 的结果暂存起来，然后 finally 执行完毕后，会返回之前暂存的结果，而不是返回 i，所以即使这边 i 已经被修改为 3，最终返回的还是之前暂存起来的结果 2。 



**34. 在Java中如何跳出多重循环？**

在需要跳出的循环前加一个标签，例如A，然后break A;

```java
    public void func8() {
        A: for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 10; j++) {
                if (j == 1) {
                    System.out.println(j);
                }
                for (int k = 0; k < 10; k++) {
                    if (k == 4) {
                        System.out.println(k);
                        break A;
                    }
                }
            }
        }
    }
```



**35. 普通数组和String获得length的方式**

数组通过length属性获得length，String通过length()方法获得length。



**36. switch中参数的适用类型？**

- Java5以前，switch中的参数只能是byte、short、int、char中的其中一种。
- Java5的时候，它也可以是enum枚举类型。
- Java7的时候，它还可以是String字符串类型。

但long在目前的所有Java版本中都是不可以作为switch中的参数的。



**37. int 和 Integer 的区别**

Java是一门纯洁的面向对象的编程语言，为了编程方便引入了基本的数据类型，为了能够将这些基本数据类型当成对象操作，Java为每一个基本数据类型引入了对应的包装类型，Integer就是基本数据类型int的包装类型。



**38. Java中有goto吗？**

有，在目前的Java版本中没有使用。goto是Java中的保留字，和const一样，是不能使用的关键字。



# 容器

**1. Java的容器都有哪些？**

 Java 容器分为 Collection 和 Map 两大类，其下又有很多子类 。

- Collection
  - List
    - ArrayList
    - LinkedList
    - Vector
    - Stack
  - Set
    - HashSet
    - LinkedHashSet
    - TreeSet
- Map
  - HashMap
    - LinkedHashMap
  - TreeMap
  - ConcurrentHashMap
  - Hashtable

