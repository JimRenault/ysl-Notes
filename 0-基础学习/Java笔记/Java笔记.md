# Java笔记

## 一、Java初阶

### 1.1 数据类型

整数数据类型：

| 类型  | 占用存储空间 |                   表数范围                   |
| :---: | :----------: | :------------------------------------------: |
| byte  |    1字节     |            -2^7~2^7-1 (-128~127)             |
| short |    2字节     |         -2^15~2^15-1 (-32768~32767)          |
|  int  |    4字节     | -2^31~2^31-1 (-2147483648~2147483647) 约21亿 |
| long  |    8字节     |                 -2^63~2^63-1                 |

```java
// 赋值给long类型需要在数字后面加上 l 或者 L
// 因为 12345678910 这个数在int类型中已经算是超了
long num = 12345678910L;
```

| 类型   | 占用存储空间 | 表数范围                                                   |
| ------ | ------------ | ---------------------------------------------------------- |
| float  | 4字节        | 大约±3.402 823 47E+38F (有效位数为6-7位左右)               |
| double | 8字节        | 大约±1.797 693 134 862 315 70E+308 (有效位数为15-16位左右) |

PS：有效数字指的是从左开始第一个不为0的数到最后一个数

```java
public static void main(String[] args){
    //浮点类型的常量有两种形式：
    //十进制形式：
    double num1 = 3.14;
    System.out.println(num1);
    //科学计数法形式：
    double num2 = 314E-2; // 314×10^-2
    System.out.println(num2);

    //浮点类型的变量：
    //注意：浮点型默认是double类型的，要想将一个double类型的数赋给float类型，必须后面加上F或者f
    float f1 = 3.14234567898623F;
    System.out.println(f1);
    //注意：double类型后面可以加D或者d，但是一般我们都省略不写
    double d1 = 3.14234567898623D;
    System.out.println(d1);

    //注意：我们最好不要进行浮点类型的比较：
    float f2 = 0.3F;
    double d2 = 0.3;
    System.out.println(f2==d2);
    /*
    区别：
    = 赋值运算：  将等号右侧的值赋给等号左侧
    == 判断==左右两侧的值是否相等  ：结果要么相等 要么不相等
    ==运算符的结果就是要么是true，要么是false
    */
}
```

### 1.2 运算符

```java
// 逻辑与 ：& 规律：只要有一个操作数是false，那么结果一定是false
// 短路与：&& 规律：效率高一些，只要第一个表达式是false，那么第二个表达式就不用计算了，结果一定是false

// 逻辑或：| 规律：只要有一个操作数是true，那么结果一定是true
// 短路或：|| 规律：效率高一些，只要第一个表达式是true，那么第二个表达式就不用计算了，结果一定是true

//逻辑异或： ^  规律：两个操作数相同，结果为false，不相同，结果为true
```

### 1.3 流程控制

```java
// 随机数
// 随机生成三个1-6之间的数
Math.random() -------> [0.0,1.0)
Math.random()*6 ----->[0.0,6.0)
(int)(Math.random()*6)  ----->[0,5]
(int)(Math.random()*6) +1 ----->[1,6]

```

```java
// switch多分支结构(多值情况)
switch (表达式) {
    case 值1:
         语句序列1;
         [break];
    case 值2:
         语句序列2;
         [break];
        … … …      … …
    [default:默认语句;]
}
```

### 1.4 数组

```java
// 数组的三种初始化方式: 静态初始化、动态初始化、默认初始化
// 1.静态初始化: 除了用new关键字来产生数组以外，还可以直接在定义数组的同时就为数组元素分配空间并赋值。
eg:
int[] arr = {12,23,45};
int[] arr = new int[]{12,23,45};
注意：
1.new int[3]{12,23,45};-->错误
2.int[] arr ;
   arr = {12,23,45};  --->错误
   
// 2.动态初始化: 数组定义与为数组元素分配空间并赋值的操作分开进行。
eg:
int[] arr ;
arr = new int[3]
arr[0] = 12;
arr[1] = 23;
arr[2] = 45;

// 3.默认初始化: 数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。
int[] arr = new int[3];   ---> 数组有默认的初始化值,要看是什么类型的数组
```

```java
// 可变参数
public class TestArray12{
        /*
        1.可变参数：作用提供了一个方法，参数的个数是可变的 ,解决了部分方法的重载问题
        int...num
        double...num
        boolean...num
        2.可变参数在JDK1.5之后加入的新特性
        3.方法的内部对可变参数的处理跟数组是一样
        4.可变参数和其他数据一起作为形参的时候，可变参数一定要放在最后
        5.我们自己在写代码的时候，建议不要使用可变参数。
        */
    public static void main(String[] args){
                //method01(10);
                //method01();
                //method01(20,30,40);
                method01(30,40,50,60,70);
                //method01(new int[]{11,22,33,44});
        }
        public static void method01(int num2,int...num){ // 30在num2,后面在num中
                System.out.println("-----1");
                for(int i:num){
                        System.out.print(i+"\t");
                }
                System.out.println();
                System.out.println(num2);
        }
}
```

```java
// Arrays工具类
//给定一个数组：
int[] arr = {1,3,7,2,4,8};
//toString:对数组进行遍历查看的，返回的是一个字符串，这个字符串比较好看
System.out.println(Arrays.toString(arr));
//binarySearch:二分法查找：找出指定数组中的指定元素对应的索引
//这个方法的使用前提：一定要查看的是一个有序的数组
//sort：排序 -->升序
Arrays.sort(arr);
System.out.println(Arrays.binarySearch(arr,4));

//copyOf:完成数组的复制
int[] newArr = Arrays.copyOf(arr2,4);
//copyOfRange:区间复制：
int[] newArr2 = Arrays.copyOfRange(arr2,1,4);//[1,4)-->1,2,3位置

//equals:比较两个数组的值是否一样
int[] arr3 = {1,3,7,2,4,8};
int[] arr4 = {1,3,7,2,4,8};
System.out.println(Arrays.equals(arr3,arr4));//true
System.out.println(arr3==arr4);//false ==比较左右两侧的值是否相等，比较的是左右的地址值，返回结果一定是false

//fill：数组的填充
Arrays.fill(arr5,10);
```

```java
// 数组的复制
//给一个源数组：
int[] srcArr = {11,22,33,44,55,66,77,88};
//给一个目标数组：
int[] destArr = new int[10];

//复制：
//参数：src-源数组、srcPos-源数组中的起始位置、dest-目标数组、destPos-目标数组起始位置、length-要复制的数组元素的数量
System.arraycopy(srcArr,1,destArr,3,3);
//遍历查看目标数组：
System.out.println(Arrays.toString(destArr));
```

```java
// 二维数组初始化方式有三种：静态初始化、动态初始化、默认初始化。
// 静态初始化: 除了用new关键字来产生数组以外，还可以直接在定义数组的同时就为数组元素分配空间并赋值。
eg:
int[][] arr = {{1,2},{4,5,6},{4,5,6,7,8,9,9}};
int[][] arr =new int[][] {{1,2},{4,5,6},{4,5,6,7,8,9,9}};
// 动态初始化: 数组定义与为数组元素分配空间并赋值的操作分开进行。
eg:
int[][] arr = new int[3][]; //本质上定义了一维数组长度为3，每个“格子”中放入的是一个数组
arr[0] = new int[]{1,2};
arr[1] = new int[]{3,4,5,6};
arr[2] = new int[]{34,45,56};

eg:
int[][] arr = new int[3][2];
//本质上: 定义一维数组,长度为3,每个数组"格子"中,有一个默认的长度为2的数组,当然也可以放进去长度大于2的数组.
arr[1] = new int[]{1,2,3,4};
//数组遍历：
for(int[] a:arr){
    for(int num:a){
        System.out.print(num+"\t");
    }
    System.out.println();
}

// 默认初始化: 数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。
```

### 1.5 IDEA快捷键

```java
// 代码向上/下移动：Ctrl + Shift + Up / Down
// 搜索类：  ctrl+n
// 单行注释或多行注释 ：  Ctrl + / 或 Ctrl + Shift + /
// 代码块包围：try-catch,if,while等  ctrl+alt+t
// 显示代码结构  : alt + 7
```

## 二、Java中阶

## 2.1 面向对象

### 2.1.1 三个阶段

```java
// 面向对象三个阶段：
//【1】面向对象分析OOA  --  Object Oriented Analysis
对象：张三，王五，朱六，你，我
抽取出一个类----》人类
类里面有什么：
动词--》动态特性--》方法
名词--》静态特性--》属性
//【2】面向对象设计OOD  --  Object Oriented Design
先有类，再有对象：
类：人类： Person
对象：zhangsan ，lisi，zhuliu
//【3】面向对象编程OOP  --  Object Oriented Programming
```

```java
//Person 属于 引用数据类型
//第一次加载类的时候，会进行类的加载，初始化创建对象的时候，对象的属性没有给赋值，有默认的初始化的值。
//再创建一个对象：
//再次创建类的时候，就不会进行类的加载了，类的加载只在第一次需要的时候加载一次
```

### 2.1.2 代码块

```java
// 代码块	运行下面的代码 查看分析结果
public class Test {

    //属性
    int a;
    static int sa;
    //方法
    public void a(){
        System.out.println("-----a");
        {
            //普通块限制了局部变量的作用范围
            System.out.println("这是普通块");
            System.out.println("----000000");
            int num = 10;
            System.out.println(num);
        }
        //System.out.println(num);
        //if(){}
        //while(){}
    }
    public static void b(){
        System.out.println("------b");
    }
    //构造块
    {
        System.out.println("------这是构造块");
    }
    //静态块
    static{
        System.out.println("-----这是静态块");
        //在静态块中只能方法：静态属性，静态方法
        System.out.println(sa);
        b();
    }
    //构造器
    public Test(){
        System.out.println("这是空构造器");
    }
    public Test(int a){
        this.a = a;
    }
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Test t = new Test();
        t.a();
        Test t2 = new Test();
        t2.a();
    }
}
//总结：
//（1）代码块执行顺序：
//最先执行静态块，只在类加载的时候执行一次，所以一般以后实战写项目：创建工厂，数据库的初始化信息都放入静态块。
//一般用于执行一些全局性的初始化操作。

//再执行构造块，（不常用）
//再执行构造器，
//再执行方法中的普通块。
```

### 2.1.3 权限修饰符

|           | 同一个类 | 同一个包 | 子类 | 所有类 |
| --------- | -------- | -------- | ---- | ------ |
| private   | *        |          |      |        |
| default   | *        | *        |      |        |
| protected | *        | *        | *    |        |
| public    | *        | *        | *    | *      |

### 2.1.4 重载和重写的区别

重载：在同一个类中，当方法名相同，形参列表不同的时候  多个方法构成了重载
重写：在不同的类中，子类对父类提供的方法不满意的时候，要对父类的方法进行重写。

|      | 英文     | 位置       | 修饰符                       | 返回值                   | 方法名   | 参数     | 抛出异常 | 方法体 |
| ---- | -------- | ---------- | ---------------------------- | ------------------------ | -------- | -------- | -------- | ------ |
| 重载 | overload | 同一个类中 | 无关                         | 无关                     | 必须相同 | 必须不同 | 无关     | 不同   |
| 重写 | override | 子类父类中 | 父类的权限修饰符要低于子类的 | 父类的返回值类型大于子类 | 必须相同 | 必须不同 | 小于等于 | 不同   |

