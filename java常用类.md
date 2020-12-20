





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

     该方法归纳元素的的数量，非常简单，不再举例说明。

## Stream

### maven强制打包

```shell
-DskipTests=true clean package -e -U
```

**2. 流的中间操作**

2.1 筛选与切片 filter：过滤流中的某些元素 limit(n)：获取n个元素 skip(n)：跳过n元素，配合limit(n)可实现分页 distinct：通过流中元素的 hashCode() 和 equals() 去除重复元素

```java
Stream<Integer> stream = Stream.of(6, 4, 6, 7, 3, 9, 8, 10, 12, 14, 14);
Stream<Integer> newStream = stream.filter(s -> s > 5) //6 6 7 9 8 10 12 14 14
    .distinct() //6 7 9 8 10 12 14
    .skip(2) //9 8 10 12 14
    .limit(2); //9 8
newStream.forEach(System.out::println);
```

2.2 映射
map：接收一个函数作为参数，该函数会被应用到每个元素上，并将其映射成一个新的元素。 flatMap：接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流。

```jsvs
List<String> list = Arrays.asList("a,b,c", "1,2,3");
//将每个元素转成一个新的且不带逗号的元素
Stream<String> s1 = list.stream().map(s -> s.replaceAll(",", ""));
s1.forEach(System.out::println); // abc  123
Stream<String> s3 = list.stream().flatMap(s -> {
    //将每个元素转换成一个stream
    String[] split = s.split(",");
    Stream<String> s2 = Arrays.stream(split);
    return s2;
});
s3.forEach(System.out::println); // a b c 1 2 3
```

2.3 排序 sorted()：自然排序，流中元素需实现Comparable接口 sorted(Comparator com)：定制排序，自定义Comparator排序器

```java
List<String> list = Arrays.asList("aa", "ff", "dd");
//String 类自身已实现Compareable接口
list.stream().sorted().forEach(System.out::println);// aa dd ff
Student s1 = new Student("aa", 10);
Student s2 = new Student("bb", 20);
Student s3 = new Student("aa", 30);
Student s4 = new Student("dd", 40);
List<Student> studentList = Arrays.asList(s1, s2, s3, s4);
//自定义排序：先按姓名升序，姓名相同则按年龄升序
studentList.stream().sorted(
    (o1, o2) -> {
        if (o1.getName().equals(o2.getName())) {
            return o1.getAge() - o2.getAge();
        } else {
            return o1.getName().compareTo(o2.getName());
        }
    }
).forEach(System.out::println);      
```

**3. 流的终止操作**

3.1 匹配、聚合操作 allMatch：接收一个 Predicate 函数，当流中每个元素都符合该断言时才返回true，否则返回false noneMatch：接收一个 Predicate 函数，当流中每个元素都不符合该断言时才返回true，否则返回false anyMatch：接收一个 Predicate 函数，只要流中有一个元素满足该断言则返回true，否则返回false findFirst：返回流中第一个元素 findAny：返回流中的任意元素 count：返回流中元素的总个数 max：返回流中元素最大值 min：返回流中元素最小值

```
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
boolean allMatch = list.stream().allMatch(e -> e > 10); //false
boolean noneMatch = list.stream().noneMatch(e -> e > 10); //true
boolean anyMatch = list.stream().anyMatch(e -> e > 4);  //true
Integer findFirst = list.stream().findFirst().get(); //1
Integer findAny = list.stream().findAny().get(); //1
long count = list.stream().count(); //5
Integer max = list.stream().max(Integer::compareTo).get(); //5
Integer min = list.stream().min(Integer::compareTo).get(); //1
```

