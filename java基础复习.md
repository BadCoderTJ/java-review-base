[TOC]



### 1、数组复习

#### 1.1数组的静态动态初始化

```java
public static void main(String[] args) {
        //数组的静态初始化
        int[] arrays = new int[]{1,2,3};
        System.out.println(Arrays.toString(arrays));
        //动态初始化
        int[] arrays1 = new int[4];
        arrays1[3] = 7;
        System.out.println(Arrays.toString(arrays1));
    }
    //输出：[1, 2, 3]
    //     [0, 0, 0, 7]
```

#### 1.2数组元素的默认初始化值

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129144424.png)

#### 1.3内存分析

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129145022.png)

#### 1.4二维数组的内存分析

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129145438.png)

#### 1.5常见Arrays工具类方法

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129151039.png)

### 2、面向对象编程

#### 1.1基本概述

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129151421.png)

#### 1.2对象的创建与使用：内存

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129151952.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129152230.png)

#### 1.3成员变量与局部变量

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129152603.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129152812.png)

#### 1.4方法重载

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129153200.png)

#### 1.5jdk包分布

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129154455.png)

#### 1.6子类与父类

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129155801.png)

#### 1.7this与super

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129155947.png)

#### 1.8对象的强制转换

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129164149.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129164344.png)

#### 1.9==与equals区别

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129164730.png)

#### 1.10代码块

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129170856.png)

### 3、异常

#### 3.1异常与错误

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201129172959.png)

### 4、常用类

#### 4.1String

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130212859.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130213037.png)

`StringBuffer传入构造器的String不能为空`

#### 4.2Date

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130214222.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130214821.png)

##### 4.2.1LocalDate、LocalTime、LocalDateTime

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130220508.png)

> 查找接口的实现类：
>
> IDEA 风格 ctrl + alt +B

#### 4.3System

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130223118.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130223148.png)

#### 4.4Math

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130223215.png)

##### 4.4.1BigInteger

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130223458.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130225246.png)

##### 4.4.2BigDecimal

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130225401.png)

### 5、枚举与注解

#### 5.1枚举

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130225756.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130225841.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130230020.png)

#### 5.2注解

##### 5.1.1 自定义注解

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130230617.png)

##### 5.1.2 元注解

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130230852.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130231034.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130231130.png)

##### 5.1.3 Java的可重复注解

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130231352.png)

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201130231447.png)

### 6、集合

#### 6.1 迭代器

![](C:\Users\GOD_T\Desktop\java基础复习\QQ截图20201209214621.png)

![](QQ截图20201209214805.png)

#### 6.2 vector、ArrayList、LinkedList

![](QQ截图20201209214929.png)

#### 6.3 hashset

![](QQ截图20201209215123.png)