### 2.1.5 super

```tex
1.super可以修饰属性，可以修饰方法；
2.在特殊情况下，当子类和父类的属性重名时，你要想使用父类的属性，必须加上修饰符super.，只能通过super.属性来调用
在特殊情况下，当子类和父类的方法重名时，你要想使用父类的方法，必须加上修饰符super.，只能通过super.方法来调用
在这种情况下，super.就不可以省略不写。
3.super修饰构造器：
其实我们平时写的构造器的第一行都有：super()  -->作用：调用父类的空构造器，只是我们一般都省略不写
（所有构造器的第一行默认情况下都有super(),但是一旦你的构造器中显示的使用super调用了父类构造器，那么这个super()就不会给你默认分配了。
如果构造器中没有显示的调用父类构造器的话，那么第一行都有super(),可以省略不写）
如果构造器中已经显示的调用super父类构造器，那么它的第一行就没有默认分配的super();了
在构造器中，super调用父类构造器和this调用子类构造器只能存在一个，两者不能共存：
因为super修饰构造器要放在第一行，this修饰构造器也要放在第一行：
所以只能二选一
4.以后写代码构造器的生成可以直接使用IDEA提供的快捷键：alt+insert
```

### 2.1.6 Object类

```java
// toString()方法
// 出现的问题：子类Student对父类Object提供的toString方法不满意，不满意--》对toString方法进行重写：
// 总结：toString的作用就是对对象进行“自我介绍”，一般子类对父类提供的toString都不满意，都要进行重写。
```

```java
// .equals()方法
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建Phone类的对象：
        Phone p1 = new Phone("华为P40",2035.98,2020);
        Phone p2 = new Phone("华为P40",2035.98,2020);
        //比较两个对象：p1和p2对象：
        //==的作用：比较左右两侧的值是否想的，要么相等，返回true,要么不相等,返回false
        System.out.println(p1==p2);//-->>>对于引用数据类型来说，比较的是地址值。--->一定返回的是false
        //Object类提供了一个方法 equals方法 ：作用：比较对象具体内容是否相等。
        boolean flag = p1.equals(p2);//点进源码发现：底层依旧比较的是==，比较的还是地址值。
        System.out.println(flag);
    }
}

// 在子类中对equals方法进行重写：
    public boolean equals(Object obj) {//Object obj = new Phone();
        //将obj转为Phone类型：
        if(obj instanceof Phone){	//判断obj类型是否Phone
       		Phone other = (Phone)obj;//向下转型，为了获取子类中特有的内容
        }
        if(this.getBrand()==other.getBrand()&&this.getPrice()==other.getPrice()&&
    			this.getYear()==other.getYear()){
            return true;
        }
        return false;
    }
//总结：equals作用：这个方法提供了对对象的内容是否相等 的一个比较方式，对象的内容指的就是属性。父类Object提供的equals就是在比较==地址，没有实际的意义，我们一般不会直接使用父类提供的方法，而是在子类中对这个方法进行重写。
//平时重写equals方法的时候可以使用idea自动生成该方法。
```

### 2.1.7 类之间关系

```java
//七、总结     
对于继承、实现这两种关系没多少疑问，它们体现的是一种类和类、或者类与接口间的纵向关系。其他的四种关系体现的是类和类、或者类与接口间的引用、横向关系，是比较难区分的，有很多事物间的关系要想准确定位是很难的。前面也提到，这四种关系都是语义级别的，所以从代码层面并不能完全区分各种关系。
但总的来说，后几种关系所表现的强弱程度依次为：组合>聚合>关联>依赖。
```

### 2.1.8 多态

```java
// 先有父类，再有子类：--》继承   先有子类，再抽取父类 ----》泛化
// 什么是多态?
多态就是多种状态：同一个行为，不同的子类表现出来不同的形态。
多态指的就是同一个方法调用，然后由于对象不同会产生不同的行为。
// 多态的好处?
为了提高代码的扩展性，符合面向对象的设计原则：开闭原则。
开闭原则：指的就是扩展是 开放的，修改是关闭的。
注意：多态可以提高扩展性，但是扩展性没有达到最好，以后我们会学习 反射
// 多态的要素
一，继承：Cat extends Animal  ,Pig extends Animal,   Dog extends Animal
二，重写：子类对父类的方法shout()重写
三，父类引用指向子类对象：

Pig p = new Pig();
Animal an = p;
将上面的代码合为一句话：
Animal an = new Pig();
=左侧：编译期的类型
=右侧：运行期的类型

public void play(Animal an){	//Animal an = an = new Pig();
    an.shout();
}
Animal an = new Pig();
g.play(an);
上面的代码，也是多态的一种非常常见的应用场合：父类当方法的形参，然后传入的是具体的子类的对象，
然后调用同一个方法，根据传入的子类的不同展现出来的效果也不同，构成了多态。
// 向下转型 和 向上转型
public static void main(String[] args) {
	Pig p = new Pig();
	Animal an = p;//转型：向上转型
	an.shout();
	//加入转型的代码：
	//将Animal转为Pig类型：
	Pig pig = (Pig)an ;//转型：向下转型
	pig.eat();
	pig.age = 10;
	pig.weight = 60.8;
}
```

### 2.1.9 简单工厂设计模式

```java
//不仅可以使用父类做方法的形参，还可以使用父类做方法的返回值类型，真实返回的对象可以是该类的任意一个子类对象。
//简单工厂模式的实现，它是解决大量对象创建问题的一个解决方案。将创建和使用分开，工厂负责创建，使用者直接调用即可。简单工厂模式的基本要求是
//1.定义一个static方法，通过类名直接调用
//2.返回值类型是父类类型，返回的可以是其任意子类类型
//3.传入一个字符串类型的参数，工厂根据参数创建对应的子类产品
public class PetStore {//宠物店 ---》工厂类
    //方法：提供动物
    public static Animal getAnimal(String petName){//多态的应用场合（二）
        Animal an = null;
        if("猫".equals(petName)){//petName.equals("猫") --》这样写容易发生空指针异常
            an = new Cat();
        }
        if("狗".equals(petName)){
            an = new Dog();
        }
        if("猪".equals(petName)){
            an = new Pig();
        }
        return an;
    }
}

public class Test {
    public static void main(String[] args) {
        Girl g = new Girl();
        //Cat c = new Cat();
        //Dog d = new Dog();
        //Pig p = new Pig();
        Animal an = PetStore.getAnimal("狗");
        g.play(an);
    }
}
```

### 2.1.10 final

```java
//1.修饰变量
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //第1种情况：
        //final修饰一个变量，变量的值不可以改变，这个变量也变成了一个字符常量，约定俗称的规定：名字大写
        final int A = 10;//final修饰基本数据类型
        //A = 20; 报错：不可以修改值
        //第2种情况：
        final Dog d = new Dog();//final修饰引用数据类型，那么地址值就不可以改变
        //d = new Dog(); -->地址值不可以更改
        //d对象的属性依然可以改变：
        d.age = 10;
        d.weight = 13.7;
        //第3种情况：
        final Dog d2 = new Dog();
        a(d2);
        //第4种情况：
        b(d2);
    }
    public static void a(Dog d){
        d = new Dog();
    }
    public static void b(final Dog d){//d被final修饰 ，指向不可以改变
        //d = new Dog();
    }
}

//2.修饰方法：final修饰方法，那么这个方法不可以被该类的子类重写：
//3.修饰类：final修饰类，代表没有子类，该类不可以被继承，一旦一个类被final修饰，那么里面的方法也没有必要用final修饰了（final可以省略不写）。子类也无法重写父类方法

//案例：JDK提供的Math类：看源码发现：
（1）使用Math类的时候无需导包，直接使用即可：因为它属于java.lang包
（2）Math类没有子类，不能被其他类继承：因为用final修饰
（3）里面的属性全部被final修饰，方法也是被final修饰的，只是省略不写了
原因：子类没有必要进行重写。
（4）外界不可以创建对象：
Math m = new Math(); //无法创建实例对象,因为构造方法被private修饰
（5）发现Math类中的所有的属性，方法都被static修饰
那么不用创建对象去调用，只能通过类名.属性名  类名.方法名 去调用
```

### 3.1.11 抽象类_抽象方法

```java
//【1】抽象类和抽象方法的关系：
抽象类中可以定义0-n个抽象方法。
//【2】抽象类作用：
在抽象类中定义抽象方法，目的是为了为子类提供一个通用的模板，子类可以在模板的基础上进行开发，先重写父类的抽象方法，然后可以扩展子类自己的内容。抽象类设计避免了子类设计的随意性，通过抽象类，子类的设计变得更加严格，进行某些程度上的限制。使子类更加的通用。
//【3】代码：
package com.msb.test03;
//4.一个类中如果有方法是抽象方法，那么这个类也要变成一个抽象类。
//5.一个抽象类中可以有0-n个抽象方法
public abstract class Person {
    //1.在一个类中，会有一类方法，子类对这个方法非常满意，无需重写，直接使用
    public void eat(){
        System.out.println("一顿不吃饿得慌");
    }
    //2.在一个类中，会有一类方法，子类对这个方法永远不满意，会对这个方法进行重写。
    //3.一个方法的方法体去掉，然后被abstract修饰，那么这个方法就变成了一个抽象方法
    public abstract void say();
    public abstract void sleep();
}
//6.抽象类可以被其他类继承：
//7.一个类继承一个抽象类，那么这个类可以变成抽象类
//8.一般子类不会加abstract修饰，一般会让子类重写父类中的抽象方法
//9.子类继承抽象类，就必须重写全部的抽象方法
//10.子类如果没有重写父类全部的抽象方法，那么子类也可以变成一个抽象类。但一般没有必要
class Student extends Person{
    @Override
    public void say() {
        System.out.println("我是东北人，我喜欢说东北话。。");
    }
    @Override
    public void sleep() {
        System.out.println("东北人喜欢睡炕。。");
    }
}
class Demo{
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //11.创建抽象类的对象：-->抽象类不可以创建对象！！！！！！！！！！！！
        //Person p = new Person();
        //12.创建子类对象： 可以创建
        Student s = new Student();
        s.sleep();
        s.say();
        
        //13.多态的写法：父类引用只想子类对象：
        Person p  = new Student();
        p.say();
        p.sleep();
    }
}
//【4】面试题：
（1）抽象类不能创建对象，那么抽象类中是否有构造器？
抽象类中一定有构造器。构造器的作用  给子类初始化对象的时候要先super调用父类的构造器。
（2）抽象类是否可以被final修饰？
不能被final修饰，因为抽象类设计的初衷就是给子类继承用的。要是被final修饰了这个抽象类了，就不存在继承了，就没有子类。
```

### 2.1.12 接口(JDK1.8之前)