3.2 规约操作 Optional<T> reduce(BinaryOperator<T> accumulator)：第一次执行时，accumulator函数的第一个参数为流中的第一个元素，第二个参数为流中元素的第二个元素；第二次执行时，第一个参数为第一次函数执行的结果，第二个参数为流中的第三个元素；依次类推。 T reduce(T identity, BinaryOperator<T> accumulator)：流程跟上面一样，只是第一次执行时，accumulator函数的第一个参数为identity，而第二个参数为流中的第一个元素。 `java  U reduce(U identity,BiFunction accumulator,BinaryOperator combiner)：` 在串行流(stream)中，该方法跟第二个方法一样，即第三个参数combiner不会起作用。在并行流(parallelStream)中,我们知道流被fork join出多个线程进行执行，此时每个线程的执行流程就跟第二个方法reduce(identity,accumulator)一样，而第三个参数combiner函数，则是将每个线程的执行结果当成一个新的流，然后使用第一个方法reduce(accumulator)流程进行规约。

```java
//经过测试，当元素个数小于24时，并行时线程数等于元素个数，当大于等于24时，并行时线程数为16
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24);
Integer v = list.stream().reduce((x1, x2) -> x1 + x2).get();
System.out.println(v);   // 300
Integer v1 = list.stream().reduce(10, (x1, x2) -> x1 + x2);
System.out.println(v1);  //310
Integer v2 = list.stream().reduce(0,
                                  (x1, x2) -> {
                                      System.out.println("stream accumulator: x1:" + x1 + "  x2:" + x2);
                                      return x1 - x2;
                                  },
                                  (x1, x2) -> {
                                      System.out.println("stream combiner: x1:" + x1 + "  x2:" + x2);
                                      return x1 * x2;
                                  });
System.out.println(v2); // -300
Integer v3 = list.parallelStream().reduce(0,
                                          (x1, x2) -> {
                                              System.out.println("parallelStream accumulator: x1:" + x1 + "  x2:" + x2);
                                              return x1 - x2;
                                          },
                                          (x1, x2) -> {
                                              System.out.println("parallelStream combiner: x1:" + x1 + "  x2:" + x2);
                                              return x1 * x2;
                                          });
System.out.println(v3); //197474048
```

3.3 收集操作 collect：接收一个Collector实例，将流中元素收集成另外一个数据结构。 Collector<T, A, R> 是一个接口，有以下5个抽象方法： Supplier supplier()：创建一个结果容器A BiConsumer<A, T> accumulator()：消费型接口，第一个参数为容器A，第二个参数为流中元素T。 BinaryOperator combiner()：函数接口，该参数的作用跟上一个方法(reduce)中的combiner参数一样，将并行流中各个子进程的运行结果(accumulator函数操作后的容器A)进行合并。 Function<A, R> finisher()：函数式接口，参数为：容器A，返回类型为：collect方法最终想要的结果R。 Set<Characteristics> characteristics()：返回一个不可变的Set集合，用来表明该Collector的特征。有以下三个特征： CONCURRENT：表示此收集器支持并发。（官方文档还有其他描述，暂时没去探索，故不作过多翻译） UNORDERED：表示该收集操作不会保留流中元素原有的顺序。 IDENTITY_FINISH：表示finisher参数只是标识而已，可忽略。

## Comparator

- 对整数列表排序（升序）

```java
List<Integer> list = Arrays.asList(1, 4, 2, 6, 2, 8);
list.sort(Comparator.naturalOrder());
System.out.println(list);
```

- 对整数列表排序（降序）

```java
List<Integer> list = Arrays.asList(1, 4, 2, 6, 2, 8);
list.sort(Comparator.reverseOrder());
System.out.println(list);
```

- 根据对象属性（年龄）进行排序

```java
public class Test {
    public static void main(String[] args) {
        List<Person> personList = new ArrayList<>();
        personList.add(new Person("a", 2));
        personList.add(new Person("b", 4));
        personList.add(new Person("c", 7));
        // 升序
        personList.sort(Comparator.comparingInt(Person::getAge));
        // 降序
        personList.sort(Comparator.comparingInt(Person::getAge).reversed());
        System.out.println(personList);
    }
}
```

- 根据对象属性（价格、速度）进行排序，需要注意的是，**排序有先后之分，不同的顺序会导致不同的结果** 

