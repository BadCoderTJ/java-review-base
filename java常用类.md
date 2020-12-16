





## lang包

### 1、Object方法

### ![QQ截图20201214205401.png](https://i.loli.net/2020/12/15/dkowBW7Mu8baf1p.png)

> getClass(): 获取Class对象, 返回此 Object 的运行时类。 
>
> clone():
>
>  ① 实现Cloneable接口，这是一个标记接口，自身没有方法。 
>  ② 覆盖clone()方法，可见性提升为public。 
>
> equals：返回值类型boolean，比较两个对象是否相同
>
> hashCode：返回值类型int，返回对象的哈希码值
>
> toString：返回值类型String，返回对象的字符串表示形式
>
>  `在Obect类中有些方法使用native修改，native修饰示该方法的实现不是由java语言编写的，native可以与其他修饰符一起使用，但是不能与abstract一起使用，abstract表示该方式是抽象的，不能有方法体，而native虽然没有写方法体，实质是存在方法体的。` 

```java
Person p1 = new Person(1001, "AA");
System.out.println(p1.getClass());
Method[] methods = p1.getClass().getMethods();
for (Method method : methods) {
    System.out.println(method);
}
```

```java
@Data
public class Person implements Cloneable {
    private String name;
    private Integer age;
    private Address address;
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
 
@Test
public void testShallowCopy() throws Exception{
  Person p1=new Person();
  p1.setAge(31);
  p1.setName("Peter");
 
  Person p2=(Person) p1.clone();
  System.out.println(p1==p2);//false
  p2.setName("Jacky");
  System.out.println("p1="+p1);//p1=Person [name=Peter, age=31]
  System.out.println("p2="+p2);//p2=Person [name=Jacky, age=31]
}
```

### 2、包装类

 Boolean，Character，Byte，Short，Integer，Long，Float，Double 

| 基本类型 | 包装类    | 字节(byte) | 位数(bit) | 范围                       |
| -------- | --------- | ---------- | --------- | -------------------------- |
| boolean  | Boolean   | N/A        |           |                            |
| byte     | Byte      | 1 字节     | 8 位      | -128 ~ 127                 |
| char     | Character | 2 字节     | 16 位     | Unicode0 ~ Unicode(2^16)-1 |
| short    | Short     | 2 字节     | 16 位     | -2^15 ~ 2^15 - 1           |
| int      | Integer   | 4 字节     | 32 位     | -2^31 ~ 2^31 - 1           |
| long     | Long      | 8 字节     | 64 位     | -2^63 ~ 2^63 - 1           |
| float    | Float     | 4 字节     | 32 位     | IEEE754 ~ IEEE754          |
| double   | Double    | 8 字节     | 64 位     | IEEE754 ~ IEEE754          |

> 注意： 如果i在[-128,127]集合内，返回指向的是IntegerCache.cache中已经存在的对象的引用，否则创建一个新的Integer对象，源码如下：

```java
//IntegerCache.high = 127
public static Integer valueOf(int i) {
        if(i >= -128 && i <= IntegerCache.high){
            return IntegerCache.cache[i + 128];
        }else{
            return new Integer(i);
        }
}
```

### 3、字符串

 String ，StringBuilder， StringBuffer 

1.首先说运行速度，或者说是执行速度，在这方面运行速度快慢为：StringBuilder > StringBuffer > String

原因：String为字符串常量，而StringBuilder和StringBuffer均为字符串变量，即String对象一旦创建之后该对象是不可更改的，但后两者的对象是变量，是可以更改的

Java中对String对象进行的操作实际上是一个不断创建新的对象并且将旧的对象回收的一个过程，所以执行速度很慢。

而StringBuilder和StringBuffer的对象是变量，对变量进行操作就是直接对该对象进行更改，而不进行创建和回收的操作，所以速度要比String快很多

2.线程安全

在线程安全上，StringBuilder是线程不安全的，而StringBuffer是线程安全的

如果一个StringBuffer对象在字符串缓冲区被多个线程使用时，StringBuffer中很多方法可以带有**synchronized**关键字，所以可以保证线程是安全的，但StringBuilder的方法则没有该关键字，所以不能保证线程安全，有可能会出现一些错误的操作。所以如果要进行的操作是多线程的，那么就要使用StringBuffer，但是在单线程的情况下，还是建议使用速度比较快的StringBuilder。