```java
//【1】接口声明格式：
[访问修饰符]  interface 接口名   [extends  父接口1，父接口2…]  {
    常量定义；       
    方法定义；
}
//【2】代码：
package com.msb.test04;
/**
 * 1.类是类，接口是接口，它们是同一层次的概念。
 * 2.接口中没有构造器
 * 3.接口如何声明：interface
 * 4.在JDK1.8之前，接口中只有两部分内容：
 * （1）常量：固定修饰符：public static final
 * （2）抽象方法：固定修饰符：public abstract
 * 注意：修饰符可以省略不写，IDE会帮你自动补全，但是初学者建议写上，防止遗忘。
 */
public interface TestInterface01 {
    //常量：
    /*public static final*/ int NUM = 10;
    //抽象方法：
    /*public abstract*/ void a();
    /*public abstract*/ void b(int num);
    /*public abstract*/ int c(String name);
}
interface TestInterface02{
    void e();
    void f();
}
/*
5.类和接口的关系是什么？ 实现关系  类实现接口：
6.一旦实现一个接口，那么实现类要重写接口中的全部的抽象方法：
7.如果没有全部重写抽象方法，那么这个类可以变成一个抽象类。
8.java只有单继承，java还有多实现
一个类继承其他类，只能直接继承一个父类
但是实现类实现接口的话，可以实现多个接口
9.写法：先继承 再实现：extends Person implements TestInterface01,TestInterface02
 */
class Student extends Person implements TestInterface01,TestInterface02 {
    @Override
    public void a() {
        System.out.println("---1");
    }
    @Override
    public void b(int num) {
        System.out.println("---2");
    }
    @Override
    public int c(String name) {
        return 100;
    }
    @Override
    public void e() {
        System.out.println("---3");
    }
    @Override
    public void f() {
        System.out.println("---4");
    }
}
class Test{
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //10.接口不能创建对象：
        //TestInterface02 t = new TestInterface02();
        TestInterface02 t = new Student();//接口指向实现类 ---》多态
        //11.接口中常量如何访问：
        System.out.println(TestInterface01.NUM);
        System.out.println(Student.NUM);
        Student s = new Student();
        System.out.println(s.NUM);
        TestInterface01 t2 = new Student();
        System.out.println(t2.NUM);
    }
}
//【3】接口的作用是什么？
定义规则，只是跟抽象类不同地方在哪？它是接口不是类。
接口定义好规则之后，实现类负责实现即可。
//【4】
继承：子类对父类的继承
实现：实现类对接口的实现

手机  是不是  照相机  
继承：手机   extends 照相机     “is-a”的关系，手机是一个照相机 
上面的写法 不好：
实现：  手机    implements   拍照功能   “has-a”的关系，手机具备照相的能力
案例：飞机，小鸟，风筝
定义一个接口： Flyable

//【5】多态的应用场合：
（1）父类当做方法的形参，传入具体的子类的对象
（2）父类当做方法的返回值，返回的是具体的子类的对象
（3）接口当做方法的形参，传入具体的实现类的对象
（4）接口当做方法的返回值，返回的是具体的实现类的对象
//【6】接口和抽象类的区别：
1.抽象类：1、抽象类使用abstract修饰；2、抽象类不能实例化，即不能使用new关键字来实例化对象；3、含有抽象方法（使用abstract关键字修饰的方法）的类是抽象类，必须使用abstract关键字修饰；4、抽象类可以含有抽象方法，也可以不包含抽象方法，抽象类中可以有具体的方法；5、如果一个子类实现了父类（抽象类）的所有抽象方法，那么该子类可以不必是抽象类，否则就是抽象类；6、抽象类中的抽象方法只有方法体，没有具体实现；
2.接口： 1、接口使用interface修饰；2、接口不能被实例化；3、一个类只能继承一个类，但是可以实现多个接口； 4、接口中方法均为抽象方法；5、接口中不能包含实例域或静态方法（静态方法必须实现，接口中方法是抽象方法，不能实现）
```

### 2.1.13 接口(JDK1.8之后)

```java
//在JDK1.8之前，接口中只有两部分内容：
（1）常量：固定修饰符：public static final
（2）抽象方法：固定修饰符：public abstract 
//在JDK1.8之后，新增非抽象方法：
（1）被public default修饰的非抽象方法：
注意1：default修饰符必须要加上，否则出错
注意2：实现类中要是想重写接口中的非抽象方法，那么default修饰符必须不能加，否则出错。
（2）静态方法：
注意1：static不可以省略不写
注意2：静态方法不能重写

public interface TestInterface {
    //常量：
    public static final int NUM= 10;
    //抽象方法：
    public abstract void a();
    //public default修饰的非抽象方法：
    public default void b(){
        System.out.println("-------TestInterface---b()-----");
    }
}
class Test implements TestInterface{
    public void c(){
        //用一下接口中的b方法：
        b();//可以
        //super.b();不可以
        TestInterface.super.b();//可以
    }
    @Override
    public void a() {
        System.out.println("重写了a方法");
    }
    @Override
    public void b() {
    }
}
// ----------------------------------------------
public interface TestInterface2 {
    //常量：
    public static final int NUM = 10;
    //抽象方法：
    public abstract  void a();
    //public default非抽象方法；
    public default void b(){
        System.out.println("-----TestInterface2---b");
    }
    //静态方法：
    public static void c(){
        System.out.println("TestInterface2中的静态方法");
    }
}
class Demo implements TestInterface2{
    @Override
    public void a() {
        System.out.println("重写了a方法");
    }
    public static void c(){
        System.out.println("Demo中的静态方法");
    }
}
class A {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Demo d = new Demo();
        d.c();
        Demo.c();
        TestInterface2.c();
    }
}
//疑问：为什么要在接口中加入非抽象方法？？？
如果接口中只能定义抽象方法的话，那么我要是修改接口中的内容，那么对实现类的影响太大了，所有实现类都会受到影响。
现在在接口中加入非抽象方法，对实现类没有影响，想调用就去调用即可。
```

### 2.1.14 成员内部类

```java
package com.msb.test07;
/**
 * 1.类的组成：属性，方法，构造器，代码块（普通块，静态块，构造块，同步块），内部类
 * 2.一个类TestOuter的内部的类SubTest叫内部类， 内部类 ：SubTest  外部类：TestOuter
 * 3.内部类：成员内部类 (静态的，非静态的) 和  局部内部类（位置：方法内，块内，构造器内）
 * 4.成员内部类:
 *      里面属性，方法，构造器等
 *      修饰符：private，default，protect，public，final,abstract
 */
public class TestOuter {
    //非静态的成员内部类：
    public class D{
        int age = 20;
        String name;
        public void method(){
            //5.内部类可以访问外部类的内容
            /*System.out.println(age);
            a();*/
            int age = 30;
            //8.内部类和外部类属性重名的时候，如何进行调用：
            System.out.println(age);//30
            System.out.println(this.age);//20
            System.out.println(TestOuter.this.age);//10
        }
    }
    //静态成员内部类：
    static class E{
        public void method(){
            //6.静态内部类中只能访问外部类中被static修饰的内容
            /*System.out.println(age);
            a();*/
        }
    }
    //属性：
    int age = 10;
    //方法：
    public void a(){
        System.out.println("这是a方法");
        {
            System.out.println("这是一个普通块");
            class B{
            }
        }
        class A{
        }
        //7.外部类想要访问内部类的东西，需要创建内部类的对象然后进行调用
        D d = new D();
        System.out.println(d.name);
        d.method();
    }
    static{
        System.out.println("这是静态块");
    }
    {
        System.out.println("这是构造块");
    }
    //构造器：
    public TestOuter(){
        class C{
        }
    }
    public TestOuter(int age) {
        this.age = age;
    }
}
class Demo{
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建外部类的对象：
        TestOuter to = new TestOuter();
        to.a();
        //9.创建内部类的对象：
        //静态的成员内部类创建对象：
        TestOuter.E e = new TestOuter.E();
        //非静态的成员内部类创建对象：				//这里不太理解
        //错误：TestOuter.D d = new TestOuter.D();
        TestOuter t = new TestOuter();
        TestOuter.D d = t.new D();
    }
}

```

### 2.1.15 局部内部类

```java
package com.msb.test08;

public class TestOuter {
    //1.在局部内部类中访问到的变量必须是被final修饰的
    public void method(){
        final int num = 10;
        class A{
            public void a(){
                //num = 20;
                System.out.println(num);
            }
        }
    }
    //2.如果类B在整个项目中只使用一次，那么就没有必要单独创建一个B类，使用内部类就可以了
    public Comparable method2(){
        class B implements Comparable{
            @Override
            public int compareTo(Object o) {
                return 100;
            }
        }
        return new B();
    }
    public Comparable method3(){
        //3.匿名内部类
        return new Comparable(){
            @Override
            public int compareTo(Object o) {
                return 200;
            }
        };
    }
    public void test(){
        Comparable com = new Comparable(){
            @Override
            public int compareTo(Object o) {
                return 200;
            }
        };
        System.out.println(com.compareTo("abc"));
    }
}
```

## 2.2 异常

### 2.2.1 try-catch

```java
//原理：
把可能出现异常的代码放入try代码块中，然后将异常封装为对象，被catch后面的()中的那个异常对象接收，接收以后：执行catch后面的{}里面的代码，然后try-catch后面的代码，该怎么执行就怎么执行。
//详细说一下：
（1）try中没有异常，catch中代码不执行。
（2）try中有异常，catch进行捕获：
如果catch中异常类型和你出的异常类型匹配的话：走catch中的代码--》进行捕获
如果catch中异常类型和你出的异常类型不匹配的话：不走catch中的代码--》没有捕获成功，程序相当于遇到异常了，中断了，后续代码不执行
//注意：
（1）try中如果出现异常，然后用catch捕获成功的话，那么try中后续的代码是不会执行的。
（2）如果catch捕获异常成功，那么try-catch后面的代码该执行还是执行没有影响。
```

### 2.2.2 finally

```java
//【1】在什么情况下，try-catch后面的代码不执行？
（1）throw抛出异常的情况
（2）catch中没有正常的进行异常捕获
（3）在try中遇到return

//【2】怎么样才可以将 try-catch后面的代码  必须执行？
只要将必须执行的代码放入finally中，那么这个代码无论如何一定执行。

//【3】return和finally执行顺序？
先执行finally最后执行return

//【4】什么代码会放在finally中呢？
关闭数据库资源，关闭IO流资源，关闭socket资源。

//【5】有一句话代码很厉害，它可以让finally中代码不执行!
System.exit(0);//终止当前的虚拟机执行

public class Test {
    public static void main(String[] args) {
        //实现一个功能：键盘录入两个数，求商：
        try{
            Scanner sc = new Scanner(System.in);
            System.out.println("请录入第一个数：");
            int num1 = sc.nextInt();
            System.out.println("请录入第二个数：");
            int num2 = sc.nextInt();
            System.out.println("商："+num1/num2);
            System.exit(0);//终止当前的虚拟机执行
            return;
        }catch(ArithmeticException ex){
            //throw ex;
        }finally {
            System.out.println("----谢谢你使用计算器!!!");
        }
    }
}
```

### 2.2.3 异常的分类

<img src="..\..\images\Java_ExceptionClass.png" alt="Java_ExceptionClass" style="zoom: 50%;" />

### 2.2.4 throw和throws的区别