```cpp
public class Test {
    public static void main(String[] args) {
        List<Computer> list = new ArrayList<>();
        list.add(new Computer("xiaomi",4000,6));
        list.add(new Computer("sony",5000,4));
        list.add(new Computer("dell",4000,5));
        list.add(new Computer("mac",6000,8));
        list.add(new Computer("micro",5000,6));
        // 先以价格（升序）、后再速度（升序）
        list.sort(Comparator.comparingInt(Computer::getPrice).thenComparingInt(Computer::getSpeed));
        // 先以速度（降序）、后再价格（升序）
        list.sort(Comparator.comparingInt(Computer::getSpeed).reversed().thenComparingInt(Computer::getPrice));
        // 先以价格（降序）、后再速度（降序）
        list.sort(Comparator.comparingInt(Computer::getPrice).thenComparingInt(Computer::getSpeed).reversed());
        System.out.println(list);
    }

    public static class Computer {
        private String name;
        private Integer price;
        private Integer speed;
    }
```

- nullFirst、nullLast

  nullFirst，返回一个对null友好的比较器，该比较器认为null小于非null，nullLast反之

## JUC

volatile类型，说明了多线程下的可见性，即任何一个线程的修改，在其它线程中都会被立刻看到

[![raUvDI.png](https://s3.ax1x.com/2020/12/20/raUvDI.png)](https://imgchr.com/i/raUvDI)

### 内存可见性

 Java Memory Model (JAVA 内存模型）描述线程之间如何通过内存(memory)来进行交互。 具体说来， JVM中存在一个主存区（Main Memory或Java Heap Memory），对于所有线程进行共享，而每个线程又有自己的工作内存（Working Memory），工作内存中保存的是主存中某些变量的拷贝，线程对所有变量的操作并非发生在主存区，而是发生在工作内存中，而线程之间是不能直接相互访问，变量在程序中的传递，是依赖主存来完成的。

 如果线程1**对共享变量flag进行了修改**，但是线程1**没有及时把更新后的值刷入到主内存中**，而此时main线程从主内存读取共享变量flag的值，所以flag的值是原始值，那么我们就说对于main线程来讲，共享变量flag的更改对main线程是不可见的  

[![](https://s3.ax1x.com/2020/12/20/raNzhF.png)](https://imgchr.com/i/raNzhF)



### AtomicInteger

- **有参构造函数**：从构造函数函数可以看出，数值存放在成员变量value中;
- 成员变量value声明为volatile类型，说明了多线程下的可见性，即任何一个线程的修改，在其它线程中都会被立刻看到

```java
public AtomicInteger(int initialValue) { 
  value = initialValue;
}
```

------

- **compareAndSet**方法（value的值通过内部this和valueOffset传递）
- 这个方法就是最核心的CAS操作
- 接收2个参数，一个是期望数据(expected)，一个是新数据(new)；如果atomic里面的数据和期望数据一致，则将新数据设定给atomic的数据，返回true，表明成功；否则就不设定，并返回false。

```java
public final boolean compareAndSet(int expect, int update) {
	return unsafe.compareAndSwapInt(this, valueOffset, expect, update);
}
```

------

- **getAndSet**方法,在该方法中调用了compareAndSet方法
- 本质是get( )操作，然后做set( )操作。尽管这2个操作都是atomic，但是他们合并在一起的时候，就不是atomic
- 如果在执行if(compareAndSet(current,newValue)之前其它线程更改了value的值，那么导致value的值必定和current的值不同，compareAndSet执行失败，只能重新获取value的值，然后继续比较，直到成功。

```java
public final int getAndSet(int newValue) {
    for (;;) {
      int current = get();
      if (compareAndSet(current, newValue))
        return current;
    }
}
```

### Lock与ReentrantLock

### 1、概述

Java中的锁有两种，synchronized与Lock。因为使用synchronized并不需要显示地加锁与解锁，所以往往称synchronized为**隐式锁**，而使用Lock时则相反，所以一般称Lock为**显示锁**

synchronized修饰方法或语句块，所有锁的获取和释放都必须出现在一个块结构中。Lock接口的实现允许锁在不同的范围内获取和释放，并支持以任何顺序获取和释放多个锁。

使用synchronized修饰方法或语句时锁自动释放，Lock实现需要手动释放锁

除了更灵活之外，Lock还有以下优点：

- Lock 实现提供了使用 synchronized 方法和语句所没有的其他功能，包括提供了一个非块结构的获取锁尝试 `tryLock()`、一个获取可中断锁的尝试 `lockInterruptibly()` 和一个获取超时失效锁的尝试 `tryLock(long, TimeUnit)`。
- Lock 类还可以提供与隐式监视器锁完全不同的行为和语义，如保证排序、非重入用法或死锁检测。如果某个实现提供了这样特殊的语义，则该实现必须对这些语义加以记录。

**ReentrantLock是一个可重入的互斥锁。**顾名思义，“互斥锁”表示在某一时间点只能被同一线程所拥有。“可重入”表示锁可被某一线程多次获取。**当然 synchronized 也是可重入的互斥锁**

当锁没有被某一线程占有时，调用 lock() 方法的线程将成功获取锁。可以使用`isHeldByCurrentThread()`和 `getHoldCount()`方法来判断当前线程是否拥有该锁。

**ReentrantLock既可以是公平锁又可以是非公平锁。**当此类的构造方法 ReentrantLock(boolean fair) 接收true作为参数时，ReentrantLock就是公平锁，线程依次排队获取公平锁，即锁将被等待最长时间的线程占有。与默认情况（使用非公平锁）相比，使用公平锁的程序在多线程环境下效率比较低。而且公平锁不能保证线程调度的公平性，tryLock方法可在锁未被其他线程占用的情况下获得该锁。

### 2、API

**1、构造方法**

```java
//创建一个 ReentrantLock 的实例。
ReentrantLock() 

//创建一个具有给定公平策略的 ReentrantLock。  
ReentrantLock(boolean fair) 12345
```

**2、方法摘要**

```java
int getHoldCount() 
          //查询当前线程保持此锁的次数。
protected  Thread   getOwner() 
          //返回目前拥有此锁的线程，如果此锁不被任何线程拥有，则返回 null。
protected  Collection<Thread>   getQueuedThreads() 
          //返回一个 collection，它包含可能正等待获取此锁的线程。
 int    getQueueLength() 
          //返回正等待获取此锁的线程估计数。
protected  Collection<Thread>   getWaitingThreads(Condition condition) 
          //返回一个 collection，它包含可能正在等待与此锁相关给定条件的那些线程。
 int    getWaitQueueLength(Condition condition) 
          //返回等待与此锁相关的给定条件的线程估计数。
 boolean    hasQueuedThread(Thread thread) 
          //查询给定线程是否正在等待获取此锁。
 boolean    hasQueuedThreads() 
          //查询是否有些线程正在等待获取此锁。
 boolean    hasWaiters(Condition condition) 
          //查询是否有些线程正在等待与此锁有关的给定条件。
 boolean    isFair() 
          //如果此锁的公平设置为 true，则返回 true。
 boolean    isHeldByCurrentThread() 
          //查询当前线程是否保持此锁。
 boolean    isLocked() 
          //查询此锁是否由任意线程保持。
 void   lock() 
          //获取锁。
 void   lockInterruptibly() 
          //如果当前线程未被中断，则获取锁。
 Condition  newCondition() 
          //返回用来与此 Lock 实例一起使用的 Condition 实例。
 String toString() 
          //返回标识此锁及其锁定状态的字符串。
 boolean    tryLock() 
          //仅在调用时锁未被另一个线程保持的情况下，才获取该锁。
 boolean    tryLock(long timeout, TimeUnit unit) 
          //如果锁在给定等待时间内没有被另一个线程保持，且当前线程未被中断，则获取该锁。
 void   unlock() 
          //试图释放此锁。
```

### 3、代码

**1、典型的代码**

```java
class X {
    private final ReentrantLock lock = new ReentrantLock();
    // ...

    public void m() { 
        lock.lock();  // block until condition holds
        try {
            // ... method body
        } finally {
            lock.unlock()
        }
    }
}
```