### 4、System

常用方法：

| 返回值            | 方法                                                         | 功能                                                     |
| ----------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| static void       | arraycopy(Object src, int srcPos, Object dest, int destPos, int length) | 将指定源数组中的数组从指定位置复制到目标数组的指定位置。 |
| static void       | currentTimeMillis()                                          | 返回当前时间（以毫秒为单位）。                           |
| static Properties | getProperties()                                              | 获取指定键指示的系统属性。                               |
| static void       | gc()                                                         | 运行垃圾回收器。                                         |

### 5、Math

math类中包含执行基本数学运算的方法，比如：绝对值-abs()、较大值-max()、较小值-min{}、四舍五入-round()

```java
double sqrt(double a)
double ceil(double a)
double floor(double a)
int max(int a, int b)
```

### 6、Throwable

1. Throwable
   Throwable是 Java 语言中所有错误或异常的超类。
   Throwable包含两个子类: Error 和 Exception。它们通常用于指示发生了异常情况。
   Throwable包含了其线程创建时线程执行堆栈的快照，它提供了printStackTrace()等接口用于获取堆栈跟踪数据等信息。
2. Exception
   Exception及其子类是 Throwable 的一种形式，它指出了合理的应用程序想要捕获的条件。
3. RuntimeException
   RuntimeException是那些可能在 Java 虚拟机正常运行期间抛出的异常的超类。
   编译器不会检查RuntimeException异常。例如，除数为零时，抛出ArithmeticException异常。RuntimeException是ArithmeticException的超类。当代码发生除数为零的情况时，倘若既"没有通过throws声明抛出ArithmeticException异常"，也"没有通过try…catch…处理该异常"，也能通过编译。这就是我们所说的"编译器不会检查RuntimeException异常"！
   如果代码会产生RuntimeException异常，则需要通过修改代码进行避免。例如，若会发生除数为零的情况，则需要通过代码避免该情况的发生！
4. Error
   和Exception一样，Error也是Throwable的子类。它用于指示合理的应用程序不应该试图捕获的严重问题，大多数这样的错误都是异常条件。
   和RuntimeException一样，编译器也不会检查Error

我们最常见的异常就是运行时异常（非检查异常）

| 异常                           | 描述                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| ArithmeticException            | 当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时，抛出此类的一个实例。 |
| ArrayIndexOutOfBoundsException | 用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引。 |
| ArrayStoreException            | 试图将错误类型的对象存储到一个对象数组时抛出的异常。         |
| ClassCastException             | 当试图将对象强制转换为不是实例的子类时，抛出该异常           |
| IllegalArgumentException       | 抛出的异常表明向方法传递了一个不合法或不正确的参数。         |
| IndexOutOfBoundsException      | 指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。 |
| NullPointerException           | 当应用程序试图在需要对象的地方使用 null 时，抛出该异常       |
| NumberFormatException          | 当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。 |

我们常见的检查异常

| 异常                   | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| ClassNotFoundException | 应用程序试图加载类时，找不到相应的类，抛出该异常。           |
| NoSuchFieldException   | 请求的变量不存在                                             |
| NoSuchMethodException  | 请求的方法不存在                                             |
| IOException            | 表示发生某种类型的I / O异常。 此类是由失败或中断的I / O操作产生的一般异常类。 |
| SQLException           | 提供有关数据库访问错误或其他错误的信息的异常。               |
| FileNotFoundException  | 指示尝试打开由指定路径名表示的文件失败。                     |
| EOFException           | 表示在输入过程中意外地到达文件结束或流结束。                 |

### 7、Thread

第一种：

- 继承 java.lang.Thread
- 重写 run 方法

```java
class Processor extends Thread{
    public void run(){
    System.out.println("helloworld");
    }
}
```

第二种：

- 实现 java.lang.Runnable
- 实现 run 方法

```java
class Processor1 implements Runnable{
    public void run(){
    System.out.println("helloworld");
    }
}
```

### 8、其他