```java
总结：
throw和throws的区别：
（1）位置不同：
throw: 出现在函数体
throws: 出现在方法函数头

（2）内容不同：
throw+异常对象（检查异常，运行时异常）
throws+异常的类型（可以多个类型，用，拼接）

（3）作用不同：
throw: 异常出现的源头，制造异常。抛出了异常，执行throw则一定抛出了某种异常对象。
throws: 表示出现异常的一种可能性，并不一定会发生这些异常。在方法的声明处，告诉方法的调用者，这个方法中可能会出现我声明的这些异常。然后调用者对这个异常进行处理：要么自己处理要么再继续向外抛出异常
```

2.2.4 自定义异常

```java
//自定义的异常可以继承：运行时异常
public class MyException extends RuntimeException {
    
    static final long serialVersionUID = -70348971907L;
    
    public MyException(){
    }
    public MyException(String msg){
        super(msg);
    }
}
//也可以继承检查异常：
public class MyException extends Exception {
    static final long serialVersionUID = -70348971907L;
    public MyException(){
    }
    public MyException(String msg){
        super(msg);
    }
}
//如果继承的是运行时异常，那么在使用的时候无需额外处理
//如果继承的是检查异常，那么使用的时候需要try-catch捕获或者throws向上抛
```

## 2.3 常用类

### 2.3.1 包装类

```java
【1】什么是包装类：
以前定义变量，经常使用基本数据类型，
对于基本数据类型来说，它就是一个数，加点属性，加点方法，加点构造器，
将基本数据类型对应进行了一个封装，产生了一个新的类，---》包装类。
int,byte.....--->基本数据类型
包装类--->引用数据类型

【2】对应关系：
基本数据类型          对应的包装类                继承关系
byte                    Byte                       ---》Number---》Object
short                   Short                      ---》Number---》Object
int                     Integer                    ---》Number---》Object
long                    Long                       ---》Number---》Object
float                   Float                      ---》Number---》Object
double                  Double                     ---》Number---》Object
char                    Character                  Object
boolean                 Boolean                    Object

【3】已经有基本数据类型了，为什么要封装为包装类？
（1）java语言 面向对象的语言，最擅长的操作各种各样的类。
（2）以前学习装数据的---》数组，int[]  String[]  double[]   Student[]
     以后学习的装数据的---》集合，有一个特点，只能装引用数据类型的数据

【4】是不是有了包装类以后就不用基本数据类型了？
不是。
```

### 2.3.2 Integer

```java
【1】直接使用，无需导包：
java.lang.Integer

【2】类的继承关系：
java.lang.Integer -> java.lang.Number -> java.lang.Object

【3】实现接口：
所有已实现接口：Serializable，Comparable<Integer>

【4】这个类被final修饰，那么这个类不能有子类，不能被继承：
public final class Integer extends Number implements Comparable<Integer>{}

【5】包装类是对基本数据类型的封装： 对int类型封装产生了Integer
Integer 类对象包装了一个基本数据类型 int 的值。 Integer 类型的对象包含了一个 int 类型的字段。

【6】类的历史：
从JDK1.0开始

【7】属性：
//属性：
System.out.println(Integer.MAX_VALUE);
System.out.println(Integer.MIN_VALUE);
//“物极必反”原理：
System.out.println(Integer.MAX_VALUE+1);
System.out.println(Integer.MIN_VALUE-1);

【8】构造器（发现没有空参构造器）
（1）int类型作为构造器的参数：
Integer i1 = new Integer(12);
（2）String类型作为构造器的参数：
Integer i2 = new Integer("12");
Integer i3 = new Integer("abcdef"); //报错

【9】包装类特有的机制：自动装箱  自动拆箱：
Integer i = 12;	//自动装箱：int--->Integer
System.out.println(i);

Integer i2 = new Integer(12);	
int num = i2;	//自动拆箱：Integer--->int
System.out.println(num);
（1）自动装箱  自动拆箱 ：是从JDK1.5以后新出的特性
（2）自动装箱  自动拆箱 ：将基本数据类型和包装类进行快速的类型转换。
//经过反编译后是这样的
Integer i = Integer.valueOf(12);//自动装箱：int--->Integer
System.out.println(i);

Integer i2 = new Integer(12);		
int num = i2.intValue;			//自动拆箱：Integer--->int
System.out.println(num);
```

### 2.3.3 Integer常用类

```java
【10】Integer常用方法：
注意去看valueOf方法的底层
public static Integer valueOf(int i) {
	if (i >= IntegerCache.low && i <= IntegerCache.high)
		return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
//cache作为缓冲。这是JDK在1.5版本中添加的一项新特性，把-128~127的数字缓存起来了，用于提升性能和节省内存。所以这个范围内的自动装箱（相当于调用valueOf(int i)方法）的数字都会从缓存中获取，而我们通过new Integer(1)这样就不会从缓存中获取。
private static class IntegerCache {
        static final int low = -128;
        static final int high;
        static final Integer cache[];
        static {
            int h = 127;
            high = h;
            cache = new Integer[(high - low) + 1];
            int j = low;
            for(int k = 0; k < cache.length; k++)
                cache[k] = new Integer(j++);
        }
	private IntegerCache() {}
}

【11】测试方法
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //compareTo：只返回三个值：要么是0,-1,1
        Integer i1 = new Integer(6);
        Integer i2 = new Integer(12);
        System.out.println(i1.compareTo(i2));// return (x < y) ? -1 : ((x == y) ? 0 : 1);
        //equals:Integer对Object中的equals方法进行了重写，比较的是底层封装的那个value的值。
        //Integer对象是通过new关键字创建的对象：
        Integer i3 = new Integer(12);
        Integer i4 = new Integer(12);
        System.out.println(i3 == i4);//false 因为==比较的是两个对象的地址
        boolean flag = i3.equals(i4);
        System.out.println(flag);
        //Integer对象通过自动装箱来完成：
        Integer i5 = 130;
        Integer i6 = 130;
        System.out.println(i5.equals(i6));//true
        System.out.println(i5 == i6);
        /*
        如果自动装箱值在-128~127之间，那么比较的就是具体的数值
        否在，比较的就是对象的地址
         */
        //intValue() :作用将Integer--->int
        Integer i7 = 130;
        int i = i7.intValue();
        System.out.println(i);
        //parseInt(String s) :String--->int:
        int i8 = Integer.parseInt("12");
        System.out.println(i8);
        //toString:Integer--->String
        Integer i10 = 130;
        System.out.println(i10.toString());
    }
}
```

### 2.3.4 java.util.Date

```java
public static void main(String[] args) {
    //java.util.Date:
    Date d = new Date();
    System.out.println(d);
    System.out.println(d.toString());
    System.out.println(d.toGMTString());//过期方法，过时方法，废弃方法。
    System.out.println(d.toLocaleString());
    System.out.println(d.getYear());//120+1900=2020
    System.out.println(d.getMonth());//5 :返回的值在 0 和 11 之间，值 0 表示 1 月。
    //返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。
    System.out.println(d.getTime());//1592055964263
    System.out.println(System.currentTimeMillis());
    /*
        （1）疑问：以后获取时间差用：getTime()还是currentTimeMillis()
        答案：currentTimeMillis()--》因为这个方法是静态的，可以类名.方法名直接调用
        （2）public static native long currentTimeMillis();
        本地方法
        为什么没有方法体？因为这个方法的具体实现不是通过java写的。
        （3）这个方法的作用：
        一般会去衡量一些算法所用的时间
         */
    long startTime = System.currentTimeMillis();
    for (int i = 0; i < 100000; i++) {
        System.out.println(i);
    }
    long endTime = System.currentTimeMillis();
    System.out.println(endTime-startTime);
}
```

### 2.3.5 java.sql.Date

```java
import java.sql.Date;
public static void main(String[] args) {
    //java.sql.Date:
    Date d = new Date(1592055964263L);
    System.out.println(d);
    /*
        (1)java.sql.Date和java.util.Date的区别：
        java.util.Date：年月日  时分秒
        java.sql.Date：年月日
        (2)java.sql.Date和java.util.Date的联系：
        java.sql.Date(子类) extends java.util.Date （父类）
         */
    //java.sql.Date和java.util.Date相互转换：
    //【1】util--->sql:
    java.util.Date date = new Date(1592055964263L);//创建util.Date的对象	注意这里的多态
    //方式1：向下转型
    Date date1 = (Date) date;
    /*
        父类：Animal 子类：Dog
        Animal an = new Dog();
        Dog d = (Dog)an;
         */
    //方式2：利用构造器
    Date date2 = new Date(date.getTime());
    //【2】sql-->util:
    java.util.Date date3 = d;
    //[3]String--->sql.Date:
    Date date4 = Date.valueOf("2019-3-8");
}
```

### 2.3.6 SimpleDateFormat

```java
【1】String---》java.util.Date 类型转换：
分解：
（1）String--->java.sql.Date
（2）java.sql.Date--->java.util.Date
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //（1）String--->java.sql.Date
        java.sql.Date date = java.sql.Date.valueOf("2015-9-24");
        //（2）java.sql.Date--->java.util.Date
        java.util.Date date2 = date;
        System.out.println(date2.toString());
    }
}
//上面的代码有局限性，字符串的格式只能是年-月-日拼接的形式，换成其它类型，就会出现异常：
【2】引入新的类：SimpleDateFormat
public class Test01{
    public static void main(String[] args) throws ParseException {
        //日期转换：
        //SimpleDateFormat(子类) extends DateFormat（父类是一个抽象类,不能创建对象）
        //格式化的标准已经定义好了：
        DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        //String--->Date
        Date d = df.parse("2019-4-6 12:23:54");
        System.out.println(d);
        //Date--->String
        String format = df.format(new Date());
        System.out.println(format);

        Date date = new Date();
        System.out.println(date.toString());
        System.out.println(date.toGMTString());
        System.out.println(date.toLocaleString());
    }
}
```

日期格式：

<img src="..\..\images\Java_SimpleDateFormat.png" alt="Java_SimpleDateFormat" style="zoom:67%;" />

### 2.3.7 Calendar

```java
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //Calendar是一个抽象类，不可以直接创建对象
        //GregorianCalendar()子类 extends Calendar（父类是一个抽象类）
        Calendar cal = new GregorianCalendar();
        Calendar cal2 = Calendar.getInstance();
        System.out.println(cal);
        //常用的方法：
        // get方法，传入参数：Calendar中定义的常量
        System.out.println(cal.get(Calendar.YEAR));
        System.out.println(cal.get(Calendar.MONTH));
        System.out.println(cal.get(Calendar.DATE));
        System.out.println(cal.get(Calendar.DAY_OF_WEEK));
        System.out.println(cal.getActualMaximum(Calendar.DATE));//获取当月日期的最大天数
        System.out.println(cal.getActualMinimum(Calendar.DATE));//获取当月日期的最小天数
        // set方法：可以改变Calendar中的内容
        cal.set(Calendar.YEAR,1990);
        cal.set(Calendar.MONTH,3);
        cal.set(Calendar.DATE,16);
        System.out.println(cal);
        //String--->Calendar:
        //分解：
        //String--->java.sql.Date:
        java.sql.Date date = java.sql.Date.valueOf("2020-4-5");
        //java.sql.Date-->Calendar:
        cal.setTime(date);
        System.out.println(cal);
    }
}
```

### 2.3.8 LocalDate、LocalTime、LocalDateTime

```java
//JDK1.0中使用java.util.Date类 --》第一批日期时间API
//JDK1.1引入Calendar类 --》第二批日期时间API
//缺陷：
//可变性 : 像日期和时间这样的类应该是不可变的。
//偏移性 : Date中的年份是从1900开始的，而月份都从0开始。
//格式化 : 格式化只对Date有用，Calendar则不行。
//JDK1.8新增日期时间API --》第三批日期时间API
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //1.完成实例化：
        //方法1：now()--获取当前的日期，时间，日期+时间
        LocalDate localDate = LocalDate.now();
        System.out.println(localDate);
        LocalTime localTime = LocalTime.now();
        System.out.println(localTime);
        LocalDateTime localDateTime = LocalDateTime.now();
        System.out.println(localDateTime);
        //方法2：of()--设置指定的日期，时间，日期+时间
        LocalDate of = LocalDate.of(2010, 5, 6);
        System.out.println(of);
        LocalTime of1 = LocalTime.of(12, 35, 56);
        System.out.println(of1);
        LocalDateTime of2 = LocalDateTime.of(1890, 12, 23, 13, 24, 15);
        System.out.println(of2);
        //LocalDate,LocalTime用的不如LocalDateTime多
        //下面讲解用LocalDateTime：
        //一些列常用的get***
        System.out.println(localDateTime.getYear());//2020
        System.out.println(localDateTime.getMonth());//JUNE
        System.out.println(localDateTime.getMonthValue());//6
        System.out.println(localDateTime.getDayOfMonth());//14
        System.out.println(localDateTime.getDayOfWeek());//SUNDAY
        System.out.println(localDateTime.getHour());//22
        System.out.println(localDateTime.getMinute());//22
        System.out.println(localDateTime.getSecond());//6
        //不是set方法，叫with
        //体会：不可变性
        LocalDateTime localDateTime2 = localDateTime.withMonth(8);
        System.out.println(localDateTime);
        System.out.println(localDateTime2);
        //提供了加减的操作：
        //加：
        LocalDateTime localDateTime1 = localDateTime.plusMonths(4);
        System.out.println(localDateTime);
        System.out.println(localDateTime1);
        //减：
        LocalDateTime localDateTime3 = localDateTime.minusMonths(5);
        System.out.println(localDateTime);
        System.out.println(localDateTime3);
    }
}
```

### 2.3.9 DateTimeFormatter

```java
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //格式化类：DateTimeFormatter
        //方式一:预定义的标准格式。如: ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;IS0_LOCAL_TIME
        DateTimeFormatter df1 = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
        //df1就可以帮我们完成LocalDateTime和String之间的相互转换：
        //LocalDateTime-->String:
        LocalDateTime now = LocalDateTime.now();
        String str = df1.format(now);
        System.out.println(str);//2020-06-15T15:02:51.29
        //String--->LocalDateTime
        TemporalAccessor parse = df1.parse("2020-06-15T15:02:51.29");
        System.out.println(parse);
        //方式二:本地化相关的格式。如: oflocalizedDateTime()
        //参数：FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT
        //FormatStyle.LONG :2020年6月15日 下午03时17分13秒
        //FormatStyle.MEDIUM: 2020-6-15 15:17:42
        //FormatStyle.SHORT:20-6-15 下午3:18
        DateTimeFormatter df2 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.SHORT);
        //LocalDateTime-->String:
        LocalDateTime now1 = LocalDateTime.now();
        String str2 = df2.format(now1);
        System.out.println(str2);
        //String--->LocalDateTime
        TemporalAccessor parse1 = df2.parse("20-6-15 下午3:18");
        System.out.println(parse1);
        //方式三: 自定义的格式。如: ofPattern( "yyyy-MM-dd hh:mm:ss") ---》重点，以后常用
        DateTimeFormatter df3 = DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss");
        //LocalDateTime-->String:
        LocalDateTime now2 = LocalDateTime.now();
        String format = df3.format(now2);
        System.out.println(format);//2020-06-15 03:22:03
        //String--->LocalDateTime
        TemporalAccessor parse2 = df3.parse("2020-06-15 03:22:03");
        System.out.println(parse2);
    }
}
```

### 2.3.10 Math类

```java
【1】直接使用，无需导包：
【2】final修饰类，这个类不能被继承：
【3】构造器私有化，不能创建Math类的对象：
【4】Math内部的所有的属性，方法都被static修饰：类名.直接调用，无需创建对象：
【5】常用方法：
//静态导入：这样可以去掉Math
import static java.lang.Math.*;
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //常用属性：
        System.out.println(Math.PI);
        //常用方法：
        System.out.println("随机数："+Math.random());//[0.0,1.0)
        System.out.println("绝对值："+Math.abs(-80));
        System.out.println("向上取值："+Math.ceil(9.1));
        System.out.println("向下取值："+Math.floor(9.9));
        System.out.println("四舍五入："+Math.round(3.5));
        System.out.println("取大的那个值："+Math.max(3, 6));
        System.out.println("取小的那个值："+Math.min(3, 6));
    }
}
```

### 2.3.11 Random类

```java
public static void main(String[] args) throws ParseException {
    //返回带正号的 double 值，该值大于等于 0.0 且小于 1.0。
    System.out.println("随机数："+Math.random());
    //学习Random类
    //（1）利用带参数的构造器创建对象：
    Random r1 = new Random(System.currentTimeMillis());
    int i = r1.nextInt();
    System.out.println(i);
    //（2）利用空参构造器创建对象：
    Random r2 = new Random();//表面是在调用无参数构造器，实际底层还是调用了带参构造器
    System.out.println(r2.nextInt(10));//在 0（包括）和指定值（不包括）之间均匀分布的 int 值。
    System.out.println(r2.nextDouble());//在 0.0 和 1.0 之间均匀分布的 double 值。
}
```

### 2.3.12 String

```java
//String的本质
【1】直接使用，无需导包：
【2】这个String类不可以被继承，不能有子类：
【3】String底层是一个char类型的数组

//String常用方法
【1】构造器：底层就是给对象底层的value数组进行赋值操作。
 //通过构造器来创建对象：
String s1 = new String();
String s2 = new String("abc");
String s3 = new String(new char[]{'a','b','c'});
【2】常用方法：
String s4 = "abc";
System.out.println("字符串的长度为："+s4.length());
String s5 = new SZtring("abc");
System.out.println("字符串是否为空："+s5.isEmpty());
System.out.println("获取字符串的下标对应的字符为："+s5.charAt(1));
【3】equals:
String s6 = new String("abc");
String s7 = new String("abc");
System.out.println(s6.equals(s7));
【4】String类实现了Comparable，里面有一个抽象方法叫compareTo，所以String中一定要对这个方法进行重写：
String s8 = new String("abc");
String s9 = new String("abc");
//如果两个字符串中有字符不一样,返回这两个字符差值。前面字符一样,如果两个字符串长度不一样返回长度的差值。
//如果两个字符串相同,返回0
System.out.println(s8.compareTo(s9)); 
【5】常用方法：
//字符串的截取：
String s10 = "abcdefhijk";
System.out.println(s10.substring(3));//3到最后
System.out.println(s10.substring(3, 6));//[3,6)
//字符串的合并/拼接操作：
System.out.println(s10.concat("pppp"));
//字符串中的字符的替换：
String s11 = "abcdeahija";
System.out.println(s11.replace('a', 'u'));
//按照指定的字符串进行分裂为数组的形式：
String s12 = "a-b-c-d-e-f";
String[] strs = s12.split("-");
System.out.println(Arrays.toString(strs));
//转大小写的方法：
String s13 = "abc";
System.out.println(s13.toUpperCase());
System.out.println(s13.toUpperCase().toLowerCase());
//去除收尾空格：
String s14 = "    a  b  c    ";
System.out.println(s14.trim());
//toString()
String s15 = "abc";
System.out.println(s15.toString());
//转换为String类型：
System.out.println(String.valueOf(false));
```

### 2.3.13 String内存分析

```java
【1】字符串拼接：
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        String s1 = "a"+"b"+"c";
        String s2 = "ab"+"c";
        String s3 = "a"+"bc";
        String s4 = "abc";
        String s5 = "abc"+"";
    }
}
//上面的字符串，会进行编译器优化，直接合并成为完整的字符串，我们可以反编译验证：
public class Test {
    public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "abc";
        String s3 = "abc";
        String s4 = "abc";
        String s5 = "abc";
    }
}
【2】new关键字创建对象：
String s6 = new String("abc");
内存：开辟两个空间（1.字符串常量池中的字符串 2.堆中的开辟的空间）
```

### 2.3.14 StringBuilder类

```java
//【1】字符串的分类：
（1）不可变字符串：String
（2）可变字符串：StringBuilder，StringBuffer
//【2】StringBuilder底层：非常重要的两个属性：
char[] value;	// 就是StringBuilder底层的存储
int count;		// 指的是value数组中被使用的长度
//【3】对应内存分析：
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建StringBuilder的对象：
        StringBuilder sb3 = new StringBuilder();
        //表面上调用StringBuilder的空构造器，实际底层是对value数组进行初始化，长度为16
        StringBuilder sb2 = new StringBuilder(3);
        //表面上调用StringBuilder的有参构造器，传入一个int类型的数，实际底层就是对value数组进行初始化，长度为你传入的数字
        StringBuilder sb = new StringBuilder("abc");
        System.out.println(sb.append("def").append("aaaaaaaa");//链式调用方式：return this
    }
}
```

### 2.3.15 可变和不可变字符串

```java
//【1】String---》不可变
String a = "abc";
a = "abcdef";	// 在地址不变的情况下，想把"abc"变成"abcdef"是不可能的
//【2】StringBuilder---》可变
可变，在StringBuilder这个对象的地址不变的情况下，想把“abc”变成“abcdef”是可能的，直接追加即可
StringBuilder sb = new StringBuilder();
System.out.println(sb.append("abc")==sb.append("def"));//true
```

### 2.3.16 StringBuilder常用方法

```java
//这是一个main方法，是程序的入口：
public static void main(String[] args) {
    StringBuilder sb=new StringBuilder("nihaojavawodeshijie");
    //增
    sb.append("这是梦想");
    //删
    sb.delete(3, 6);//删除位置在[3,6)上的字符
    sb.deleteCharAt(16);//删除位置在16上的字符
    //改-->插入
    StringBuilder sb1=new StringBuilder("$23445980947");
    sb1.insert(3, ",");//在下标为3的位置上插入 ,
    StringBuilder sb2=new StringBuilder("$2你好吗5980947");
    //改-->替换
    sb2.replace(3, 5, "我好累");//在下标[3,5)位置上插入字符串
    sb.setCharAt(3, '!');
    //查
    StringBuilder sb3=new StringBuilder("asdfa");
    for (int i = 0; i < sb3.length(); i++) {
        System.out.print(sb3.charAt(i)+"\t");
    }
    System.out.println();
    //截取
    String str=sb3.substring(2,4);//截取[2,4)返回的是一个新的String，对StringBuilder没有影响
}
```