- java的元注解在lang包下

  ![QQ截图20201214213631.png](https://i.loli.net/2020/12/15/lBhXL6uA7rdTHfp.png)

- 反射相关的在lang包

   ![QQ截图20201214214033.png](https://i.loli.net/2020/12/15/lWZIiO9HwFV4u3c.png)

- 常见的异常，错误在lang包

  > ArrayIndexOutOfBoundsException
  >
  > ClassCastException
  >
  > ClassNotFoundException
  >
  > IllegalArgumentException
  >
  > IndexOutOfBoundsException
  >
  > NullPointerException
  >
  > NumberFormatException   。。。。。。。。。。

## math包

#### BigInteger

BigInteger有三个静态的常数，分别为ONE, TEM, ZERO

```JAVA
public static void main(String[] args) {
    System.out.println(BigInteger.ONE);//1
    System.out.println(BigInteger.TEN);//10
    System.out.println(BigInteger.ZERO);//0
}
```

BigInteger构造函数中有一个将十进制字符串转成成BigInteger,注意：BigInteger没有无参构造函数

```java
BigInteger  bigInteger = new BigInteger("100")//100
```

BigInteger还可以通过valueOf方法将普通数值转成大数值

```java
BigInteger valueOf = BigInteger.valueOf(1000);
System.out.println(valueOf);
```

**注意**：BigInteger不能通过基本数据类型的加减乘除(+,-,*,/)方式处理，而是通过方法来处理

BigInteger提供了各种数学计算的方式，比如绝对值，异或运算

```java
    public static void main(String[] args) {
        BigInteger bigInteger = new BigInteger("100");
        BigInteger valueOf = BigInteger.valueOf(1000);
        //加法
        BigInteger add = valueOf.add(bigInteger);
        //减法
        BigInteger subtract = valueOf.subtract(bigInteger);
        //除法
        BigInteger divide = valueOf.divide(bigInteger);
        //乘法
        BigInteger multiply = valueOf.multiply(bigInteger);
        //转成double  当然floatValue，intValue，longValue
        double v = valueOf.doubleValue();
        //比较是否相等
        boolean equals = valueOf.equals(bigInteger);
        //求负数
        BigInteger negate = valueOf.negate();
        //转换成字符串
        String s = valueOf.toString();
        BigInteger xor = valueOf.xor(bigInteger);
        System.out.println(xor);//908
        System.out.println(s);//1000
        System.out.println(negate);//-1000
        System.out.println(equals);//false
        System.out.println(v);//1000.0
        System.out.println(multiply);//100000
        System.out.println(divide);//10
        System.out.println(subtract);//900
        System.out.println(add);//1100
    }
```

> 普通精度计算丢失： 我们的计算机是二进制的。浮点数没有办法是用二进制进行精确表示。我们的CPU表示浮点数由两个部分组成：**指数和尾数**，这样的表示方法一般都会失去一定的精确度，有些浮点数运算也会产生一定的误差。如：2.4的二进制表示并非就是精确的2.4。反而最为接近的二进制表示是 2.3999999999999999。浮点数的值实际上是由一个特定的数学公式计算得到的。 

#### BigDecimal

**使用Double.toString(double)转成String，然后使用String构造方法，或使用BigDecimal的静态方法valueOf，如下**

```java
public static void main(String[] args)
{
    BigDecimal bDouble1 = BigDecimal.valueOf(2.3);
    BigDecimal bDouble2 = new BigDecimal(Double.toString(2.3));

    System.out.println("bDouble1=" + bDouble1);
    System.out.println("bDouble2=" + bDouble2);

}
```

运算结果：

```
bDouble1=2.3
bDouble2=2.3
```

**BigDecimal运算**

对于常用的加，减，乘，除，BigDecimal类提供了相应的成员方法。例如：

```java
public static void main(String[] args)
    {
        BigDecimal a = new BigDecimal("4.5");
        BigDecimal b = new BigDecimal("1.5");

        System.out.println("a + b =" + a.add(b));
        System.out.println("a - b =" + a.subtract(b));
        System.out.println("a * b =" + a.multiply(b));
        System.out.println("a / b =" + a.divide(b));
    }
```

结果：

```
a + b =6.0
a - b =3.0
a * b =6.75
a / b =3
```

这里有一点需要注意的是除法运算divide.

BigDecimal除法可能出现不能整除的情况，比如 4.5/1.3，这时会报错java.lang.ArithmeticException: Non-terminating decimal expansion; no exact representable decimal result.

其实divide方法有可以传三个参数

public BigDecimal divide(BigDecimal divisor, int scale, int roundingMode)
第一参数表示除数， 第二个参数表示小数点后保留位数，
第三个参数表示舍入模式，只有在作除法运算或四舍五入时才用到舍入模式，有下面这几种

```java
ROUND_CEILING    //向正无穷方向舍入

ROUND_DOWN    //向零方向舍入

ROUND_FLOOR    //向负无穷方向舍入

ROUND_HALF_DOWN    //向（距离）最近的一边舍入，除非两边（的距离）是相等,如果是这样，向下舍入, 例如1.55 保留一位小数结果为1.5

ROUND_HALF_EVEN    //向（距离）最近的一边舍入，除非两边（的距离）是相等,如果是这样，如果保留位数是奇数，使用ROUND_HALF_UP，如果是偶数，使用ROUND_HALF_DOWN

ROUND_HALF_UP    //向（距离）最近的一边舍入，除非两边（的距离）是相等,如果是这样，向上舍入, 1.55保留一位小数结果为1.6

ROUND_UNNECESSARY    //计算结果是精确的，不需要舍入模式

ROUND_UP    //向远离0的方向舍入
123456789101112131415
```

按照各自的需要，可传入合适的第三个参数。四舍五入采用 ROUND_HALF_UP

需要对BigDecimal进行截断和四舍五入可用setScale方法，例：

```java
public static void main(String[] args)
    {
        BigDecimal a = new BigDecimal("4.5635");

        a = a.setScale(3, RoundingMode.HALF_UP);    //保留3位小数，且四舍五入
        System.out.println(a);//4.564
    }
```

减乘除其实最终都返回的是一个新的BigDecimal对象，因为BigInteger与BigDecimal都是不可变的（immutable）的，在进行每一步运算时，都会产生一个新的对象。

```java
    public static void main(String[] args)
    {
        BigDecimal a = new BigDecimal("4.5");
        BigDecimal b = new BigDecimal("1.5");
        BigDecimal add = a.add(b);

        System.out.println(add);//6.0
        System.out.println(a);  //输出4.5. 加减乘除方法会返回一个新的BigDecimal对象，原来的a不变
    }
```

## Collectors

1. joining

   ```java
   List<User> listUser = new ArrayList<>();
   listUser.add(new User(20, "李白", true));
   listUser.add(new User(40, "杜甫", true));
   listUser.add(new User(18, "李清照", false));
   listUser.add(new User(23, "李商隐", true));
   listUser.add(new User(39, "杜牧", true));
   listUser.add(new User(16, "苏小妹", false));
   listUser.add(new User(16, "苏小妹", false));
   listUser.add(new User(16, "苏小妹", false));
   
   String join3 = listUser.stream().map(User::getName).collect(Collectors.joining(",", "{", "}"));
   System.out.println("join后的结果：" + join3); // 输出==》{李白,杜甫,李清照,李商隐,杜牧,苏小妹}
   ```

2.  mapping : 通过第一个参数函数来处理List中的每一个数据，然后用第二个参数来将处理后的数据收集起来 

   ```java
   List<String> userNames = listUser.stream()
       							 .collect(
       							 Collectors.mapping(User::getName, Collectors.toList()));
   // [李白, 杜甫, 李清照, 李商隐, 杜牧, 苏小妹]
   ```


3. toColletcion、toSet、toList

   ```java
   List<Integer> userNames = listUser.stream()
                   .map(User::getNum).collect(Collectors.toList());
   Set<String> sets = listUser.stream().map(User::getName).collect(Collectors.toSet());
   TreeSet<Integer> trees = listUser.stream().map(User::getNum)
                   .collect(Collectors.toCollection(TreeSet::new));
   System.out.println(userNames);//[20, 40, 18, 23, 39, 16, 16, 16]
   System.out.println(sets);//[李清照, 李白, 杜甫, 李商隐, 杜牧, 苏小妹]
   System.out.println(trees);//[16, 18, 20, 23, 39, 40]
   ```

4. collectingAndThen

    先 Collector ，再 Function
   注意：Function是对 Collector操作后的整体stream做操作 

   ```java
   Set<Entry<Boolean, List<User>>> collect = listUser.stream()
                   .collect(Collectors.collectingAndThen(Collectors.partitioningBy(User::getFlag),
                           Map::entrySet));
   System.out.println(collect);
   // [false=[User{num=18, name='李清照', flag=false}, User{num=16, name='苏小妹', flag=false}, User{num=16, name='苏小妹', flag=false}, User{num=16, name='苏小妹', flag=false}], true=[User{num=20, name='李白', flag=true}, User{num=40, name='杜甫', flag=true}, User{num=23, name='李商隐', flag=true}, User{num=39, name='杜牧', flag=true}]]
   ```

5. maxBy、minBy

   ```java
   Optional<User> collect = listUser.stream()
       .collect(Collectors.maxBy(Comparator.comparing(User::getNum)));
   Optional<User> collect1 = listUser.stream()
       .collect(Collectors.minBy(Comparator.comparing(User::getNum)));
   System.out.println(collect);
   System.out.println(collect1);
   
   //Optional[User{num=40, name='杜甫', flag=true}]
   //Optional[User{num=16, name='苏小妹', flag=false}]
   ```

6. summingInt、summingLong、summingDouble

   ```java
   Integer collect = listUser.stream()
       .collect(Collectors.summingInt(User::getNum));
   System.out.println(collect);
   //188
   ```

7. averagingInt、averagingLong、saveragingDouble

   求平均值

8. reducing

   ```java
   //例如，给定Person流，以计算每个城市中的最高人员：
    
   Comparator<Person> byHeight = Comparator.comparing(Person::getHeight);
   Map<City, Person> tallestByCity
       = people.stream().collect(groupingBy(Person::getCity, reducing(BinaryOperator.maxBy(byHeight))));
   ```

9. groupingBy

   按照条件对元素进行分组，和 **SQL** 中的 `group by` 用法有异曲同工之妙，通常也建议使用 **Java** 进行分组处理以减轻数据库压力。`groupingBy` 也有三个重载方法
   我们将 `servers` 按照长度进行分组:

   ```java
   // 按照字符串长度进行分组    符合条件的元素将组成一个 List 映射到以条件长度为key 的 Map<Integer, List<String>> 中
   servers.stream.collect(Collectors.groupingBy(String::length))
   ```

   如果我不想 `Map` 的 `value` 为 `List` 怎么办？ 上面的实现实际上调用了下面的方式：

   ```java
   //Map<Integer, Set<String>>
   servers.stream.collect(Collectors.groupingBy(String::length, Collectors.toSet()))
   ```

   我要考虑同步安全问题怎么办？ 当然使用线程安全的同步容器啊，那前两种都用不成了吧！ 别急！ 我们来推断一下，其实第二种等同于下面的写法:

   ```java
   Supplier<Map<Integer,Set<String>>> mapSupplier = HashMap::new;
   Map<Integer,Set<String>> collect = servers.stream.collect(Collectors.groupingBy(String::length, mapSupplier, Collectors.toSet()));
   ```

   这就非常好办了，我们提供一个同步 `Map` 不就行了，于是问题解决了：

   ```java
   Supplier<Map<Integer, Set<String>>> mapSupplier = () -> Collections.synchronizedMap(new HashMap<>());
   Map<Integer, Set<String>> collect = servers.stream.collect(Collectors.groupingBy(String::length, mapSupplier, Collectors.toSet()));
   ```

   其实同步安全问题 `Collectors` 的另一个方法 `groupingByConcurrent` 给我们提供了解决方案。用法和 `groupingBy` 差不多。

10. partitioningBy

       `partitioningBy` 我们在本文开头的提到的文章中已经见识过了，可以看作 `groupingBy` 的一个特例，基于断言（`Predicate`）策略分组。这里不再举例说明。

11. counting

        该方法归纳元素的的数量，非常简单，不再举例说明。111