### 2.3.17 String、StringBuffer、StringBuilder区别与联系

```java
1. String类是不可变类，即一旦一个String对象被创建后，包含在这个对象中的字符序列是不可改变的，直至这个对象销毁。
2. StringBuffer类则代表一个字符序列可变的字符串，可以通过append、insert、reverse、setChartAt、setLength等方法改变其内容。一旦生成了最终的字符串，调用toString方法将其转变为String
3. JDK1.5新增了一个StringBuilder类，与StringBuffer相似，构造方法和方法基本相同。不同是StringBuffer是线程安全的，而StringBuilder是线程不安全的，所以性能略高。通常情况下，创建一个内容可变的字符串，应该优先考虑使用StringBuilder
	StringBuilder:JDK1.5开始  效率高   线程不安全
	StringBuffer:JDK1.0开始   效率低    线程安全
```

## 2.4 集合

### 2.4.1 集合的分类

<img src="..\..\images\Java_SetClass.jpg" alt="Java_SetClass" style="zoom: 50%;" />

### 2.4.2 Collection 接口常用方法

```java
public static void main(String[] args) throws ParseException {
    /*
        Collection接口的常用方法：
        增加：add(E e) addAll(Collection<? extends E> c)
        删除：clear() remove(Object o)
        修改：
        查看：iterator() size()
        判断：contains(Object o)  equals(Object o) isEmpty()
         */
    //创建对象：接口不能创建对象，利用实现类创建对象：
    Collection col = new ArrayList();
    //调用方法：
    //集合有一个特点：只能存放引用数据类型的数据，不能是基本数据类型
    //基本数据类型自动装箱，对应包装类。int--->Integer
    col.add(18);
    col.add(12);
    col.add(11);
    col.add(17);
    System.out.println(col/*.toString()*/);
    List list = Arrays.asList(new Integer[]{11, 15, 3, 7, 1});
    col.addAll(list);//将另一个集合添加入col中
    System.out.println(col);
    //col.clear();清空集合
    System.out.println(col);
    System.out.println("集合中元素的数量为："+col.size());
    System.out.println("集合是否为空："+col.isEmpty());
    boolean isRemove = col.remove(15);
    System.out.println(col);
    System.out.println("集合中数据是否被删除："+isRemove);
    Collection col2 = new ArrayList();
    col2.add(18);
    col2.add(12);
    col2.add(11);
    col2.add(17);
    Collection col3 = new ArrayList();
    col3.add(18);
    col3.add(12);
    col3.add(11);
    col3.add(17);
    System.out.println(col2.equals(col3));
    System.out.println(col2==col3);//地址一定不相等  false
    System.out.println("是否包含元素："+col3.contains(117));
}
```

### 2.4.3 Collection 集合的遍历

```java
//遍历方式：1.增强for循环	2.迭代器
//这是main方法，程序的入口
public static void main(String[] args) {
    Collection col = new ArrayList();
    col.add(18);
    col.add(12);
    col.add(11);
    col.add(17);
    col.add("abc");
    col.add(9.8);
    //对集合遍历（对集合中元素进行查看）
    //方式1：普通for循环   失败,不能用此方法进行遍历
    /*for(int i= 0;i<col.size();i++){
            col.
        }*/
    //方式2：增强for循环   需要使用object来接收对象,因为可以存入多种类型的数据
    for(Object o:col){
        System.out.println(o);
    }
    System.out.println("------------------------");
    //方式3：iterator()
    Iterator it = col.iterator();
    while(it.hasNext()){
        System.out.println(it.next());
    }
}
```

### 2.4.4 List接口的常用方法和遍历方式

```java
//这是main方法，程序的入口
public static void main(String[] args) {
    /*
        List接口中常用方法：
        增加：add(int index, E element)
        删除：remove(int index)  remove(Object o)
        修改：set(int index, E element)
        查看：get(int index)
        判断：
         */
    List list = new ArrayList();
    list.add(13);
    list.add(17);
    list.add(6);
    list.add(-1);
    list.add(2);
    list.add("abc");
    System.out.println(list);
    list.add(3,66);
    System.out.println(list);
    list.set(3,77);
    System.out.println(list);
    list.remove(2);//在集合中存入的是Integer类型数据的时候，调用remove方法调用的是：remove(int index)
    System.out.println(list);
    list.remove("abc");
    System.out.println(list);
    Object o = list.get(0);
    System.out.println(o);
    //List集合 遍历： 三种遍历方法
    //方式1：普通for循环：
    System.out.println("---------------------");
    for(int i = 0;i<list.size();i++){
        System.out.println(list.get(i));
    }
    //方式2：增强for循环：
    System.out.println("---------------------");
    for(Object obj:list){
        System.out.println(obj);
    }
    //方式3：迭代器：
    System.out.println("---------------------");
    Iterator it = list.iterator();
    while(it.hasNext()){
        System.out.println(it.next());
    }
}
```

### 2.4.5 ArrayList实现类（JDK1.7 和 JDK1.8 区别）

```java
//接口=实现类 推荐这样使用
Collection col = new ArrayList();
List list = new ArrayList();
//直接创建实现类对象
ArrayList al = new ArrayList();

// JDK1.7
// 1.ArrayList继承了AbstractList并且实现了List接口,但是AbstractList已经实现了List接口。这是一个错误，但Josh Bloch(Java集合框架的创始者)当时以为这样做有用，后续的JDK也未对其进行修改。
// 2.底层重要属性：
transient Object[] elementData; // 底层的数组，数组类型Object类型
private int size;	// 数组中的有效数据
在JDK1.7中：在调用构造器的时候给底层数组elementData初始化，数组初始化长度为10：
调用add方法：
ArrayList al = new ArrayList(10);
System.out.println(al.add("abc"));	//添加成功返回true
System.out.println(al.add("def"));

// JDK1.8
// 1.JDK1.8底层依旧是Object类型的数组，size:数组中有效长度：
transient Object[] elementData; // 底层的数组，数组类型Object类型
private int size;	// 数组中的有效数据
// 2.ArrayList al = new ArrayList();调用空构造器：
在JDK1.8中，在调用空构造器的时候，底层elementData数组的初始化为{}

// 总结
// JDK1.7源码
底层数组，在调用构造器的时候，数组长度初始化为10，当数组中的10个位置都满了的时候就开始进行数组的扩容，扩容长度为 原数组的1.5倍：将elementData的指向从老数组变为新数组：扩容的本质。将老数组中的内容复制到新数组中，然后返回新数组。
// JDK1.8源码
底层数组，在调用构造器的时候，底层数组为{}，在调用add方法以后，底层数组才重新赋值为新数组，新数组的长度为10--->节省内存，在add后才创建长度为10的数组。
```

### 2.4.6 Vector实现类

```java
【1】属性
protected Object[] elementData;	//底层Object数组
protected int elementCount;	//数组中有效长度
【2】调用构造器
List vector = new Vector();
【3】add方法
底层扩容数组长度的2倍

//Vector和ArrayList联系区别总结：
联系：底层都是数组的扩容
区别：
ArrayList底层扩容长度为原数组的1.5倍  线程不安全  效率高
Vector底层扩容长度为原数组的2倍  线程安全  效率低

数组优点：查询效率高	特点：数组可重复
数组缺点：删除，增加元素效率低
```

### 2.4.7 泛型

```java
【1】什么是泛型（Generic）：
泛型就相当于标签
形式：<>  
集合容器类在设计阶段/声明阶段不能确定这个容器到底实际存的是什么类型的对象，所以在JDK1.5之前只能把元素类型设计为Object，
JDK1.5之 后使用泛型来解决。因为这个时候除了元素的类型不确定，其他的部分是确定的，例如关于这个元素如何保存，如何管理等是确定的，因此此时把元素的类型设计成一个参数，这个类型参数叫做泛型。
Collection<E>, List<E>， ArrayList<E> 这个<E>就是类型参数，即泛型。

【2】没有泛型的时候使用集合：
//这是main方法，程序的入口
public static void main(String[] args) {
     //创建一个ArrayList集合，向这个集合中存入学生的成绩：
     ArrayList al = new ArrayList();
     al.add(98);
     al.add(18);
     al.add(39);
     al.add(60);
     al.add(83);
     al.add("丽丽");
     //对集合遍历查看：
     for(Object obj:al){
        System.out.println(obj);
	}
}
如果不使用泛型的话，有缺点：一般我们在使用的时候基本上往集合中存入的都是相同类型的数据--》便于管理，所以现在什么引用数据类型都可以存入集合，不方便！
【3】JDK1.5以后开始使用泛型，集合中使用泛型：
//这是main方法，程序的入口
public static void main(String[] args) {
	//创建一个ArrayList集合，向这个集合中存入学生的成绩：
	//加入泛型的优点：在编译时期就会对类型进行检查，不是泛型对应的类型就不可以添加入这个集合。
	ArrayList<Integer> al = new ArrayList<Integer>();
	al.add(98);
	al.add(18);
	al.add(39);
	al.add(60);
	al.add(83);
	/*al.add("丽丽");	
	al.add(9.8);*/
	//对集合遍历查看：
	/*for(Object obj:al){
		System.out.println(obj);
	}*/
	for(Integer i:al){
		System.out.println(i);
	}
}
【4】泛型总结：
（1）JDK1.5以后
（2）泛型实际就是 一个<>引起来的 参数类型，这个参数类型  具体在使用的时候才会确定具体的类型。
（3）使用了泛型以后，可以确定集合中存放数据的类型，在编译时期就可以检查出来。
（4）使用泛型你可能觉得麻烦，实际使用了泛型才会简单，后续的遍历等操作简单。
（5）泛型的类型：都是引用数据类型，不能是基本数据类型。
（6）ArrayList<Integer> al = new ArrayList<Integer>();在JDK1.7以后可以写为：
ArrayList<Integer> al = new ArrayList<>();  --<>  ---钻石运算符
```

### 2.4.8 泛型类，泛型接口

```java
【1】泛型类的定义和实例化：
/**
 * GenericTes就是一个普通的类
 * GenericTest<E> 就是一个泛型类
 * <>里面就是一个参数类型，但是这个类型是什么呢？这个类型现在是不确定的，相当于一个占位
 * 但是现在确定的是这个类型一定是一个引用数据类型，而不是基本数据类型
 */
public class GenericTest<E> {
    int age;
    String name;
    E sex;
    public void a(E n){
    }
    public void b(E[] m){
    }
}
class Test{
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //GenericTest进行实例化：
        //(1)实例化的时候不指定泛型：如果实例化的时候不明确的指定类的泛型，那么认为此泛型为Object类型
        GenericTest gt1 = new GenericTest();
        gt1.a("abc");
        gt1.a(17);
        gt1.a(9.8);
        gt1.b(new String[]{"a","b","c"});
        //（2）实例化的时候指定泛型：---》推荐方式
        GenericTest<String> gt2 = new GenericTest<>();
        gt2.sex = "男";
        gt2.a("abc");
        gt2.b(new String[]{"a","b","c"});
    }
}
【2】继承情况：
（1）父类指定泛型：
class SubGenericTest extends GenericTest<Integer>{
}
class Demo{
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //指定父类泛型，那么子类就不需要再指定泛型了，可以直接使用
        SubGenericTest sgt = new SubGenericTest();
        sgt.a(19);
    }
}
（2）父类不指定泛型：
如果父类不指定泛型，那么子类也会变成一个泛型类，那这个E的类型可以在创建子类对象的时候确定：
class SubGenericTest2<E> extends GenericTest<E>{
}
class Demo2{
    //这是main方法，程序的入口
    public static void main(String[] args) {
        SubGenericTest2<String> s = new  SubGenericTest2<>();
        s.a("abc");
        s.sex = "女";
    }
}
// 细节
// 泛型类可以定义多个参数类型
public class TestGeneric<A,B,C>{
	A age;
	B name;
	C sex;
	public void a(A a,B b,C c){
	
	}
	// 泛型类的构造器的写法
	public TestGeneric(A a,B b,C c){
		this.age = a;
		this.name = b;
		this.sex = c;
	}
	// 不同的泛型的引用类型不可以相互赋值：
	public void b(){
		ArrayList<String> list1 = null;
		ArrayList<Integer> list2 = null;
		list1 = list2;	//此句报错！！！
	}
	// 泛型类中的静态方法不能使用类的泛型： 因为static优先于对象存在
	public static int c(A a){	//此句报错！！！
		return 10;
	}
	// 不能直接使用E[]创建数组
	public void a(A a,B b,C c){
		//不可以: A[] i = new A[10]; //错误
		A[] i = (A[])new Object[10]; //正确
	}
}
```

### 2.4.9 泛型方法

```java
/**
 * 1.什么是泛型方法：
 * 不是带泛型的方法就是泛型方法
 * 泛型方法有要求：这个方法的泛型的参数类型要和当前的类的泛型无关
 * 换个角度：
 * 泛型方法对应的那个泛型参数类型 和  当前所在的这个类 是否是泛型类，泛型是啥  无关
 * 2.泛型方法定义的时候，前面要加上<T>
 *     原因：如果不加的话，会把T当做一种数据类型，然而代码中没有T类型那么就会报错
 * 3.T的类型是在调用方法的时候确定的
 * 4.泛型方法可否是静态方法？可以是静态方法
 */
public class TestGeneric<E> {
    //不是泛型方法 （不能是静态方法）
    public static void a(E e){
    }
    //是泛型方法
    public static <T>  void b(T t){
    }
}
class Demo{
    //这是main方法，程序的入口
    public static void main(String[] args) {
        TestGeneric<String> tg = new TestGeneric<>();
        tg.a("abc");
        tg.b("abc");
        tg.b(19);
        tg.b(true);
    }
}
```

### 2.4.10  泛型参数存在继承关系的情况

```java
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        Object obj = new Object();
        String s = new String();
        obj = s; //多态的一种形式

        Object[] objArr = new Object[10];
        String[] strArr = new String[10];
        objArr = strArr; //多态的一种形式

        List<Object> list1 = new ArrayList<>();
        List<String> list2 = new ArrayList<>();
        list1 = list2; //报错

        //总结: A和B是父类子类的关系，但是G<A>和G<B>不存在继承的关系，是并列关系。
    }
}
```

### 2.4.11 通配符

```java
【1】在没有通配符的时候：
下面的a方法，相当于方法的重复定义，报错
public class Test {
    /*public void a(List<Object> list){
    }
    public void a(List<String> list){
    }
    public void a(List<Integer> list){
    }*/
}
【2】引入通配符：
public class Demo {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        List<Object> list1 = new ArrayList<>();
        List<String> list2 = new ArrayList<>();
        List<Integer> list3 = new ArrayList<>();
        List<?> list = null;
        list = list1;
        list = list2;
        list = list3;
    }
}
发现： A 和 B是子类父类的关系，G<A>和G<B>不存在子类父类关系，是并列的
加入通配符？后，G<?>就变成了 G<A>和G<B>的父类
【3】使用通配符：
public class Test {
    /*public void a(List<Object> list){
    }
    public void a(List<String> list){
    }
    public void a(List<Integer> list){
    }*/
    public void a(List<?> list){
        //1.内部遍历的时候用Object即可，不用？
        for(Object a:list){
            System.out.println(a);
        }
        //2.数据的写入操作 ：不能写入
        //list.add("abc");-->出错，不能随意的添加数据
        list.add(null);
        //3.数据的读取操作：使用Object接收
        Object s = list.get(0)
    }
}
class T{
    //这是main方法，程序的入口
    public static void main(String[] args) {
        Test t = new Test();
        t.a(new ArrayList<Integer>());
        t.a(new ArrayList<String>());
        t.a(new ArrayList<Object>());
    }
}
```

### 2.4.12 泛型受限

```java
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //Student extends Person
        //a,b,c三个集合是并列的关系：
        List<Object> a = new ArrayList<>();
        List<Person> b = new ArrayList<>();
        List<Student> c = new ArrayList<>();
        /*开始使用泛型受限：泛型的上限
        List<? extends Person>:
        就相当于：
        List<? extends Person>是List<Person>的父类，是List<Person的子类>的父类
         */
        List<? extends Person> list1 = null;
//        list1 = a;  //报错
//        list1 = b;
//        list1 = c;
        /*开始使用泛型受限：泛型的下限
        List<? super Person>
        就相当于：
        List<? super Person>是List<Person>的父类，是List<Person的父类>的父类
         */
        List<? super Person> list2 = null;
//        list2 = a;
//        list2 = b;
//        list3 = c;  //报错
    }
}
```

### 2.4.13 LinkedList实现类的使用

```java
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        /*
        LinkedList常用方法：
        增加 addFirst(E e) addLast(E e)
             offer(E e) offerFirst(E e) offerLast(E e)
        删除 poll()
            pollFirst() pollLast()  ---》JDK1.6以后新出的方法，提高了代码的健壮性
            removeFirst() removeLast()
        修改
        查看 element()
             getFirst()  getLast()
             indexOf(Object o)   lastIndexOf(Object o)
             peek()
             peekFirst() peekLast()
        判断
         */
        //创建一个LinkedList集合对象：
        LinkedList<String> list = new LinkedList<>();
        list.add("aaaaa");
        list.add("bbbbb");
        list.add("ccccc");
        list.add("ddddd");
        list.add("eeeee");
        list.add("bbbbb");
        list.add("fffff");
        list.addFirst("jj");
        list.addLast("hh");
        list.offer("kk");//添加元素在尾端
        list.offerFirst("pp");
        list.offerLast("rr");
        System.out.println(list);//LinkedList可以添加重复数据
        System.out.println(list.poll());//删除头上的元素并且将元素输出
        System.out.println(list.pollFirst());
        System.out.println(list.pollLast());
        System.out.println(list.removeFirst());
        System.out.println(list.removeLast());
        System.out.println(list);//LinkedList可以添加重复数据
        /*list.clear();//清空集合
        System.out.println(list);*/
        /*System.out.println(list.pollFirst());*/
        /*System.out.println(list.removeFirst());报错：Exception in thread "main" java.util.NoSuchElementException*/
        //集合的遍历：
        System.out.println("---------------------");
        //普通for循环：
        for(int i = 0;i<list.size();i++){
            System.out.println(list.get(i));
        }
        System.out.println("---------------------");
        //增强for：
        for(String s:list){
            System.out.println(s);
        }
        System.out.println("---------------------");
        //迭代器：
        /*Iterator<String> it = list.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
        }*/
        //下面这种方式好，节省内存
        for(Iterator<String> it = list.iterator();it.hasNext();){
            System.out.println(it.next());
        }
    }
}

// ArrayList数据结构：
物理结构：紧密结构
逻辑结构：线性表(数组)
// LinkedList数据结构：
物理结构：跳转结构
逻辑结构：线性表(链表,双向链表)
```

### 2.4.14 Iterator和ListIterator区别

```java
我们在使用List,Set的时候，为了实现对其数据的遍历，我们经常使用到了Iterator(迭代器)。使用迭代器，你不需要干涉其遍历的过程，只需要每次取出一个你想要的数据进行处理就可以了。
但是在使用的时候也是有不同的。List和Set都有iterator()来取得其迭代器。对List来说，你也可以通过listIterator()取得其迭代器，两种迭代器在有些时候是不能通用的，Iterator和ListIterator主要区别在以下方面：

1. ListIterator有add()方法，可以向List中添加对象，而Iterator不能

2. ListIterator和Iterator都有hasNext()和next()方法，可以实现顺序向后遍历，但是ListIterator有hasPrevious()和previous()方法，可以实现逆向（顺序向前）遍历。Iterator就不可以。

3. ListIterator可以定位当前的索引位置，nextIndex()和previousIndex()可以实现。Iterator没有此功能。

4. 都可实现删除对象，但是ListIterator可以实现对象的修改，set()方法可以实现。Iierator仅能遍历，不能修改。

因为ListIterator的这些功能，可以实现对LinkedList等List数据结构的操作。其实，数组对象也可以用迭代器来实现。
```

### 2.4.15 HashSet的使用及简要原理

```java
//1.放入引用类型数据
public class TestInteger {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //创建一个HashSet集合：
        HashSet<Integer> hs = new HashSet<>();
        System.out.println(hs.add(19));//true
        hs.add(5);
        hs.add(20);
        System.out.println(hs.add(19));//false 这个19没有放入到集合中
        hs.add(41);
        hs.add(0);
        System.out.println(hs.size());//唯一，无序
        System.out.println(hs);
    }
}
//2.放入自定义的引用数据类型的数据
public class TestStudent {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //创建一个HashSet集合：
        HashSet<Student> hs = new HashSet<>();
        hs.add(new Student(19,"lili"));
        hs.add(new Student(20,"lulu"));
        hs.add(new Student(18,"feifei"));
        hs.add(new Student(19,"lili"));
        hs.add(new Student(10,"nana"));
        System.out.println(hs.size());	//输出5
        System.out.println(hs);		//这里的自定义的类型不满足 唯一,无序的特点。为什么呢？
    }
}
//3.HashSet原理
1.集合中存入的数据,(以Integer类型为案例)
2.调用对应的hashCode方法计算哈希值
3.通过哈希值和一个表达式计算在数组中存放的位置
HashSet底层原理：数组 + 链表 = 哈希表
注意：如果放入HashSet中的数据，一定要重写两个方法：hashCode、equals
```

### 2.4.16 LinkedHashSet原理

```java
LinkedHashSet其实就是在HashSet的基础上，多了一个总的链表，这个总链表将放入的元素串在一起，方便有序的遍历：
public class TestInteger {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //创建一个HashSet集合：
        LinkedHashSet<Integer> hs = new LinkedHashSet<>();
        System.out.println(hs.add(19));//true
        hs.add(5);
        hs.add(20);
        System.out.println(hs.add(19));//false 这个19没有放入到集合中
        hs.add(41);
        hs.add(0);
        System.out.println(hs.size());//唯一，无序
        System.out.println(hs);
    }
}
```

### 2.4.17 比较器的使用

```java
【1】以int类型为案例：
比较的思路：将比较的数据做差，然后返回一个int类型的数据，将这个int类型的数值  按照 =0  >0  <0
int a = 10;
int b = 20;
System.out.println(a-b); // =0  >0  <0
【2】比较String类型数据：
String类实现了Comparable接口，这个接口中有一个抽象方法compareTo，String类中重写这个方法即可
String a = "A";
String b = "B";
System.out.println(a.compareTo(b));
【3】比较double类型数据：
double a = 9.6;
double b = 9.3;
/* System.out.println((int)(a-b));*/
System.out.println(((Double) a).compareTo((Double) b));
【4】比较自定义的数据类型：
（1）内部比较器：	实现 Comparable<Student>接口
public class Student implements Comparable<Student>{
	//...
	@Override	//重写compareTo方法
    public int compareTo(Student o) {
        //按照年龄进行比较：
        /*return this.getAge() - o.getAge();*/
        //按照身高比较
        /*return ((Double)(this.getHeight())).compareTo((Double)(o.getHeight()));*/
        //按照名字比较：
        return this.getName().compareTo(o.getName());
    }
}
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //比较两个学生：
        Student s1 = new Student(14,160.5,"alili");
        Student s2 = new Student(14,170.5,"bnana");
        System.out.println(s1.compareTo(s2));
    }
}
（2）外部比较器：
class BiJiao01 implements Comparator<Student> {
    @Override
    public int compare(Student o1, Student o2) {
        //比较年龄：
        return o1.getAge()-o2.getAge();
    }
}
class BiJiao02 implements Comparator<Student> {
    @Override
    public int compare(Student o1, Student o2) {
        //比较姓名：
        return o1.getName().compareTo(o2.getName());
    }
}
class BiJiao03 implements Comparator<Student> {
    @Override
    public int compare(Student o1, Student o2) {
        //在年龄相同的情况下 比较身高  年龄不同比较年龄
        if((o1.getAge()-o2.getAge())==0){
            return ((Double)(o1.getHeight())).compareTo((Double)(o2.getHeight()));
        }else{//年龄不一样
            return o1.getAge()-o2.getAge();
        }
    }
}
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //比较两个学生：
        Student s1 = new Student(9,160.5,"alili");
        Student s2 = new Student(14,170.5,"bnana");
        //获取外部比较器：
        Comparator bj1 = new BiJiao03();
        System.out.println(bj1.compare(s1, s2));
    }
}
【5】外部比较器和内部比较器 谁好呀？
答案：外部比较器，多态，扩展性好
```

### 2.4.18 TreeSet实现类的使用

```java
【1】存入Integer类型数据：（底层利用的是内部比较器）
//特点：唯一，无序（没有按照输入顺序进行输出）， 有序（按照升序进行遍历）
public class Test01 {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //创建一个TreeSet:
        TreeSet<Integer> ts = new TreeSet<>();
        ts.add(12);
        ts.add(3);
        ts.add(7);
        ts.add(9);
        ts.add(3);
        ts.add(16);
        System.out.println(ts.size());
        System.out.println(ts);
    }
}
【2】TreeSet原理：底层：二叉树（数据结构中的一个逻辑结构）
在树中放入数据的时候，是依靠比较器来存放到特定位置的。
TreeSet底层的二叉树的遍历是按照升序的结果出现的，这个升序是靠中序遍历得到的：
【3】放入String类型数据：（底层实现类内部比较器）
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //创建一个TreeSet:
        TreeSet<String> ts = new TreeSet<>();
        ts.add("elili");
        ts.add("blili");
        ts.add("alili");
        ts.add("elili");
        ts.add("clili");
        ts.add("flili");
        ts.add("glili");
        System.out.println(ts.size());
        System.out.println(ts);
    }
}
【4】想放入自定义的Student类型的数据：
（1）利用内部比较器：
public class Student implements Comparable<Student> {
	//...
    @Override
    public int compareTo(Student o) {
    	return this.getAge()-o.getAge();
    }
}
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //创建一个TreeSet:
        TreeSet<Student> ts = new TreeSet<>();
        ts.add(new Student(10,"elili"));
        ts.add(new Student(8,"blili"));
        ts.add(new Student(4,"alili"));
        ts.add(new Student(9,"elili"));
        ts.add(new Student(10,"flili"));
        ts.add(new Student(1,"dlili"));
        System.out.println(ts.size());
        System.out.println(ts);
    }
}
（2）通过外部比较器：
public class Student  {
	//...
}
class BiJiao implements Comparator<Student>{
    @Override
    public int compare(Student o1, Student o2) {
        return o1.getName().compareTo(o2.getName());
    }
}
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //创建一个TreeSet:
        //利用外部比较器，必须自己制定：
        Comparator<Student> com = new BiJiao();
        TreeSet<Student> ts = new TreeSet<>(com);//一旦指定外部比较器，那么就会按照外部比较器来比较
        ts.add(new Student(10,"elili"));
        ts.add(new Student(8,"blili"));
        ts.add(new Student(4,"alili"));
        ts.add(new Student(9,"elili"));
        ts.add(new Student(10,"flili"));
        ts.add(new Student(1,"dlili"));
        System.out.println(ts.size());
        System.out.println(ts);
    }
}
实际开发中利用外部比较器多，因为扩展性好（多态）
换一种写法：
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        //创建一个TreeSet:
        //利用外部比较器，必须自己制定：
        /*Comparator<Student> com = new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                return o1.getName().compareTo(o2.getName());
            }
        };*/
        TreeSet<Student> ts = new TreeSet<>(new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                return o1.getName().compareTo(o2.getName());
            }
        });//一旦指定外部比较器，那么就会按照外部比较器来比较
        ts.add(new Student(10,"elili"));
        ts.add(new Student(8,"blili"));
        ts.add(new Student(4,"alili"));
        ts.add(new Student(9,"elili"));
        ts.add(new Student(10,"flili"));
        ts.add(new Student(1,"dlili"));
        System.out.println(ts.size());
        System.out.println(ts);
    }
}
```

### 2.4.19 Map接口常用方法

```java
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        /*
        增加：put(K key, V value)
        删除：clear() remove(Object key)
        修改：
        查看：entrySet() get(Object key) keySet() size() values()
        判断：containsKey(Object key) containsValue(Object value)
            equals(Object o) isEmpty()
         */
        //创建一个Map集合：无序，唯一
        Map<String,Integer> map = new HashMap<>();
        map.put("lili", 10101010);  //打印输出null
        map.put("nana",12345234);
        map.put("feifei",34563465);
        map.put("lili", 34565677);  //打印输出10101010
        map.put("mingming",12323);
        /*map.clear();清空*/
        /*map.remove("feifei");移除*/
        System.out.println("map大小 = " + map.size());
        System.out.println(map);
        System.out.println("map中是否包含key为lili? = " + map.containsKey("lili"));
        System.out.println("map中是否包含value为12323? = " + map.containsValue(12323));

        Map<String,Integer> map2 = new HashMap<>();
        map2.put("lili", 10101010);  //打印输出null
        map2.put("nana",12345234);
        map2.put("feifei",34563465);
        map2.put("lili", 34565677);  //打印输出10101010
        map2.put("mingming",12323);
        System.out.println(map==map2);  //输出false   判断地址
        System.out.println(map.equals(map2));//输出true equals进行了重写，比较的是集合中的值是否一致
        System.out.println("判断是否为空："+map.isEmpty());
        System.out.println(map.get("nana"));
        System.out.println("-----------------------------------");
        //keySet()对集合中的key进行遍历查看：
        Set<String> set = map.keySet();
        for(String s:set){
            System.out.println(s);
        }
        System.out.println("-----------------------------------");
        //values()对集合中的value进行遍历查看：
        Collection<Integer> values = map.values();
        for(Integer i:values){
            System.out.println(i);
        }
        System.out.println("-----------------------------------");
        //get(Object key) 结合 keySet()
        Set<String> set2 = map.keySet();
        for(String s:set2){
            System.out.println(map.get(s));
        }
        System.out.println("-----------------------------------");
        //entrySet()
        Set<Map.Entry<String, Integer>> entries = map.entrySet();
        for(Map.Entry<String, Integer> e:entries){
            System.out.println(e.getKey()+"----"+e.getValue());
        }
        System.out.println("-----------------------------------");
        //Iterator
        Iterator<Map.Entry<String, Integer>> it=map.entrySet().iterator();
        while(it.hasNext()){
             Map.Entry<String, Integer> entry=it.next();
             System.out.println("键key ："+entry.getKey()+" value ："+entry.getValue());
        }
    }
}
```

### 2.4.20  Hashtable、LinkedHashMap的使用

```java
public interface Map<K,V>
public class HashMap<K,V> extends AbstractMap<K,V> implements Map<K,V>, Cloneable, Serializable
public class Hashtable<K,V> extends Dictionary<K,V> implements Map<K,V>, Cloneable, java.io.Serializable
public class LinkedHashMap<K,V> extends HashMap<K,V> implements Map<K,V>

HashMap: 无序、唯一，按照key进行总结的，因为底层key遵照哈希表的结构(数组+链表)，哈希表原理：比如放入这个集合的数据对应的那个类：必须重写hashCode方法和equals方法
HashMap JDK1.2: 效率高，线程不安全，key可以存入null值，并且key的null值也遵循唯一的特点
Hashtable JDK1.0: 效率低，线程安全，key不可以存入null值
LinkedHashMap: 唯一，有序(按照输入顺序进行输出)
```

### 2.4.21 TreeMap 实现类

```java
特点：唯一，有序(按照升序或者降序)
原理：二叉树，key遵照二叉树的特点，放入集合的key的数据对应的类型内部一定要实现比较器(内部比较器,外部比较器)
【1】key的类型为String类型：
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        Map<String,Integer> map = new TreeMap<>();
        map.put("blili",1234);
        map.put("alili",2345);
        map.put("blili",5467);
        map.put("clili",5678);
        map.put("dlili",2345);
        System.out.println(map.size());
        System.out.println(map);
    }
}
【2】key的类型是一个自定义的引用数据类型：
（1）内部比较器：
public class Student implements Comparable<Student>{
    private int age;
    private String name;
    private double height;
    //get set toString等方法...
    @Override
    public int compareTo(Student o) {
       /* return this.getAge()-o.getAge();*/
        return this.getName().compareTo(o.getName());
    }
}
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        Map<Student,Integer> map = new TreeMap<>();
        map.put(new Student(19,"blili",170.5),1001);
        map.put(new Student(18,"blili",150.5),1003);
        map.put(new Student(19,"alili",180.5),1023);
        map.put(new Student(17,"clili",140.5),1671);
        map.put(new Student(10,"dlili",160.5),1891);
        System.out.println(map);
        System.out.println(map.size());
    }
}
（2）外部比较器：
public class Test {
    //这是main方法，程序的入口
    public static void main(String[] args) {
        Map<Student,Integer> map = new TreeMap<>(new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                return ((Double)(o1.getHeight())).compareTo((Double)(o2.getHeight()));
            }
        });
        map.put(new Student(19,"blili",170.5),1001);
        map.put(new Student(18,"blili",150.5),1003);
        map.put(new Student(19,"alili",180.5),1023);
        map.put(new Student(17,"clili",140.5),1671);
        map.put(new Student(10,"dlili",160.5),1891);
        System.out.println(map);
        System.out.println(map.size());
    }
}
```









### #

### #

### #

### #

### #

### #