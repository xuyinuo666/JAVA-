# 变量

<img src="image-20201225205205012.png" alt="image-20201225205205012" style="zoom:50%;" />

<img src="image-20201225205927572.png" alt="image-20201225205927572" style="zoom:50%;" />

## 浮点型





1. | double | 8字节 |
   | ------ | ----- |
   | float  | 4字节 |

   

## 字符型

1个字符=2个字节

- | 表示一个字符 | '静'     |
  | ------------ | -------- |
  | 表示转义字符 | '\n'     |
  | Unicode      | '\uXXXX' |

  

## 基本类型变量之间的转换

1. 容量小的数据类型转换为容量大的数据类型做运算时,会自动转换为容量大的数据类型

   byte .short.char-->int-->long -->float-->double

   ==**容量大小指的是数的范围大小,不是数字节的大小**,比如float大于long==

2. 字符型也可以进行运算:

   'A'+1=98

3. 特殊的,byte .short.char三种数据类型进行运算时,需要int接收.(包括相同类型的两个数据运算).

   整形常量默认为int , 浮点型常量默认为double

逻辑运算符
---

1. 取模结果的符号按照被模数的符号

2. ==自增不会改变数据本省数据类型==  += .-= .%=都不会改变 

   ```java
   short s = 10 ;
   s++ ;//类型还是short
   s = s+1;//会改变类型
   ```

逻辑运算符
---

<img src="image-20201226114656306.png" alt="image-20201226114656306" style="zoom:50%;" />

| &       | 两个添加必须同时满足才为true .条件可以同时参与运算           |
| ------- | ------------------------------------------------------------ |
| && 短路 | 两个添加必须同时满足才为true .当条件1不满足时,直接判断为false 符号后面的不参与运算 |

|| 与&&相反,只要有一个条件满足为true, 符号后面的不参与运算 .==推荐使用短路运算符==!!!!!!!!!!!!!!!

循环
---

| continue | 结束当次循环                          |
| -------- | ------------------------------------- |
| break    | 结束当前循环,(包裹此关键字最近的循环) |

两者后面不能有语句

数组
===

Array:多个相同类型的数据，按一定排序，有编号的集合.==本身是引用数据类型==，在内存中开辟了一块连续的空间。一旦确定长度不可改变

初始化
---

1. 静态初始化

   ```java
   int[] x;//声明
   x= new int[]{1,2,3,4}//初始化
   int [] x =new int[]{1,2,3,4} //声明+初始化。直接初始化数组
   ```

2. 动态初始化

   ```java
   int [] x=new int [4]//初始化一个长度为4的数组
   ```

   数组初始化只能存在长度或者内容

3. 二维数组：

   ```java
   //1.二维数组的声明和初始化
   		int[] arr = new int[]{1,2,3};//一维数组
   		//静态初始化
   		int[][] arr1 = new int[][]{{1,2,3},{4,5},{6,7,8}};
   		//动态初始化1
   		String[][] arr2 = new String[3][2];
   		//动态初始化2
   		String[][] arr3 = new String[3][];
   		//错误的情况 
   //		String[][] arr4 = new String[][4];
   //		String[4][3] arr5 = new String[][];
   //		int[][] arr6 = new int[4][3]{{1,2,3},{4,5},{6,7,8}};
   //3.获取数组的长度
   		System.out.println(arr4.length);//3
   		System.out.println(arr4[0].length);//3
   		System.out.println(arr4[1].length);//4
   		
   		//4.如何遍历二维数组
   		for(int i = 0;i < arr4.length;i++){
   			
   			for(int j = 0;j < arr4[i].length;j++){
   				System.out.print(arr4[i][j] + "  ");
   			}
   			System.out.println();
   		}
   ```

   

排序
---

1. 冒泡排序

   ```java
   public class bouble {
       public static void main(String[] args) {
       int [] x=new int[]{1,4,45,677,56,65,73,634,546,345,33,13,-1,-54,-33};
           for (int i = 0; i < x.length; i++) { //负责总体的排序，也就是需要进行几轮。
               //进行相邻的两个之间大小比较、交换。没有进行总体的排序。需要进行数组长度-1次。比较完一轮就少一个元素的比较，所以x.length-1-i
               for (int j = 0; j <x.length-1-i; j++) {
                   if (x[j]>x[j+1]){
                       int y=x[j];
                       x[j]=x[j+1];
                       x[j+1]=y;
                   }
               }
           }
           for (int i = 0; i < x.length; i++) {
               System.out.println(x[i]);
           }
       }
   
   }
   ```

   ## Arrays工具的使用



面向对象
===

封装
---

### 属性（成员变量）和局部变量

1. 成员变量可以不初始化而局部变量必须初始化

   现在假如你是java语言的开发者，你已经将对象保存在了堆内存中，而将局部变量保存在了栈内存中，你会怎么做呢？其实，不管是局部变量还是成员变量，都是必须要初始化的，那为什么成员变量会自动初始化？其实正是因为成员变量属于对象，而对象是保存在 堆中的，所以jvm就在初始化类的时候把成员变量初始化呢，而如果我们在调用方法的时候，还要jvm去将局部变量也进行初始化，是不是对会影响到性能呢？因此，直接强制局部变量必须要初始化反而更好

   ```java
   属性（成员变量）   vs  局部变量
    * 1.相同点：
    * 		1.1  定义变量的格式：数据类型  变量名 = 变量值
    * 		1.2 先声明，后使用
    * 		1.3 变量都有其对应的作用域 
    * 
    * 
    * 2.不同点：
    * 		2.1 在类中声明的位置的不同
    * 		属性：直接定义在类的一对{}内
    * 		局部变量：声明在方法内、方法形参、代码块内、构造器形参、构造器内部的变量
    * 		
    * 		2.2 关于权限修饰符的不同
    * 		属性：可以在声明属性时，指明其权限，使用权限修饰符。
    * 			常用的权限修饰符：private、public、缺省、protected  --->封装性
    * 			目前，大家声明属性时，都使用缺省就可以了。
    * 		局部变量：不可以使用权限修饰符。
    * 
    * 		2.3 默认初始化值的情况：
    * 		属性：类的属性，根据其类型，都有默认初始化值。
    * 			整型（byte、short、int、long）：0
    * 			浮点型（float、double）：0.0
    * 			字符型（char）：0  （或'\u0000'）
    * 			布尔型（boolean）：false
    * 
    * 			引用数据类型（类、数组、接口）：null
    * 
    * 		局部变量：没有默认初始化值。
    *  		意味着，我们在调用局部变量之前，一定要显式赋值。
    * 			特别地：形参在调用时，我们赋值即可。
    * 
    * 		2.4 在内存中加载的位置：
    * 		属性：加载到堆空间中   （非static）
    * 		局部变量：加载到栈空间
   ```

关于变量的赋值：
 * 如果变量是基本数据类型，此时赋值的是变量所保存的数据值。

 * 如果变量是引用数据类型，此时赋值的是变量所保存的数据的地址值。

   ```java
   //引用数据类型
   Order o1 = new Order();
   		o1.orderId = 1001;
   		
   		Order o2 = o1;//赋值以后，o1和o2的地址值相同，都指向了堆空间中同一个对象实体。
   		
   		System.out.println("o1.orderId = " + o1.orderId + ",o2.orderId = " +o2.orderId);
   		
   		o2.orderId = 1002;
   		
   		System.out.println("o1.orderId = " + o1.orderId + ",o2.orderId = " +o2.orderId);
   结果相同，操作的是同一个对象
   ```
```
   
   

值传递机制：

 * 如果参数是基本数据类型，此时实参赋给形参的是实参真实存储的数据值。

 * 如果参数是引用数据类型，此时实参赋给形参的是实参存储数据的地址值。

   ```java
   //基本数据类型
   public static void main(String[] args) {
           int x = 1;
           int y = 2;
           new bouble().fanzhuan(x,y);
           System.out.println("x的值"+x+"------y的值"+y);
       }
       void fanzhuan(int x, int y) {
           int u = x;
           x = y;
           y = u;
           System.out.println("fanzhuan："+"-----x的值"+x+"------y的值"+y);
       }
   fanzhuan：-----x的值2------y的值1
x的值1------y的值2
   
```


```java
//引用类型，操作的是同一个对象

    public static void main(String[] args) {
        data data = new data();
        data.m=1;
        data.n=2;
        System.out.println(data.m);
        System.out.println(data.n);
        bouble bouble = new bouble();
        bouble.YinyongSwap(data);
        System.out.println(data.m);
        System.out.println(data.n);
    }
    void YinyongSwap(data data) {
        int temp = data.m;
        data.m = data.n;
        data.n = temp;
    }

}
class data{
    int m;
    int n;
}
```

 

### 重载

在同一个类中，允许存在一个以上的同名方法，只要它们的参数个数或者参数类型不同即可。跟方法的权限修饰符、返回值类型、形参变量名、方法体都没有关系！

### this

我们在类的构造器中，可以显式的使用"this(形参列表)"方式，调用本类中指定的其他构造器

### super

特殊情况：当子类和父类中定义了同名的属性时，我们要想在子类中调用父类中声明的属性，则必须显式的

特殊情况：当子类重写了父类中的方法以后，我们想在子类的方法中调用父类中被重写的方法时，则必须显式的





继承
---

一旦子类A继承父类B以后，子类A中就获取了父类B中声明的所有的属性和方法。特别的，父类中声明为private的属性或方法，子类继承父类以后，==仍然认为获取了父类中私有的结构==。只有因为封装性的影响，==使得子类不能直接调用父类的结构而已==。（不能调用私有方法、属性） 

### 加载顺序

```
父类静态代变量、
父类静态代码块、
子类静态变量、
子类静态代码块、
父类非静态变量（父类实例成员变量）、
父类构造函数、
子类非静态变量（子类实例成员变量）、
子类构造函数。
```



### 重写

1. 重写以后，当创建子类对象以后，通过子类对象调用子父类中的同名同参数的方法时，实际执行的是子类重写父类的方法。
2. 子类重写的方法的方法名和形参列表与父类被重写的方法的方法名和形参列表相同
3. 子类重写的方法的权限修饰符不小于父类被重写的方法的权限修饰符
4. 子类不能重写父类中声明为private权限的方法
5. 返回值类型：
    *      	父类被重写的方法的返回值类型是void，则子类重写的方法的返回值类型只能是void
    *      	父类被重写的方法的返回值类型是A类型，则子类重写的方法的返回值类型可以是A类或A类的子类
    *      	父类被重写的方法的返回值类型是基本数据类型(比如：double)，则子类重写的方法的返回值类型必须是相同的基本数据类型(必须也是double)

```
 子类对象实例化的全过程
 * 
 * 1. 从结果上来看：（继承性）
 * 		子类继承父类以后，就获取了父类中声明的属性或方法。
 *      创建子类的对象，在堆空间中，就会加载所有父类中声明的属性。
 * 
 * 2. 从过程上来看：
 * 		当我们通过子类的构造器创建子类对象时，我们一定会直接或间接的调用其父类的构造器，进而调用父类的父类的构造器，...
 *    直到调用了java.lang.Object类中空参的构造器为止。正因为加载过所有的父类的结构，所以才可以看到内存中有
 *    父类中的结构，子类对象才可以考虑进行调用。
 *  
 * 明确：虽然创建子类对象时，调用了父类的构造器（进行初始化而已），但是自始至终就创建过一个对象，即为new的子类对象。
 * 
 */
```

多态
---

多态性的使用前提：  ① 类的继承关系  ② 方法的重写

有了对象的多态性以后，我们在编译期，只能调用父类中声明的方法，但在运行期，我们实际执行的是子类重写父类的方法，只适用于方法，不适用于属性（编译和运行都看左边）。总结：==编译，看左边；运行，看右边==。

包装类
---

基本数据类型、包装类、String三者之间的相互转换

1. String -->包装类类型   	 包装类.parseXXX()

   ```java
       String x="1";
       Integer xx=Integer.parseInt(x);
       System.out.println(xx);
       Double d=Double.parseDouble(x);
       System.out.println(d);
   ```

2. 包装类--->String类型        String.valueOf()

   ```java
       Integer x=1;
       String xx=String.valueOf(x);
       System.out.println(xx);
   ```

单例模式
---

```java
/*
 * 单例设计模式：
 * 1. 所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类只能存在一个对象实例。
 * 
 * 2. 如何实现？
 * 	 饿汉式  vs 懒汉式
 * 
 * 3. 区分饿汉式 和 懒汉式
 *   饿汉式：	
 *   	坏处：对象加载时间过长。
 *   	好处：饿汉式是线程安全的
 *   
 *   懒汉式：好处：延迟对象的创建。
 * 		  目前的写法坏处：线程不安全。--->到多线程内容时，再修改
 * 
 * 
 */
public class SingletonTest1 {
	public static void main(String[] args) {
//		Bank bank1 = new Bank();
//		Bank bank2 = new Bank();
		
		Bank bank1 = Bank.getInstance();
		Bank bank2 = Bank.getInstance();
		
		System.out.println(bank1 == bank2);
	}
}

//饿汉式
class Bank{
	
	//1.私有化类的构造器
	private Bank(){	
	}
	//2.内部创建类的对象
	//4.要求此对象也必须声明为静态的
	private static Bank instance = new Bank();
	
	//3.提供公共的静态的方法，返回类的对象
	public static Bank getInstance(){
		return instance;
	}
}
```

```java

/*
 * 单例模式的懒汉式实现
 * 
 */
public class SingletonTest2 {
	public static void main(String[] args) {
		
		Order order1 = Order.getInstance();
		Order order2 = Order.getInstance();
		
		System.out.println(order1 == order2);
		
	}
}


class Order{
	
	//1.私有化类的构造器
	private Order(){
		
	}
	
	//2.声明当前类对象，没有初始化
	//4.此对象也必须声明为static的
	private static Order instance = null;
	
	//3.声明public、static的返回当前类对象的方法
	public static Order getInstance(){
		
		if(instance == null){
			
			instance = new Order();
			
		}
		return instance;
	}
	
}
```

静态、非静态
---

| 静态                                                         | 非静态                                               |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| 伴随类的加载，加载时执行，执行一次                           | 伴随类的创建，每创建一个类执行一次                   |
| 可以调用静态的属性、静态的方法，或非静态的属性、非静态的方法 | 只能调用静态的属性、静态的方法，不能调用非静态的结构 |
| 对象的属性等进行初始化                                       | 初始化类的信息                                       |

静态代码块中不能出现this super 关键字

抽象类
---

abstract修饰类：抽象类
```
abstract修饰类：抽象类
 * 		> 此类不能实例化
 *      > 抽象类中一定有构造器，便于子类实例化时调用（涉及：子类对象实例化的全过程）
 *      > 开发中，都会提供抽象类的子类，让子类对象实例化，完成相关的操作
```

```
abstract修饰方法：抽象方法
 *      > 若子类重写了父类中的所有的抽象方法后，此子类方可实例化
 *        若子类没有重写父类中的所有的抽象方法，则此子类也是一个抽象类，需要使用abstract修饰
```

### 模板方法设计模式

```java
class A{
    void walk(){
        System.out.println("A's walk()");
    }
    // 模板方法，把基本操作组合到一起，子类一般不能重写
    public final void process() {
        this.walk();// 像个钩子，具体执行时，挂哪个子类，就执行哪个子类的实现代码
    }
}
class B extends A{
    void walk(){
        System.out.println("B's walk()");
    }
}
class C extends A{
    void walk(){
        System.out.println("C's walk()");
    }
}
```

接口
---

```
Java开发中，接口通过让类去实现(implements)的方式来使用.
 *    如果实现类覆盖了接口中的所有抽象方法，则此实现类就可以实例化
 *    如果实现类没有覆盖接口中所有的抽象方法，则此实现类仍为一个抽象类
```

```
相同点：
1.都不能被实例化
2.接口的实现类或者抽象的子类都必须实现类接口或者继承了抽象才可以被实例化
不同点：
1.接口只有定义，方法不能再接口中实现，实现接口的类要实现接口中的所有方法；抽象类可以有定义与实现方法可以在抽象类中实现
2.接口要实现，抽象要继承，一个类可以实现多个接口，但只能继承一个抽象类
3.接口强调设计理念“has-a”的关系，抽象类强调“is-a”关系
4.接口中定义变量默认为public、static、final且要设定初始值方法必须是publicstatic只能是这两个抽象类可以有自己的成员变量也可以有非抽象的成员方法，成员默认值为：default
5.接口被运用于比较常用的功能，抽象更倾向于充当公共类的角色
6.接口是定义规范的，抽象是对公共部分的抽取
```

```
		//知识点1：接口中定义的静态方法，只能通过接口来调用。
		//知识点2：通过实现类的对象，可以调用接口中的默认方法。
		//如果实现类重写了接口中的默认方法，调用时，仍然调用的是重写以后的方法
		//知识点3：如果子类(或实现类)继承的父类和实现的接口中声明了同名同参数的默认方法，那么子类在没有重写此方法的情况下，默认调用的是父类中的同名同参数的方法。-->类优先原则
		//知识点4：如果实现类实现了多个接口，而这多个接口中定义了同名同参数的默认方法，那么在实现类没有重写此方法的情况下，报错。-->接口冲突。这就需要我们必须在实现类中重写此方法
```

```
//知识点5：如何在子类(或实现类)的方法中调用父类、接口中被重写的方法
	public void myMethod(){
		method3();//调用自己定义的重写的方法
		super.method3();//调用的是父类中声明的
		//调用接口中的默认方法
		CompareA.super.method3();、、CompareA中的method3();
		CompareB.super.method3();
```

# Integer

- 1.关于int和Integer的问题区别分析
- 2.Integer的值缓存的原理
  - 2.1 Java 5 中引入缓存特性
  - 2.2 Integer类中的IntegerCache类
  - 2.3 其他整型类型的缓存机制
- 3.理解自动装箱和拆箱
  - 3.1 什么是装箱？什么是拆箱？
  - 3.2 装箱和拆箱是如何实现的
  - 3.3 装箱和拆箱在编程实际中注意点
- 4.原始类型线程安全问题
  - 4.1 那些类型是线程安全的
  - 4.2 如何验证int类型是否线程安全
  - 4.3 AtomicInteger线程安全版



### 1.关于int和Integer的问题区别分析

- 1.1 编译阶段、运行时，自动装箱 / 自动拆箱是发生在什么阶段？
- 1.2使用静态工厂方法 valueOf 会使用到缓存机制，那么自动装箱的时候，缓存机制起作用吗？
- 1.3为什么我们需要原始数据类型，Java 的对象似乎也很高效，应用中具体会产生哪些差异？
- 1.4 阅读过 Integer 源码吗？分析下类或某些方法的设计要点？
- 1.5 int和Integer的区别

```
1、Integer是int的包装类，int则是java的一种基本数据类型 
2、Integer变量必须实例化后才能使用，而int变量不需要 
3、Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值 
4、Integer的默认值是null，int的默认值是0

延伸： 
关于Integer和int的比较 
1、由于Integer变量实际上是对一个Integer对象的引用，所以两个通过new生成的Integer变量永远是不相等的（因为new生成的是两个对象，其内存地址不同）。

Integer i = new Integer(100);
Integer j = new Integer(100);
System.out.print(i == j); //false

2、Integer变量和int变量比较时，只要两个变量的值是向等的，则结果为true（因为包装类Integer和基本数据类型int比较时，java会自动拆包装为int，然后进行比较，实际上就变为两个int变量的比较）

Integer i = new Integer(100);
int j = 100；
System.out.print(i == j); //true

3、非new生成的Integer变量和new Integer()生成的变量比较时，结果为false。（因为非new生成的Integer变量指向的是java常量池中的对象，而new Integer()生成的变量指向堆中新建的对象，两者在内存中的地址不同）

Integer i = new Integer(100);
Integer j = 100;
System.out.print(i == j); //false

4、对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则比较结果为false

Integer i = 100;
Integer j = 100;
System.out.print(i == j); //true

Integer i = 128;
Integer j = 128;
System.out.print(i == j); //false

对于第4条的原因： 
java在编译Integer i = 100 ;时，会翻译成为Integer i = Integer.valueOf(100)；，而java API中对Integer类型的valueOf的定义如下：

public static Integer valueOf(int i){
    assert IntegerCache.high >= 127;
    if (i >= IntegerCache.low && i <= IntegerCache.high){
        return IntegerCache.cache[i + (-IntegerCache.low)];
    }
    return new Integer(i);
}

java对于-128到127之间的数，会进行缓存，Integer i = 127时，会将127进行缓存，下次再写Integer j = 127时，就会直接从缓存中取，就不会new了

```


### 2.Integer的值缓存的原理

#### 2.1 Java 5 中引入缓存特性

- 在 Java 5 中，为 Integer 的操作引入了一个新的特性，用来节省内存和提高性能。整型对象在内部实现中通过使用相同的对象引用实现了缓存和重用。
- 这种 Integer 缓存策略仅在自动装箱（autoboxing）的时候有用，使用构造器创建的 Integer 对象不能被缓存。



#### 2.2 Integer类中的IntegerCache类

- 在创建新的 Integer 对象之前会先在 IntegerCache.cache (是个Integer类型的数组)中查找。有一个专门的 Java 类来负责 Integer 的缓存。
- 这个类是用来实现缓存支持，并支持 -128 到 127 之间的自动装箱过程。最大值 127 可以通过 JVM 的启动参数 -XX:AutoBoxCacheMax=size 修改。 缓存通过一个 for 循环实现。从小到大的创建尽可能多的整数并存储在一个名为 cache 的整数数组中。这个缓存会在 Integer 类第一次被使用的时候被初始化出来。以后，就可以使用缓存中包含的实例对象，而不是创建一个新的实例(在自动装箱的情况下)。[博客](https://github.com/yangchong211/YCBlogs)

```
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}


private static class IntegerCache {
    static final int low = -128;
    static final int high;
    static final Integer cache[];

    static {
        // high value may be configured by property
        int h = 127;
        String integerCacheHighPropValue =
            sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
        if (integerCacheHighPropValue != null) {
            try {
                int i = parseInt(integerCacheHighPropValue);
                i = Math.max(i, 127);
                // Maximum array size is Integer.MAX_VALUE
                h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
            } catch( NumberFormatException nfe) {
                // If the property cannot be parsed into an int, ignore it.
            }
        }
        high = h;

        cache = new Integer[(high - low) + 1];
        int j = low;
        for(int k = 0; k < cache.length; k++)
            cache[k] = new Integer(j++);

        // range [-128, 127] must be interned (JLS7 5.1.7)
        assert IntegerCache.high >= 127;
    }

    private IntegerCache() {}
}
```

#### 2.3 其他整型类型的缓存机制

- 这种缓存行为不仅适用于Integer对象。我们针对所有整数类型的类都有类似的缓存机制。
  - 有 ByteCache 用于缓存 Byte 对象
  - 有 ShortCache 用于缓存 Short 对象
  - 有 LongCache 用于缓存 Long 对象
  - 有 CharacterCache 用于缓存 Character 对象
  - Byte，Short，Long 有固定范围: -128 到 127。对于 Character, 范围是 0 到 127。除了 Integer 可以通过参数改变范围外，其它的都不行。



### 3.理解自动装箱和拆箱

#### 3.1 什么是装箱？什么是拆箱？

- 装箱就是  自动将基本数据类型转换为包装器类型；拆箱就是  自动将包装器类型转换为基本数据类型。

```
//拆箱
int yc = 5;
//装箱
Integer yc = 5;
```


#### 3.2 装箱和拆箱是如何实现的

- 以Interger类为例，下面看一段代码来了解装箱和拆箱的实现

```
public class Main {
    public static void main(String[] args) {
        Integer y = 10;
        int c = i;
    }
}
```

- 然后来编译一下，看下图所示：
  - 从反编译得到的字节码内容可以看出，在装箱的时候自动调用的是Integer的valueOf(int)方法。而在拆箱的时候自动调用的是Integer的intValue方法。
  - 因此可以用一句话总结装箱和拆箱的实现过程：装箱过程是通过调用包装器的valueOf方法实现的，而拆箱过程是通过调用包装器的 xxxValue方法实现的。（xxx代表对应的基本数据类型）。
    ![image](https://upload-images.jianshu.io/upload_images/4432347-9a3efbd0f681629e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#### 3.3 装箱和拆箱在编程实际中注意点

- 建议避免无意中的装箱、拆箱行为，尤其是在性能敏感的场合，创建 10 万个 Java 对象和 10 万个整数的开销可不是一个数量级的，不管是内存使用还是处理速度，光是对象头的空间占用就已经是数量级的差距了。


### 4.原始类型线程安全问题

#### 4.1 那些类型是线程安全的

- Java自带的线程安全的基本类型包括： AtomicInteger, AtomicLong, AtomicBoolean, AtomicIntegerArray,AtomicLongArray等

#### 4.2 如何验证int类型是否线程安全

- 200个线程，每个线程对共享变量 count 进行 50 次 ++ 操作 
- int 作为基本类型，直接存储在内存栈，且对其进行+,-操作以及++,–操作都不是原子操作，都有可能被其他线程抢断，所以不是线程安全。int 用于单线程变量存取，开销小，速度快

```
int count = 0;
private void startThread() {
    for (int i = 0;i < 200; i++){
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int k = 0; k < 50; k++){
                    count++;
                }
            }
        }).start();
    }
    // 休眠10秒，以确保线程都已启动
    try {
        Thread.sleep(1000*10);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }finally {
        Log.e("打印日志----",count+"");
    }
}

//期望输出10000，最后输出的是9818
//注意：打印日志----: 9818
```


#### 4.3 AtomicInteger线程安全版

- AtomicInteger类中有有一个变量valueOffset，用来描述AtomicInteger类中value的内存位置 。
- 当需要变量的值改变的时候，先通过get（）得到valueOffset位置的值，也即当前value的值.给该值进行增加，并赋给next
- compareAndSet（）比较之前取到的value的值当前有没有改变，若没有改变的话，就将next的值赋给value，倘若和之前的值相比的话发生变化的话，则重新一次循环，直到存取成功，通过这样的方式能够保证该变量是线程安全的
- value使用了volatile关键字，使得多个线程可以共享变量，使用volatile将使得VM优化失去作用，在线程数特别大时，效率会较低。[博客](https://github.com/yangchong211/YCBlogs)


```
private static AtomicInteger atomicInteger = new AtomicInteger(1);
static Integer count1 = Integer.valueOf(0);
private void startThread1() {
    for (int i = 0;i < 200; i++){
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int k = 0; k < 50; k++){
                    // getAndIncrement: 先获得值，再自增1，返回值为自增前的值
                    count1 = atomicInteger.getAndIncrement();
                }
            }
        }).start();
    }
    // 休眠10秒，以确保线程都已启动
    try {
        Thread.sleep(1000*10);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }finally {
        Log.e("打印日志----",count1+"");
    }
}

//期望输出10000，最后输出的是10000
//注意：打印日志----: 10000



//AtomicInteger使用了volatile关键字进行修饰，使得该类可以满足线程安全。
private volatile int value;
/**
 * Creates a new AtomicInteger with the given initial value.
 *
 * @param initialValue the initial value
 */
public AtomicInteger(int initialValue) {
    value = initialValue;
}
```


### 5.Java 原始数据类型和引用类型局限性

#### 5.1 原始数据类型和 Java 泛型并不能配合使用

- Java 的泛型某种程度上可以算作伪泛型，它完全是一种编译期的技巧，Java 编译期会自动将类型转换为对应的特定类型，这就决定了使用泛型，必须保证相应类型可以转换为Object。


#### 5.2 无法高效地表达数据，也不便于表达复杂的数据结构

- Java 的对象都是引用类型，如果是一个原始数据类型数组，它在内存里是一段连续的内存，而对象数组则不然，数据存储的是引用，对象往往是分散地存储在堆的不同位置。这种设计虽然带来了极大灵活性，但是也导致了数据操作的低效，尤其是无法充分利用现代 CPU 缓存机制。
- Java 为对象内建了各种多态、线程安全等方面的支持，但这不是所有场合的需求，尤其是数据处理重要性日益提高，更加高密度的值类型是非常现实的需求。



字符串
===

String
---

| 方法                                             | 用法                                 |
| ------------------------------------------------ | ------------------------------------ |
| `boolean` `endsWith(String suffix)`              | 判断字符串是否以suffix结尾的         |
| `boolean` `startsWith(String prefix)`            | 判断字符串是否以prefix开头           |
| `boolean startsWith(String prefix, int toffset)` | 判断字符串是否在toffset以prefix开头  |
| `int indexOf(String str)`                        | 第一次出现str的位置                  |
| `int indexOf(String str, int fromIndex)`         | 从fromIndex开始第一次出现str的位置   |
| `int lastIndexOf(String str)`                    | 最后一次出现位置                     |
| `int lastIndexOf(String str, int fromIndex)`     | 从fromIndex开始最后一次出现str的位置 |
| `String concat(String str)`                      | 将str添加到字符串                    |
| `int compareTo(String anotherString)`            | 比较两个字符串的大小                 |
| `String substring(int beginIndex, int endIndex)` | 截取字符串                           |



```
String 与 byte[]之间的转换
    编码：String --> byte[]:调用String的getBytes()
    解码：byte[] --> String:调用String的构造器
String 与 char[]之间的转换
    String --> char[]:调用String的toCharArray()
    char[] --> String:调用String的构造器
```





StringBuffer
---

| 方法                                                      | 用法                                         |
| --------------------------------------------------------- | -------------------------------------------- |
| `append`                                                  | 追加                                         |
| `int capacity()`                                          | 返回当前容量                                 |
| `char`   `charAt(int index)`                              | 返回index的字符                              |
| `StringBuffer` `delete(int start,  int end)`              | 删除start-end字符                            |
| `StringBuffer` `deleteCharAt(int index)`                  | 删除指定位置的字符                           |
| `StringBuffer insert(int offset, xxx)`                    | 在指定位置插入xxx                            |
| `StringBuffer` `replace(int start,  int end, String str)` | 替换指定的 `String`字符这个序列的特征。      |
| `StringBuffer` `reverse()`                                | 将字符串倒序排列                             |
| `void` `setCharAt(int index,  char ch)`                   | 将index处设置为ch                            |
| `String` `substring(int start,  int end)`                 | 从start开始到end索引结束左闭右开区间的字符串 |

```
String、StringBuffer、StringBuilder三者的异同？
    String:不可变的字符序列；底层使用char[]存储
    StringBuffer:可变的字符序列；线程安全的，效率低；底层使用char[]存储
    StringBuilder:可变的字符序列；jdk5.0新增的，线程不安全的，效率高；底层使用char[]存储
扩容问题:如果要添加的数据底层数组盛不下了，那就需要扩容底层的数组。
             默认情况下，扩容为原来容量的2倍 + 2，同时将原有数组中的元素复制到新的数组中。
```

Comparator和Comparable
---

```java
Collections.sort(list,new Comparator<Integer>(){
			@Override
			public int compare(Integer o1, Integer o2) {
				return o2 - o1;
			}
		});
		//具有临时性
```

```java
public int compareTo(Person o) {
		//引用类型（可以排序的类型）可以直接调用CompareTo方法
		//基本类型--使用   减  
		//return this.age - o.age;//用this对象 - 参数中的对象，是按照该属性的升序进行的排列
		//return o.age - this.age;
		
		//return this.name.compareTo(o.name);
		//return o.name.compareTo(this.name);
		
		return this.age.compareTo(o.age);
	}


```

```java
   @Override
    public int compareTo(Object o) {
        if (o instanceof goods) {
            goods goods = (goods) o;
            if (this.price > goods.price) {
                return -1;
            } else if (this.price < goods.price) {
                return 1;
            } else if (this.price == goods.price) {
               return this.name.compareTo(goods.name);
            }
        }
            throw new RuntimeException("错误");

    }
```



Enum
===

|     方法名称	|描述|
| :--: | :--: |
|     values()	|以数组形式返回枚举类型的所有成员|
|     valueOf()|	将普通字符串转换为枚举实例|
|     compareTo()|	比较两个枚举成员在定义时的顺序|
|     ordinal()	|获取枚举成员的索引位置|

1. ```java
   public static void main(String[] args) {
           color[] values = color.values();
           for (int i = 0; i < values.length; i++) {
               System.out.println(values[i]);
           }
       }
   ```

2. ```
    public static void main(String[] args) {
           color sss = color.valueOf("red");
           System.out.println(sss.getClass());
   ```

集合
===



集合有单列，双列

单列：List、Set

双列：Map

List
---

> 存储有序的、可重复的数据。

初始值数组大小为10 。ArrayList扩容1.5倍，Vector 扩容2倍

### ArrayList

> 线程不安全的，效率高；底层使用Object[] elementData存储

```java
调用ArrayList无参构造时
public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA; //默认为零，并不是10，只创建了Object数组
    }

```

添加元素时，会先判断是否满了，满了进行扩容，扩容为原来的1.5倍，同时需要将原有数组中的数据复制到新的数组中。

```java

     	// 如果直接传入初始化大小，就直接创建了。当扩容时 1.5倍 
 *      ArrayList list = new ArrayList();//底层Object[] elementData初始化为{}.并没有创建长度为10的数组
 *
 *      list.add(123);//第一次调用add()时，底层才创建了长度10的数组，并将数据123添加到elementData[0]
 *      ...
 *      后续的添加和扩容操作与jdk 7 无异。
```

### Vector

与ArrayList相同，扩容机制是2倍

调用无参构造时，默认传入了10，创建Object [10]

### LinkedList

```java
LinkedList的源码分析：
 *      LinkedList list = new LinkedList(); 内部声明了Node类型的first和last属性，默认值为null
 *      list.add(123);//将123封装到Node中，创建了Node对象。
 *
 *      其中，Node定义为：体现了LinkedList的双向链表的说法
 *      private static class Node<E> {
             E item;
             Node<E> next;
             Node<E> prev;

             Node(Node<E> prev, E element, Node<E> next) {
             this.item = element;
             this.next = next;
             this.prev = prev;
             }
         }
```

```java
List的有序性一是指值插入的顺序性，即如果使用add添加到list末尾，那么遍历的顺序是和插入的顺序一致的；如果采用随机插入，那么插入的位置也是已经确定的，就是人为的确定了它的位置。所以说List是有序的。

List的有序性二是指其内部的元素可以按照某种规则进行排序，所以说List是有序的。

Map的无序性一是指Map的插入顺序和遍历顺序是不一致的，无法人为的确定插入位置，必须通过hash值来得到其存放位置，是固定的。所以说Map是无序的。

Map的无序性二是指Map中的元素无法按照某种规则进行排序，因为它的位置只与hash值和其内部数组大小有关，其位置无法进行人为改变。所以说Map是无序的。
```

==区别==

|          | ArrayList    | LinkedList    |
| -------- | ------------ | ------------- |
| 底层     | Object数组   | 双向链表      |
| 是否安全 | 否           | 否            |
| 增删速率 | 增删慢查询快 | 增删快,查询慢 |

> 将List变为线程安全

### Collection对List进行封装

```java
LinkedList<Integer>    linkedList    = new LinkedList<Integer>();
//调用Collections的synchronizedList方法，传入一个linkedList，会返回一个SynchronizedList实例对象
List<Integer> synchronizedList =  Collections.synchronizedList(linkedList);

//调用Collections的synchronizedList方法，ArrayList，返回一个SynchronizedRandomAccessList实例对象
ArrayList<Integer>    arrayList    = new ArrayList<Integer>();
List<Integer> synchronizedRandomAccessList =  Collections.synchronizedList(arrayList);
```

### CopyOnWriteArrayList

1. 读写分离 : 读数据仍从旧数组中读取，而新数据在新增或删除完成之后直接替换旧数组。
2. 加锁 : ReentrantLock 
3. volatile : 保证一个线程操作变量后直接刷回物理内存,让其他线程的缓存失效 重新读取数据  .

==区别==

使用Synchro 进行封装 加==读写锁==, Copy只加==写锁==



Set
---

> 存储无序的、不可重复的数据
>
> 1. 无序性：无序性不等于随机性，存储的数据在底层数组中并非按照数组索引的顺序添加，而是数据的hashcode值来决定的
> 2. 不可重复：保证添加的元素，按照equals（）判断时，不能返回true,即相同的元素只能添加一个

==set和map 初始值 16 。默认加载因子0.75，达到容量的0.75时，扩容2倍==

### HashSet

```
添加元素的过程：以HashSet为例：
        我们向HashSet中添加元素a,首先调用元素a所在类的hashCode()方法，（相同类Hash值相同）计算元素a的哈希值， 此哈希值接着通过某种算法计算出在HashSet底层数组中的存放位置（即为：索引位置），判断数组此位置上是否已经有元素：
            如果此位置上没有其他元素，则元素a添加成功。 --->情况1
            如果此位置上有其他元素b(或以链表形式存在的多个元素），则比较元素a与元素b的hash值：
                如果hash值不相同，则元素a添加成功。--->情况2
                如果hash值相同，进而需要调用元素a所在类的equals()方法：
                       equals()返回true,元素a添加失败
                       equals()返回false,则元素a添加成功。--->情况2

        对于添加成功的情况2和情况3而言：元素a 与已经存在指定索引位置上数据以链表的方式存储。
       当类重写了equals()和hashCode(),比如String，添加到set中时，得到的hash值相等，调用equals时也相等，就认为是同一个对象。

```

```
set底层实现的就是Map，当添加元素时，使用map的put方法，将set值放入map的key，使用静态对象 present 来占位，没有什么意义
```



### LinkedHashSet

```
LinkedHashSet作为hashset的子类，在添加数据的同时，每个数据还维护了两个引用，记录次数据前一个数据和后一个数据。（这样使得使用linkedhashset时，造成添加的先后顺序，和打印的先后顺序一致，但其实存放的数据还是无序的，只是通过链表维护起来了，方便遍历）
```

### TreeSet

> 和hashset比较方法不同，hashset用equals比较，而TreeSet用的是compareTo比较

Map
---

==加载因子为0.75 扩容2倍==

```
一、Map的实现类的结构：
 *  |----Map:双列数据，存储key-value对的数据   ---类似于高中的函数：y = f(x)
 *         |----HashMap:作为Map的主要实现类；线程不安全的，效率高；存储null的key和value
 *              |----LinkedHashMap:保证在遍历map元素时，可以按照添加的顺序实现遍历。
 *                      原因：在原有的HashMap底层结构基础上，添加了一对指针，指向前一个和后一个元素。
 *                      对于频繁的遍历操作，此类执行效率高于HashMap。
 *         |----TreeMap:保证按照添加的key-value对进行排序，实现排序遍历。此时考虑key的自然排序或定制排序
 *                      底层使用红黑树
 *         |----Hashtable:作为古老的实现类；线程安全的，效率低；不能存储null的key和value
 *              |----Properties:常用来处理配置文件。key和value都是String类型
 *
 *
 *      HashMap的底层：数组+链表  （jdk7及之前）
 *                    数组+链表+红黑树 （jdk 8）
 *

```

```java
HashMap： JDK1.8 之前 HashMap 由数组+链表组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的（“拉链法”解决冲突）。JDK1.8 以后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8），将链表转化为红黑树，以减少搜索时间
```



```
map的key value存储特点：
 Map中的key:无序的、不可重复的，使用Set存储所有的key  ---> key所在的类要重写equals()和hashCode() （以HashMap为例）
 *    Map中的value:无序的、可重复的，使用Collection存储所有的value --->value所在的类要重写equals()
 *    一个键值对：key-value构成了一个Entry对象。
 *    Map中的entry:无序的、不可重复的，使用Set存储所有的entry
```

```
 *
 *  面试题：
 *  1. HashMap的底层实现原理？
HashMap map = new HashMap():
 *      在实例化以后，底层创建了长度是16的一维数组Entry[] table。
 *      ...可能已经执行过多次put...
 *      map.put(key1,value1):
 *      首先，调用key1所在类的hashCode()计算key1哈希值，此哈希值经过某种算法计算以后，得到在Entry数组中的存放位置。
 *      如果此位置上的数据为空，此时的key1-value1添加成功。 ----情况1
 *      如果此位置上的数据不为空，(意味着此位置上存在一个或多个数据(以链表形式存在)),比较key1和已经存在的一个或多个数据
 *      的哈希值：
 *              如果key1的哈希值与已经存在的数据的哈希值都不相同，此时key1-value1添加成功。----情况2
 *              如果key1的哈希值和已经存在的某一个数据(key2-value2)的哈希值相同，继续比较：调用key1所在类的equals(key2)方法，比较：
 *                      如果equals()返回false:此时key1-value1添加成功。----情况3
 *                      如果equals()返回true:使用value1替换value2。
 *
 *       补充：关于情况2和情况3：此时key1-value1和原来的数据以链表的方式存储。
 *
 *      在不断的添加过程中，会涉及到扩容问题，当超出临界值(且要存放的位置非空)时，扩容。默认的扩容方式：扩容为原来容量的2倍，并将原有的数据复制过来。
 *
 *      jdk8 相较于jdk7在底层实现方面的不同：
 *      1. new HashMap():底层没有创建一个长度为16的数组
 *      2. jdk 8底层的数组是：Node[],而非Entry[]
 *      3. 首次调用put()方法时，底层创建长度为16的数组
 *      4. jdk7底层结构只有：数组+链表。jdk8中底层结构：数组+链表+红黑树。
 *         4.1 形成链表时，七上八下（jdk7:新的元素指向旧的元素。jdk8：旧的元素指向新的元素）
           4.2 当数组的某一个索引位置上的元素以链表形式存在的数据个数 > 8 且当前数组的长度 > 64时，此时此索引位置上的所数据改为使用红黑树存储。
 *
 *      DEFAULT_INITIAL_CAPACITY : HashMap的默认容量，16
 *      DEFAULT_LOAD_FACTOR：HashMap的默认加载因子：0.75
 *      threshold：扩容的临界值，=容量*填充因子：16 * 0.75 => 12
 *      TREEIFY_THRESHOLD：Bucket中链表长度大于该默认值，转化为红黑树:8  转换为链表时:6
 *      MIN_TREEIFY_CAPACITY：桶中的Node被树化时最小的hash表容量:64 在桶中容量大于8 且 总数量>64 时,这个桶才会进行转换为树,否则只进行扩容.
```



```
 *  2. HashMap 和 Hashtable的异同？
    HashMap 线程不安全的，效率高；存储null的key和value
    Hashtable 线程安全的，效率低；不能存储null的key和value
 *  3. CurrentHashMap 与 Hashtable的异同？
    ConcurrentHashMap采用锁分段的技术,它对数据集进行分段,每段竞争一把锁,不同数据段的数据不存在锁竞争,从而有效提高了并发访问效率;可以理解为把一个大的Map拆分为N个小的HashTable,在put或者get的时候,根据key.hashCode()来决定把key放在哪一个HashTable中,在源码中一个小的HashTable就是一个Segment

总的来说,ConcurrentHashMap就是一个线程安全的HashMap,而且还保证一定的并发访问效率
```

Collections工具类
---

> Collections 类中提供了多个 synchronizedXxx() 方法，
>         该方法可使将指定集合包装成线程同步的集合，从而可以解决
>         多线程并发访问集合时的线程安全问题 ==如下的多线程章节==

```
reverse(List)：反转 List 中元素的顺序
shuffle(List)：对 List 集合元素进行随机排序
sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序
sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换

Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素
Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
Object min(Collection)
Object min(Collection，Comparator)
int frequency(Collection，Object)：返回指定集合中指定元素的出现次数
void copy(List dest,List src)：将src中的内容复制到dest中
boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换 List 对象的所有旧值
```







![image-20210518143202723](E:\文档\JAVA笔记\Typora\image-20210518143202723.png)

### 为什么ConcurrentHashMap，HashTable不支持key，value为null？

因为HashMap是非线程安全的，默认单线程环境中使用，如果get(key)为null，可以通过containsKey(key)
方法来判断这个key的value为null，还是不存在这个key，而ConcurrentHashMap，HashTable是线程安全的，
在多线程操作时，因为get(key)和containsKey(key)两个操作和在一起不是一个原子性操作，可能在containsKey(key)时发现存在这个键值对，但是get(key)时，有其他线程删除了键值对，导致get(key)返回的Node是null，然后执行方法时抛出异常。所以无法区分value为null还是不存在key。

> ConcurrentHashMap原理

在添加元素时,将Key进行Hash操作,得到应放的位置,如果没有元素就进行CAS操作放入,如果有元素,就用synchronized锁将链表头锁定,在进行插入操作.

ConcurrentHashMap在解决扩容时其他线程访问的问题，是通过设置**ForwardingNode标识节点**来解决的，扩容时，某个线程对数组中某个下标下所有Hash冲突的元素进行迁移时，那么会将数组下标的数组元素设置为一个**标识节点ForwardingNode**，之后其他线程在访问时，如果发现key的hash值映射的数组下标对应是一个**标识节点ForwardingNode**，那么会根据ForwardingNode中的nextTable变量，去新的tab中查找元素。（如果是添加新的键值对时发现是ForwardingNode，当前线程会进行辅助扩容或阻塞等待，扩容完成后去新数组中更新或插入元素）





I/O
===

## 字符流

```java
        ----------------------------------------缓冲字符流
        File file1 = new File("F://xugaowei.txt");
        File file2 = new File("F://IO_T//BufferRead2.txt");
        BufferedReader br = new BufferedReader(new FileReader(file1));
        BufferedWriter bw = new BufferedWriter(new FileWriter(file2));
        char[] chars = new char[1024 * 10];
        try {
            while (br.read(chars) != -1) {
                bw.write(chars);
            }
        } finally {
            if (br != null) {
                br.close();
            }
            if (bw != null) {
                bw.close();
            }
        }
        --------------------------------------普通字符流
        File file1 = new File("F://xugaowei.txt");
        File file2 = new File("F://IO_T//BufferRead.txt");
        FileReader fileReader = new FileReader(file1);
        FileWriter fileWriter = new FileWriter(file2,true);
        int len;
        char[] chars = new char[1024];
        try {
            while ((len = (fileReader.read(chars))) != -1) {
                fileWriter.write(chars);
            }
        } finally {
            if (fileReader != null) {
                fileReader.close();
            }
            if (fileWriter != null) {
                fileWriter.close();
            }
        }
```



## 字节流

```java
 ---------------------------------------------缓冲字节流

        File file1 = new File("F://xugaowei.txt");
        File file2 = new File("F://IO_T//Buffer.txt");
        if (!file2.exists()){
            file2.createNewFile();
        }
        BufferedInputStream br = new BufferedInputStream(new FileInputStream(file1));
        BufferedOutputStream bw = new BufferedOutputStream(new FileOutputStream(file2));
        int len;
        byte[] bytes = new byte[1024];
        try {
            while ((len = br.read(bytes)) != -1) {
                bw.write(bytes);
            }
        } finally {
            if (br != null) {
                br.close();
            }
            if (bw != null) {
                bw.close();
            }

        }
        ---------------------------------------------普通字节流
        File file1 = new File("F://xugaowei.txt");
        File file2 = new File("F://xugaowei//xugaoweiCp.txt");
        FileInputStream fi = new FileInputStream(file1);
        FileOutputStream fo = new FileOutputStream(file2);
        byte[] bytes=new byte[1024];
        int len;
        while ((len=(fi.read(bytes)))!=-1){
//            String s = new String(bytes, 0, len);
            fo.write(bytes);
        }
        fi.close();
        fo.close();
```



## 转换流

```java
------------------------------------------将字符流转为字节流（缓冲）
        File file1 = new File("F://xugaowei.txt");
        File file2 = new File("F://IO_T//BufferRead8.txt");
        InputStreamReader in = new InputStreamReader(new FileInputStream(file1));
        OutputStreamWriter out = new OutputStreamWriter(new FileOutputStream(file2));
        BufferedReader br = new BufferedReader(in);
        BufferedWriter bw = new BufferedWriter(out);
        char[] chars = new char[1024];
        while (br.read(chars) != -1) {
            bw.write(chars);
            bw.flush();
        }

```





## RandomAccessFile

```java
package IO;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.RandomAccessFile;

public class RandomAccessFiletest {
    public static void main(String[] args) throws IOException {
        RandomAccessFile r1 = null;
        RandomAccessFile r2 = null;
        File file = new File("src\\aaa.txt");
        try {
            r1 = new RandomAccessFile(file, "r");
            r2 = new RandomAccessFile("src\\aaaa.txt", "rw");
            int x = 0;
            byte[] b = new byte[1024];
            //将指针位移到文件的最后,添加数据添加到最后
            r2.seek(file.length());
            r2.write("fwq".getBytes());
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (r1 != null && r2 != null) {
                r1.close();
                r2.close();
            }
        }


    }
}

```

> 此操作会直接替换而不是覆盖.从前往后

复制文件夹文件
---

```java

public class CopyFiles {


    void into(File root, String dest) {
        File dest1 = new File(dest);
        File[] dir = root.listFiles();
        if (!dest1.exists()) {
            dest1.mkdirs();
        }
        for (int i = 0; i < dir.length; i++) {
            if (dir[i].isFile()) {
                copy(dir[i].getPath(), dest + "//" + dir[i].getName());
            } else {
                into(dir[i], dest + "//" + dir[i].getName());
            }
        }
    }

    void copy(String src, String dest) {
        File file1 = new File(src);
        File file2 = new File(dest);
        InputStreamReader in = null;
        OutputStreamWriter out = null;
        try {
            out = new OutputStreamWriter(new FileOutputStream(file2));
            in = new InputStreamReader(new FileInputStream(file1));
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        BufferedReader br = new BufferedReader(in);
        BufferedWriter bw = new BufferedWriter(out);
        char[] chars = new char[1024];
        while (true) {
            try {
                if (br.read(chars)==-1) break;
                bw.write(chars);
                bw.flush();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }

}

class main_T {
    public static void main(String[] args) {
        File file1 = new File("F://IO_T");
        CopyFiles c = new CopyFiles();
        c.into(file1, "F://IO_T2");
    }
}

```

ObjectInputStream：读取对象数据

DataInputStream：读取对象的某个属性

# NIO

- 





## Buffer

使用Buffer读写数据一般遵循以下四个步骤：

1. 写入数据到Buffer
2. 调用`flip()`方法
3. 从Buffer中读取数据
4. 调用`clear()`方法或者`compact()`方法

当向buffer写入数据时，buffer会记录下写了多少数据。一旦要读取数据，需要通过flip()方法将Buffer从写模式切换到读模式。在读模式下，可以读取之前写入到buffer的所有数据。

一旦读完了所有的数据，就需要清空缓冲区，让它可以再次被写入。有两种方式能清空缓冲区：调用clear()或compact()方法。clear()方法会清空整个缓冲区。compact()方法只会清除已经读过的数据。任何未读的数据都被移到缓冲区的起始处，新写入的数据将放到缓冲区未读数据的后面。

参数:

```java
	// 相当于辅助指针,
	private int mark = -1;
	//正在操作的位置,添加时指向最后
    private int position = 0;
	//限制,缓冲区内可访问的数据量.后面的值无法访问
    private int limit;
	//缓冲区最大容量
    private int capacity;
	//clear(); 负责清空所有指向,但不会清空数据,被遗忘状态
	//mark (); 在哪使用就负责标记position位置 reset(); position回到此位置
```

> 向Buffer中写数据

写数据到Buffer有两种方式：

- 从Channel写到Buffer。channel.read()
- 通过Buffer的put()方法写到Buffer里。buf.put() 

读数据也是如此

> rewind()

重新读

> 通道之间的通信

TransferFrom 接收通道接收来自发送通道的数据

TransferTo 发送通道发送给接收通道数据

## selector

Selector selector = Selector.open();
向Selector注册通道
为了将Channel和Selector配合使用，必须将channel注册到selector上。通过SelectableChannel.register()方法来实现，如下：


channel.configureBlocking(false);

SelectionKey key = channel.register(selector, Selectionkey.OP_READ);
与Selector一起使用时，==Channel必须处于非阻塞模式下==。这意味着不能将FileChannel与Selector一起使用，因为FileChannel不能切换到非阻塞模式。而套接字通道都可以。

注意register()方法的第二个参数。这是一个“interest集合”，意思是在通过Selector监听Channel时对什么事件感兴趣。可以监听四种不同类型的事件：

1. Connect
2. Accept
3. Read
4. Write

======================================================================================================

- int select()
- int select(long timeout)
- int selectNow()

`select()`阻塞到至少有一个通道在你注册的事件上就绪了。

`select(long timeout)`和select()一样，除了最长会阻塞timeout毫秒(参数)。

`selectNow()`不会阻塞，不管什么通道就绪都立刻返回

select()方法返回的int值表示有多少通道已经就绪。亦即，自上次调用select()方法后有多少通道变成就绪状态。如果调用select()方法，因为有一个通道变成就绪状态，返回了1，若再次调用select()方法，如果另一个通道就绪了，它会再次返回1。如果对第一个就绪的channel没有做任何操作，现在就有两个就绪的通道，但在每次select()方法调用之间，只有一个通道就绪了。



```java
Selector selector = Selector.open();
channel.configureBlocking(false);
//将选择器注册到通道
SelectionKey key = channel.register(selector, SelectionKey.OP_READ);

while(true) {
    //选择器轮询等待事件发生
  int readyChannels = selector.select();
    //没有事件重新轮询,有就往下执行
  if(readyChannels == 0) continue;
    //得到选择器感兴趣的事件而且已经发来的事件集合
  Set selectedKeys = selector.selectedKeys();
    
  Iterator keyIterator = selectedKeys.iterator();
  while(keyIterator.hasNext()) {
      //遍历
    SelectionKey key = keyIterator.next();
    if(key.isAcceptable()) {
        SocketChannel client = channel.accept(); //得到该通道,如果没有感兴趣事件,会造成一直堵塞.所以要在已经有感兴趣事件发生时调用
        // a connection was accepted by a ServerSocketChannel.
    } else if (key.isConnectable()) {
        // a connection was established with a remote server.
    } else if (key.isReadable()) {
        SocketChannel client = (SocketChannel) key.channel();
        // a channel is ready for reading
    } else if (key.isWritable()) {
        // a channel is ready for writing
    }
    keyIterator.remove();
  }
}
```



测试

```java
package NIO;

import java.nio.Buffer;
import java.nio.ByteBuffer;

public class test {
    public static void main(String[] args) {
        ByteBuffer b1=ByteBuffer.allocate(1024);
        System.out.println(b1.capacity());
        System.out.println(b1.position());
        System.out.println(b1.limit());
        System.out.println("------------------");
//        ==========================================
        b1.put("xugaowei".getBytes());
        System.out.println(b1.position());
        System.out.println(b1.capacity());
        System.out.println(b1.limit());
        System.out.println("------------------");
//        ==========================================
        //反转.写->读
        b1.flip();
        //恢复到起始位置
        System.out.println(b1.position());
        System.out.println(b1.capacity());
        System.out.println(b1.limit());
        System.out.println("------------------");
//        ==========================================
        byte[] b=new byte[b1.limit()];
        //将数据读取到b中
        b1.get(b);
        System.out.println(new String (b,0,b.length));
        System.out.println(b1.position());
        System.out.println(b1.capacity());
        System.out.println(b1.limit());
        System.out.println("------------------");
//        ==========================================

//      rewind重复读,将position返回到0
        b1.rewind();
        System.out.println(b1.position());
        System.out.println(b1.capacity());
        System.out.println(b1.limit());
        System.out.println("------------------");
//        ==========================================
        
    }
}

```

## channel 

- FileChannel
- DatagramChannel
- SocketChannel
- ServerSocketChannel

FileChannel 从文件中读写数据。

DatagramChannel 能通过UDP读写网络中的数据。

SocketChannel 能通过TCP读写网络中的数据。

ServerSocketChannel可以监听新进来的TCP连接，像Web服务器那样。对每一个新进来的连接都会创建一个SocketChannel。



### 非直接缓冲区

**非直接缓冲区：**
通过`allocate()`方法分配缓冲区，将缓存区建立在JVM内存中

```java
static ByteBuffer allocate(int capacity)
```

创建的缓冲区，在JVM中内存中创建，在每次调用基础操作系统的一个本机IO之前或者之后，虚拟机都会将缓冲区的内容复制到中间缓冲区（或者从中间缓冲区复制内容），缓冲区的内容驻留在JVM内，因此销毁容易，但是占用JVM内存开销，处理过程中有复制操作。
非直接缓冲区写入步骤：

1. 创建一个临时的直接ByteBuffer对象。
2. 将非直接缓冲区的内容复制到临时缓冲中。
3. 使用临时缓冲区执行低层次I/O操作。
4. 临时缓冲区对象离开作用域，并最终成为被回收的无用数据。
5. ![image-20201127181751127](image-20201127181751127.png)

```java
package NIO;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;
public class test1 {
    public static void main(String[] args) throws IOException {
        File file1 = new File("src\\aaa.txt");
        File file2 = new File("src\\qqq.txt");
        FileInputStream f1 = new FileInputStream(file1);
        FileOutputStream f2 = new FileOutputStream(file2);
        //获取通道
        FileChannel c1 = f1.getChannel();
        FileChannel c2 = f2.getChannel();
        //获取Buffer
        ByteBuffer b = ByteBuffer.allocate(1024);
        //将Buffer存入通道
            //读取Buffer
        while (c1.read(b)!=-1){
            //切换到写入模式
            b.flip();
            //写入
            c2.write(b);
            //清空
            b.clear();
        }
        f1.close();
        f2.close();
        c1.close();
        c2.close();
    }
}

```

没有处理异常

### 直接缓冲区

**直接缓冲区：**
通过`allocateDirect()`方法分配直接缓冲区，将缓冲区建立在物理内存中

> 只有ByteBuffer 才能使用

```java
static ByteBuffer allocateDirect(int capacity)
```

创建的缓冲区，在JVM内存外开辟内存，在每次调用基础操作系统的一个本机IO之前或者之后，虚拟机都会避免将缓冲区的内容复制到中间缓冲区（或者从中间缓冲区复制内容），缓冲区的内容驻留在物理内存内，会少一次复制过程，如果需要循环使用缓冲区，用直接缓冲区可以很大地提高性能。虽然直接缓冲区使JVM可以进行高效的I/O操作，但它使用的内存是操作系统分配的，绕过了JVM堆栈，建立和销毁比堆栈上的缓冲区要更大的开销。

![image-20201127181814128](image-20201127181814128.png)





```java
/*
       
```



```java

class t2{
    //内存映射文件方式
    public static void main(String[] args) throws IOException {
        /*static FileChannel open(Path path,
         Set<? extends OpenOption> options,
         FileAttribute<?>... attrs)
        打开或创建一个文件，返回一个文件通道来访问该文件。
        参数1:
        CREATE
        创建一个新的文件，如果它不存在。
        CREATE_NEW
        创建一个新的文件，如果文件已经存在，失败。
        READ,读权限
        WRITE,写权限
*/
        FileChannel c1 = FileChannel.open(Paths.get("F:\\文档\\121.ts"), StandardOpenOption.READ);
        FileChannel c2 = FileChannel.open(Paths.get("F:\\文档\\1211.ts"),StandardOpenOption.READ,StandardOpenOption.WRITE,StandardOpenOption.CREATE);

         /* FileChannel中的map方法可以将文件映射成内存映射文件MappedByteBuffer:
        map(FileChannel.MapMode mode, long position, long size)
        将此通道的文件的区域映射到内存中。
        参数1:枚举类型
       	static FileChannel.MapMode PRIVATE
        用于私有（写在写）映射的模式。
        static FileChannel.MapMode READ_ONLY
        只读映射的模式。
        static FileChannel.MapMode READ_WRITE
        用于读/写映射的模式。
		参数2:文件起始位置
		参数3:文件的大小
      */
        MappedByteBuffer bu1 =c1.map(FileChannel.MapMode.READ_ONLY,0,c1.size());
        MappedByteBuffer bu2 =c2.map(FileChannel.MapMode.READ_WRITE,0,c1.size());
        byte[] bytes=new byte[bu1.limit()];
        bu1.get(bytes);
        bu2.put(bytes);
    }
}

```



### 分散读取 聚集写入

```java
package NIO;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

public class fensanduqu {
    //分散写入,聚集读取
    public static void main(String[] args) throws IOException {
        //建立被操作文件的通道,读取文件
        FileInputStream f1 = new FileInputStream("F:\\文档\\121.ts");
        FileOutputStream f2=new FileOutputStream("F:\\文档\\12111.ts");
        FileChannel x1 = f1.getChannel();
        FileChannel x2 = f2.getChannel();
        //创建Buffer
        ByteBuffer b1 = ByteBuffer.allocate((int) (x1.size()/3));
        ByteBuffer b2 = ByteBuffer.allocate((int) (x1.size()/3));
        ByteBuffer b3 = ByteBuffer.allocate((int) (x1.size()/3));
        //使用多个Buffer写入
        ByteBuffer[] xx={b1,b2,b3};
        x1.read(xx);
        //全部切换到读取模式
        for (ByteBuffer byteBuffer : xx) {
            byteBuffer.flip();
        }
            x2.write(xx);

    }
}

```





### 阻塞式

```java
package NIO;

import org.junit.Test;

import java.io.IOException;
import java.net.InetAddress;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;
import java.nio.channels.ServerSocketChannel;
import java.nio.channels.SocketChannel;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;

public class Bloking {
    @Test
   public void client() throws IOException {
        //获取通道
        SocketChannel s = SocketChannel.open(new InetSocketAddress("127.0.0.1", 8080));
        //需要传输的文件
        FileChannel iCH = FileChannel.open((Paths.get("F:\\文档\\121.ts")), StandardOpenOption.READ);
        //创建Buffer
        ByteBuffer b1 = ByteBuffer.allocate((int) iCH.size());
        ByteBuffer b2 = ByteBuffer.allocate(1024);
        //写入Buffer
        while (iCH.read(b1) != -1) {
            b1.flip();
            s.write(b1);
            b1.clear();
        }
        s.shutdownOutput();
        int len=0;
        while ((len=s.read(b2))!=-1){
            b1.flip();
            System.out.println(new String(b2.array(),0,len));
        }
    }
    @Test
    public void Socket() throws IOException {
        //服务器端获取通道
        ServerSocketChannel ssc=ServerSocketChannel.open();
        //绑定连接
        ssc.bind(new InetSocketAddress(8080));
        //获取客户端连接通道
        SocketChannel accept = ssc.accept();
        //接收数据,保存(本地的
        FileChannel oCH = FileChannel.open(Paths.get("F:\\文档\\1221.ts"), StandardOpenOption.READ, StandardOpenOption.WRITE, StandardOpenOption.CREATE);
        //分配缓冲区
        ByteBuffer b=ByteBuffer.allocate(1024);
       while (accept.read(b)!=-1){
           b.flip();
           oCH.write(b);
           b.clear();
       }
       //反馈
        b.put("完美".getBytes());
       b.flip();
       accept.write(b);
       accept.shutdownOutput();
       ssc.close();
       accept.close();
       oCH.close();
    }
}

```



### 非阻塞式

```java
package NIO;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.*;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.Iterator;

public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocketChannel w1 = ServerSocketChannel.open();
        //修改为非阻塞状态
        w1.configureBlocking(false);
        //绑定端口号
        w1.bind(new InetSocketAddress(8080));
        //注册选择器,负责监听通道状态
        /* 注册Channel到Selector
        channel.configureBlocking(false);
        SelectionKey key = channel.register(selector, Selectionkey.OP_READ);
        Channel必须是非阻塞的。
        所以FileChannel不适用Selector，因为FileChannel不能切换为非阻塞模式，
        更准确的来说是因为FileChannel没有继承SelectableChannel。Socket channel可以正常使用。
        SelectableChannel抽象类 有一个 configureBlocking（）方法
        用于使通道处于阻塞模式或非阻塞模式。
        abstract SelectableChannel configureBlocking(boolean block)  */
        Selector selector=Selector.open();
        //将通道注册到注册选择器,选择OP_ACCEPT (接收)状态,才能和客户端建立连接
        /*public final SelectionKey register(Selector sel,int ops)
        *
        OP_READ :监听读状态
        OP_WRITE :监听写状态
        OP_CONNECT :监听连接状态
        OP_ACCEPT :监听接收状态
        * */
        //抽象理解为在此将监听来自客户端的申请,一旦接收到,就建立连接 第一关!!!!!
        w1.register(selector, SelectionKey.OP_ACCEPT);
        //随时监控管道是否有接收事件
        while (selector.select()>0){
            //迭代所有的事件
            Iterator<SelectionKey> iterator = selector.selectedKeys().iterator();
            while (iterator.hasNext()){
                SelectionKey sk=iterator.next();
                if (sk.isAcceptable()){
                    //有接收请求发送过来,就创建接收管道,继续添加读写权限 第二关!!!!
                    SocketChannel accept = w1.accept();
                    //接受管道设置为非阻塞状态
                    accept.configureBlocking(false);
                    //再将此管道注册到管理器,并且赋予权限
                    accept.register(selector,SelectionKey.OP_READ | SelectionKey.OP_WRITE);
                }
                else if (sk.isReadable() | sk.isWritable()){
                    SocketChannel  c2 = (SocketChannel)sk.channel();
                    ByteBuffer bb = ByteBuffer.allocate(1024);
                    FileChannel f = FileChannel.open(Paths.get("F:\\文档\\1221.txt"),
                            StandardOpenOption.READ,StandardOpenOption.WRITE,
                            StandardOpenOption.CREATE);
                    int len=0;
                    while ((len=c2.read(bb))!=-1){
                        bb.flip();
                        f.write(bb);
                        System.out.println(new String(bb.array(),0,len));
                        bb.clear();
                    }
                }
                iterator.remove();
            }

        }
    }
}


```

```java
package NIO;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SocketChannel;
import java.util.Date;

//非阻塞式IO
public class Client {
    public static void main(String[] args) throws IOException {
        SocketChannel q1 = SocketChannel.open(new InetSocketAddress("127.0.0.1", 8080));
        q1.configureBlocking(false);
        ByteBuffer b1 = ByteBuffer.allocate(1024);
        b1.put(new Date().toString().getBytes());
        b1.flip();
        q1.write(b1);
        b1.clear();
        q1.close();
    }
}
```

 



```java
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SelectionKey;
import java.nio.channels.Selector;
import java.nio.channels.ServerSocketChannel;
import java.nio.channels.SocketChannel;
import java.nio.charset.Charset;
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.Set;

public class NioServer {
    public static void main(String[] args) throws Exception{
        //创建服务端
        ServerSocketChannel serverSocketChannel = ServerSocketChannel.open();
        //设置为非阻塞模式
        serverSocketChannel.configureBlocking(false);
        //绑定端口
        serverSocketChannel.bind(new InetSocketAddress("localhost",12345));
        //创建selector
        Selector selector = Selector.open();
        //在selector中注册服务端的链接事件（注1）
        serverSocketChannel.register(selector, SelectionKey.OP_ACCEPT);
//    //用于存放客户端的链接，用远端的端口，作为唯一标识（由于是本机开启多个客户端进行测试，所以不存在端口冲突问题）
//    Map<Integer,SocketChannel> clients = new HashMap<>();
        List<SocketChannel> clients = new ArrayList<>();

        while (true){
            //阻塞等待事件的到来
            selector.select();
            //获取被触发的事件
            Set<SelectionKey> selectionKeys = selector.selectedKeys();
            Iterator<SelectionKey> iterator = selectionKeys.iterator();
            //遍历触发的事件
            while (iterator.hasNext()){
                try {
                    //获取事件
                    SelectionKey event = iterator.next();
                    //是否可以链接
                    if(event.isAcceptable()){
                        //为什么需要强转？ 因为在（注1）中，我们注册的是 ServerSocketChannel ，所有需要强转回来。（注2）
                        ServerSocketChannel ssc = (ServerSocketChannel) event.channel();
                        //获取到链接的socketchannel
                        SocketChannel socketChannel = ssc.accept();
                        socketChannel.configureBlocking(false);
                        //将获取到的链接，注册读事件到selector中，
                        socketChannel.register(selector,SelectionKey.OP_READ);
//          //将获取到的客户端，保存起来，用于跟其它客户端进行通信，由于不涉及线程问题，所以使用map足已
//          clients.put(((InetSocketAddress)socketChannel.getRemoteAddress()).getPort(),socketChannel);
                        clients.add(socketChannel);
                    }else if(event.isReadable()){ //是否可以读取
                        //同理（注2）
                        SocketChannel socketChannel = (SocketChannel) event.channel();
                        //创建socketChannel需要的buffer
                        ByteBuffer byteBuffer = ByteBuffer.allocate(512);
                        String receiveMessage = "";
                        while (true){
                            try{
                                //重置buffer
                                byteBuffer.clear();
                                int read = socketChannel.read(byteBuffer);
                                if(read <= 0 ){
                                    //当读取到末尾时，跳出循环
                                    break;
                                }
                                receiveMessage += new String(byteBuffer.array(), Charset.forName("UTF-8"));
                            }catch (Exception e){
                                e.printStackTrace();
                                break;
                            }
                        }
                        System.out.println("收到的消息为："+((InetSocketAddress)socketChannel.getRemoteAddress()).getPort()+"---"+receiveMessage);
                        //拼装需要发送的消息
                        final ByteBuffer otherbf = ByteBuffer.allocate(receiveMessage.length()+10);
                        otherbf.put((((InetSocketAddress)socketChannel.getRemoteAddress()).getPort()+":"+receiveMessage).getBytes());
                        System.out.println(new String(otherbf.array()));
                        //遍历客户端，发送消息
                        clients.stream().forEach(sc -> {
                            try {
                                if(((InetSocketAddress)socketChannel.getRemoteAddress()).getPort() ==
                                        ((InetSocketAddress)sc.getRemoteAddress()).getPort()){
                                    //消息不发给自己
                                }else{
                                    otherbf.flip();
                                    sc.write(otherbf);
                                }
                            }catch (Exception e){
                                e.printStackTrace();
                            }
                        });
                    }
                }catch (Exception e){
                    //添加try是为了程序的健壮
                    e.printStackTrace();
                }finally {
                    //删除已经处理了的事件
                    iterator.remove();
                }
            }
        }
    }
}
```



# 多线程





**调用 `start()` 方法方可启动线程并使线程进入就绪状态，直接执行 `run()` 方法的话不会以多线程的方式执行**





**`synchronized` 关键字解决的是多个线程之间访问资源的同步性，`synchronized`关键字可以保证被它修饰的方法或者代码块在任意时刻只能有一个线程执行。**





**synchronized 关键字最主要的三种使用方式：**

**1.修饰实例方法:** 作用于当前对象实例加锁，进入同步代码前要获得 **当前对象实例的锁**

```
synchronized void method() {
  //业务代码
}
```

**2.修饰静态方法:** 也就是给当前类加锁，会作用于类的所有对象实例 ，进入同步代码前要获得 **当前 class 的锁**。因为静态成员不属于任何一个实例对象，是类成员（ *static 表明这是该类的一个静态资源，不管 new 了多少个对象，只有一份*）。所以，如果一个线程 A 调用一个实例对象的非静态 `synchronized` 方法，而线程 B 需要调用这个实例对象所属类的静态 `synchronized` 方法，是允许的，不会发生互斥现象，**因为访问静态 `synchronized` 方法占用的锁是当前类的锁，而访问非静态 `synchronized` 方法占用的锁是当前实例对象锁**。

```
synchronized static void method() {
//业务代码
}
```

**3.修饰代码块** ：指定加锁对象，对给定对象/类加锁。`synchronized(this|object)` 表示进入同步代码库前要获得**给定对象的锁**。`synchronized(类.class)` 表示进入同步代码前要获得 **当前 class 的锁**

```
synchronized(this) {
  //业务代码
}
```

**总结：**

- `synchronized` 关键字加到 `static` 静态方法和 `synchronized(class)` 代码块上都是是给 Class 类上锁。
- `synchronized` 关键字加到实例方法上是给对象实例上锁。
- 尽量不要使用 `synchronized(String a)` 因为 JVM 中，字符串常量池具有缓存功能！

```
public class Singleton {

    private volatile static Singleton uniqueInstance;

    private Singleton() {
    }

    public  static Singleton getUniqueInstance() {
       //先判断对象是否已经实例过，没有实例化过才进入加锁代码
        if (uniqueInstance == null) {
            //类对象加锁
            synchronized (Singleton.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```

另外，需要注意 `uniqueInstance` 采用 `volatile` 关键字修饰也是很有必要。

`uniqueInstance` 采用 `volatile` 关键字修饰也是很有必要的， `uniqueInstance = new Singleton();` 这段代码其实是分为三步执行：

1. 为 `uniqueInstance` 分配内存空间
2. 初始化 `uniqueInstance`
3. 将 `uniqueInstance` 指向分配的内存地址

但是由于 JVM 具有指令重排的特性，执行顺序有可能变成 1->3->2。指令重排在单线程环境下不会出现问题，但是在多线程环境下会导致一个线程获得还没有初始化的实例。例如，线程 T1 执行了 1 和 3，此时 T2 调用 `getUniqueInstance`() 后发现 `uniqueInstance` 不为空，因此返回 `uniqueInstance`，但此时 `uniqueInstance` 还未被初始化。

使用 `volatile` 可以禁止 JVM 的指令重排，保证在多线程环境下也能正常运行。

> 构造方法可以使用 synchronized 关键字修饰么？

先说结论：**构造方法不能使用 synchronized 关键字修饰。**

构造方法本身就属于线程安全的，不存在同步的构造方法一说。



## CAS

底层实现原理：

Unsafe类是直接操作系统中内存的类。atomic类中依靠的就是unsafe类，对对象进行操作时，直接获取内存地址值，然后进行操作

![image-20210420155804991](E:\文档\JAVA笔记\Typora\image-20210420155804991.png)

var5 就是从主存中复制到工作内存中的值。这里并没有使用synchornized也可以实现强一致性，使用了do-while循环，会一直判断期望值是否和主内存中的值是否相等。

<img src="E:\文档\JAVA笔记\Typora\image-20210420161953656.png" alt="image-20210420161953656" style="zoom:67%;" />

<img src="E:\文档\JAVA笔记\Typora\image-20210420162713060.png" alt="image-20210420162713060" style="zoom: 67%;" />



1. lock：将主存中的变量标记为独占。
2. read：操作于主内存，将变量传送给线程工作内存
3. load：将load传来的变量复制到工作内存的副本中
4. use：当虚拟机需要使用这个值时，交给执行引擎执行
5. asign：执行完毕后将值重新赋值给副本
6. store：将副本中的值传回到主内存
7. write：除安徽的值重新赋给这内存变量
8. unlock：解锁。

- 不允许read和load、store和write的操作单独出现。
- 不允许一个线程丢弃它的最近assign的操作，即变量在工作内存中改变了之后必须同步到主内存中。
- 不允许一个线程无原因地（没有发生过任何assign操作）把数据从工作内存同步回主内存中。
- 一个新的变量只能在主内存中诞生，不允许在工作内存中直接使用一个未被初始化（load或assign）的变量。即就是对一个变量实施use和store操作之前，必须先执行过了assign和load操作。
- 一个变量在同一时刻只允许一条线程对其进行lock操作，lock和unlock必须成对出现
- 如果对一个变量执行lock操作，将会清空工作内存中此变量的值，在执行引擎使用这个变量前需要重新执行load或assign操作初始化变量的值
- 如果一个变量事先没有被lock操作锁定，则不允许对它执行unlock操作；也不允许去unlock一个被其他线程锁定的变量。
- 对一个变量执行unlock操作之前，必须先把此变量同步到主内存中（执行store和write操作）。





## volatile

```
public class VolatileTest {

    volatile boolean isStop = false;

    public void test(){
        Thread t1 = new Thread(){
            public void run() {
                isStop=true;
            }
        };
        Thread t2 =  new Thread(){
            public void run() {
                while (!isStop);
            }
        };
        t2.start();
        t1.start();
    }
    public static void main(String args[]) throws InterruptedException {
        for (int i =0;i<25;i++){
            new VolatileTest().test();
        }

    }
}
```

保证了其他线程的可见性。

> ThreadLocal

一般情况下共享变量可以被多个线程所访问，ThreadLocal可以将变量复制到每个线程中的副本中，每个线程中都有一份该变量。

**最终的变量是放在了当前线程的 `ThreadLocalMap` 中，并不是存在 `ThreadLocal` 上，`ThreadLocal` 可以理解为只是`ThreadLocalMap`的封装，传递了变量值。** `ThrealLocal` 类中可以通过`Thread.currentThread()`获取到当前线程对象后，直接通过`getMap(Thread t)`可以访问到该线程的`ThreadLocalMap`对象。

> 实现 Runnable 接口和 Callable 接口的区别

`Runnable`自 Java 1.0 以来一直存在，但`Callable`仅在 Java 1.5 中引入,目的就是为了来处理`Runnable`不支持的用例。**`Runnable` 接口**不会返回结果或抛出检查异常，但是**`Callable` 接口**可以。





## ABA问题解决



```java
public void volatiletest() {
        String s = new String("111");
        AtomicStampedReference<String> i = new AtomicStampedReference<>(s, 1);
        int[] ints = new int[1];
        System.out.println(i.compareAndSet(s, "24", 1, 2));
        System.out.println(i.compareAndSet("24", "25", 2, 3));
        String s1 = i.get(ints);    //需要传入数组，array[0]就是时间戳
        System.out.println(s1);     //
        System.out.println(ints[0]); //时间戳号
    }
```



## ReentrantLock

与Synchronized区别：有公平锁+非公平锁

1. 有限时等待
2. 可中断响应
3. 实现精准唤醒

> 不支持锁升级 ，支持降级 。写锁->读锁，但是降级之后，代码执行完毕需要释放写锁

```java
public class ReentrantLockTest {
    private final Lock lock = new ReentrantLock(true);  公平锁

    @Test
    public void t1() {
        ReentrantLockTest reentrantLockTest = new ReentrantLockTest();
        for (int i = 0; i < 4; i++) {
            new Thread(() -> {
                System.out.println(Thread.currentThread().getName() + "运行");
                reentrantLockTest.add();
            }).start();
        }
    }
    void add() {
        System.out.println(Thread.currentThread().getName() + "--------------获得锁");
        try {
            lock.lock();
        } finally {
            lock.unlock();
        }
    }

}
```

## 自旋锁

```
public class SpinLockDemo {

    // 现在的泛型装的是Thread，原子引用线程
    AtomicReference<Thread>  atomicReference = new AtomicReference<>();

    public void myLock() {
        // 获取当前进来的线程
        Thread thread = Thread.currentThread();
        System.out.println(Thread.currentThread().getName() + "\t come in ");

        // 开始自旋，期望值是null，更新值是当前线程，如果是null，则更新为当前线程，否者自旋
        while(!atomicReference.compareAndSet(null, thread)) {

        }
    }

    /**
     * 解锁
     */
    public void myUnLock() {

        // 获取当前进来的线程
        Thread thread = Thread.currentThread();

        // 自己用完了后，把atomicReference变成null
        atomicReference.compareAndSet(thread, null);

        System.out.println(Thread.currentThread().getName() + "\t invoked myUnlock()");
    }
```

## 可重入锁

在外层方法中获取到的锁和在内层方法中锁是同一个锁

```
public synchronized void method1() {
	method2();
}

public synchronized void method2() { //两个锁相同，可以直接执行本方法

}

```



```
测试Thread中的常用方法：
 * 1. start():启动当前线程；调用当前线程的run()
 * 2. run(): 通常需要重写Thread类中的此方法，将创建的线程要执行的操作声明在此方法中
 * 3. currentThread():静态方法，返回执行当前代码的线程
 * 4. getName():获取当前线程的名字
 * 5. setName():设置当前线程的名字
 * 6. yield():释放当前cpu的执行权
 * 7. join():在线程a中调用线程b的join(),此时线程a就进入阻塞状态，直到线程b完全执行完以后，线程a才
 *           结束阻塞状态。也可以用作主线程等待子线程!!!!!!!!
 * 8. stop():已过时。当执行此方法时，强制结束当前线程。
 * 9. sleep(long millitime):让当前线程“睡眠”指定的millitime毫秒。在指定的millitime毫秒时间内，当前
 *                          线程是阻塞状态。
 * 10. isAlive():判断当前线程是否存活
  	getPriority():获取线程的优先级
    setPriority(int p):设置线程的优先级
```



卖票
---



```java
package Day01;

public class ThreadTest {
    public static void main(String[] args) {
        Sale ticket = new Sale();
        Thread win1 = new Thread(ticket);
        Thread win2 = new Thread(ticket);
        win1.setName("一号");
        win2.setName("二号");
        win1.start();
        win2.start();
    }
}
class Sale implements Runnable {
    private int x = 100;
    private boolean flag = true;
    @Override
    public void run() {
        while (flag) {
            synchronized (this) {
                if (x <= 1) {
                    flag = false;
                }
                System.out.println(Thread.currentThread().getName() + "卖出" + x + ",剩余票：----" + --x);
            }
        }
    }
}

```

账号存、取钱
---

```java
public class cun implements Runnable{
    private count count;
    int cunduoshao;

    public cun(count count, int cunduoshao) {
        this.count = count;
        this.cunduoshao = cunduoshao;
    }
    @Override
    public void run() {
        if (cunduoshao>0){
            count.setMoney(count.getMoney()+cunduoshao);
            System.out.println(Thread.currentThread().getName()+cunduoshao);
            System.out.println("余额"+count.getMoney());
        }
    }
}


----------------------------
package Day01.count;

public class qu implements Runnable {
    private count count;
    int quduoshao;
    public qu(count count, int quduoshao) {
        this.count = count;
        this.quduoshao = quduoshao;
    }

    @Override
    public void run() {
        if (count.getMoney()>= quduoshao) {
            count.setMoney(count.getMoney() - quduoshao);
            System.out.println(Thread.currentThread().getName()+quduoshao);
            System.out.println("余额"+count.getMoney());
        }else {
            System.out.println("余额不足");
        }
    }
}
----------------------------
package Day01.count;

public class count {
    private int money;

    public count(int money) {
        this.money = money;
    }

    public int getMoney() {
        return money;
    }

    public void setMoney(int money) {
        this.money = money;
    }
}
class test1{
    public static void main(String[] args) {
        count count = new count(5000);
        for (int i = 0; i < 10; i++) {
        qu qu = new qu(count,100);
        cun cun1 = new cun(count,500);
        Thread cun = new Thread(cun1);
        Thread quu = new Thread(qu);
        cun.setName("存");
        quu.setName("取");
        cun.start();
        quu.start();
        }
    }
}

```





## 生产者消费者问题

```java
package ThreadTest;

public class ProductAndCustom {
    public static void main(String[] args) {
        sale sale = new sale();
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    sale.get();
                }
            }, "t1").start();
        }
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    sale.get();
                }
            }, "t2").start();
        }
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    sale.out();
                }
            }, "t3").start();
        }
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    sale.out();
                }
            }, "t4").start();
        }
    }
}

class sale {
    private int shoes = 0;
    synchronized void get() {
       while (shoes!=0){
           try {
               this.wait();

           } catch (InterruptedException e) {
               e.printStackTrace();
           }

       }
           shoes++;
           System.out.println(Thread.currentThread().getName()+"--->"+shoes);
           this.notifyAll();
    }
   synchronized void out() {
        while (shoes==0){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
            shoes--;
            System.out.println(Thread.currentThread().getName()+"--->"+shoes);
            this.notifyAll();

    }
}


```

## 生产者消费者问题Lock

```java
package ThreadTest;

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class ProductAndCustomLock {
    public static void main(String[] args) {
        sale2 sale = new sale2();
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    sale.get();
                }
            }, "t1").start();
        }
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    sale.get();
                }
            }, "t2").start();
        }
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    sale.out();
                }
            }, "t3").start();
        }
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    sale.out();
                }
            }, "t4").start();
        }
    }
}

class sale2 {
    private int shoes = 0;
    private Lock lock=new ReentrantLock();
     void get() {
         
         while (shoes!=0){
            lock.lock();
            try {
                this.wait();

            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
         shoes++;
        System.out.println(Thread.currentThread().getName()+"--->"+shoes);
        this.notifyAll();
        lock.unlock();


    }
     void out() {
        while (shoes==0){
            lock.lock();
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
        shoes--;
        System.out.println(Thread.currentThread().getName()+"--->"+shoes);
        this.notifyAll();
        lock.unlock();

    }
}



```

## 线程八锁

[http://www.zyiz.net/tech/detail-132234.html](http://www.zyiz.net/tech/detail-132234.html)

原理要搞清锁的对象!!!!!!!!!!!!!!!!!!!!!!

## 线程通信实现精准唤醒

首先看普通用法，唤醒所有的，前提是只有两个线程才可以使用

```java
package ThreadTest;

public class notifywait {
    public static void main(String[] args) {
        printTest1 printTest1 = new printTest1();
        Thread thread = new Thread(printTest1);
        thread.setName("1----------");
        Thread thread2 = new Thread(printTest1);
        thread2.setName("2--");
        thread.start();
        thread2.start();
    }
}

class printTest1 implements Runnable {
    private int x = 0;
    private Object object = new Object();
    private boolean flag = true;

    @Override
    public void run() {
        while (flag) {
            synchronized (object) {
                object.notifyAll();//要首先唤醒所有等待的线程，因为已经是被锁住了。安全
                ++x;
                System.out.println(Thread.currentThread().getName() + x);
                if (x==100) flag=false;
                try {
                    object.wait();//会在此释放锁 
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```



```java
package ThreadTest;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

//实现精准唤醒
public class notifySingle {
    public static void main(String[] args) {
        A a = new A();
        for (int i = 0; i <5 ; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    a.a();
                }
            }, "t1").start();
        }
        for (int i = 0; i < 5; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    a.b();
                }
            }, "t2").start();
        }
        for (int i = 0; i < 5; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    a.c();
                }
            }, "t3").start();
        }

    }
}

class A {
    private Lock lock = new ReentrantLock();

    private int num = 1;//线程排名
    Condition condition1 = lock.newCondition();
    Condition condition2 = lock.newCondition();
    Condition condition3 = lock.newCondition();

    void a() {

        lock.lock();
        while (num != 1) {
            try {
                condition1.await();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        try {
            System.out.println(Thread.currentThread().getName() + "---->A");
            num = 2;
            condition2.signal();
        } finally {
            lock.unlock();
        }

    }

    void b() {
        lock.lock();
        while (num != 2) {
            try {
                condition2.await();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        try {
            System.out.println(Thread.currentThread().getName() + "---->B");
            num = 3;
            condition3.signal();
        } finally {
            lock.unlock();
        }

    }

    void c() {

        lock.lock();
        while (num != 3) {
            try {
                condition3.await();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        try {

            System.out.println(Thread.currentThread().getName() + "---->C");
            num = 1;
            condition1.signal();
        } finally {
            lock.unlock();
        }

    }
}

```

面试题
---

```
面试题：sleep() 和 wait()的异同？
 * 1.相同点：一旦执行方法，都可以使得当前的线程进入阻塞状态。
 * 2.不同点：1）两个方法声明的位置不同：Thread类中声明sleep() , Object类中声明wait()
 *          2）调用的要求不同：sleep()可以在任何需要的场景下调用。 wait()必须使用在同步代码块或同步方法中
 *          3）关于是否释放同步监视器：如果两个方法都使用在同步代码块或同步方法中，sleep()不会释放锁，wait()会释放锁。
 *
```



## 集合安全问题

### ArrayList.Set

<img src="image-20201231162631612.png" alt="image-20201231162631612" style="zoom:50%;" />

```java
1 	CopyOnWriteArrayList<Object> list = new CopyOnWriteArrayList<>();//写入时复制
2    //        List<String> list = Collections.synchronizedList(new ArrayList<String>());
```

### Map

![image-20201231162735074](image-20201231162735074.png)

```java
ConcurrentHashMap<Object, Object> map = new ConcurrentHashMap<>();
```



## Callable

```java
package ThreadTest;

import java.util.concurrent.Callable;
import java.util.concurrent.FutureTask;

public class Callabletest {
    public static void main(String[] args) {
        testcall testcall = new testcall();
        FutureTask futureTask=new FutureTask(testcall);
        new Thread(futureTask,"t1").start();
    }
}
class testcall implements Callable {

    @Override
    public Object call() throws Exception {
        System.out.println("??????????????");
        return null;
    }
}
```

FutureTask可以将callable的实现类和Thread建立联系

## CountDownLatch

![image-20201231164051046](image-20201231164051046.png)

```java
 ThreadPoolExecutor executor = new ThreadPoolExecutor(5, 8, 60L, TimeUnit.SECONDS, new ArrayBlockingQueue<>(1000));
        CountDownLatch countDownLatch = new CountDownLatch(1);
            executor.execute(() -> {
                try {
                    System.out.println(Thread.currentThread().getName());
                    Thread.sleep(3000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } finally {
                    countDownLatch.countDown();//切记.无论如何都要加finally
                }
            });
        // 阻塞当前线程，知道所有子线程都执行countDown方法才会继续执行
        countDownLatch.await();
        System.out.println("结束====================");
    }
```

## CyclicBarrier

![image-20201231165238867](image-20201231165238867.png)

```java
package ThreadTest;
import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;
public class CyclicBarrierTest1 {
    public static void main(String[] args) {
        final CyclicBarrier barrier = new CyclicBarrier(6, new Runnable() {
            @Override
            public void run() {
                System.out.println("收集完毕");
            }
        });
        for (int i = 1; i <= 6; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    System.out.println("龙珠");
                    try {
                        barrier.await();//执行完的线程在此等等待，计数器为六继续执行
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    } catch (BrokenBarrierException e) {
                        e.printStackTrace();
                    }

                }
            }).start();
        }
    }
}

class Aa1 {
    void ddd() {
        System.out.println(Thread.currentThread().getName() + "线程执行");
    }
}
```



![image-20210519165013212](E:\文档\JAVA笔记\Typora\image-20210519165013212.png)

1）CountDownLatch简单的说就是一个线程等待，直到他所等待的其他线程都执行完成并且调用countDown()方法发出通知后，当前线程才可以继续执行。
2）cyclicBarrier是所有线程都进行等待，直到所有线程都准备好进入await()方法之后，所有线程同时开始执行！
3）CountDownLatch的计数器只能使用一次。而CyclicBarrier的计数器可以使用reset() 方法重置。所以CyclicBarrier能处理更为复杂的业务场景，比如如果计算发生错误，可以重置计数器，并让线程们重新执行一次。



## 线程池

``` java 
package ThreadTest;

import java.util.concurrent.*;

public class pool {
    public static void main(String[] args) {
        //以下三种不推荐
//        Executors.newSingleThreadExecutor();//创建单一线程
//        Executors.newFixedThreadPool(5);//创建5个线程
//        Executors.newCachedThreadPool();//遇强则强,遇弱则弱

        //自定义线程池
        final ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(
                5,
                10,
                30, TimeUnit.SECONDS,
                new LinkedBlockingDeque<>(5),
                Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.AbortPolicy()
        );
        try {
            for (int i = 1; i <= 15; i++) {
                threadPoolExecutor.execute(new Runnable() {
                    @Override
                    public void run() {

                        System.out.println(Thread.currentThread().getName());
                    }

                });

            }
        } finally {
            threadPoolExecutor.shutdown();
        }
    }
}
```

Executor 是父接口 



> 源码分析

```java
public ThreadPoolExecutor(int corePoolSize, //核心线程池大小
                              int maximumPoolSize, //最大线程池大小
                              long keepAliveTime, //超时了没人调用的存活时间
                              TimeUnit unit, //单位
                              BlockingQueue<Runnable> workQueue, //阻塞队列
                              ThreadFactory threadFactory, //线程池工厂
                              RejectedExecutionHandler handler ) { //拒绝策略
    //最多承载的线程数=maximumPoolSize+BlockingQueue
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.acc = System.getSecurityManager() == null ?
                null :
                AccessController.getContext();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
```

### 四种拒绝策略

| 拒绝策略            | 详情                                               |
| ------------------- | -------------------------------------------------- |
| AbortPolicy         | 默认的，线程数超出最大承载线程数时抛出异常         |
| CallerRunsPolicy    | 哪来的回哪去，用main线程执行                       |
| DiscardPolicy       | 直接扔掉，不会抛出异常，也不会有线程执行多余的任务 |
| DiscardOldestPolicy | 队列满了会和第一个线程竞争，不会抛出异常           |

### CPU密集型和IO密集型

| CPU密集型                                  | IO密集型                                       |
| ------------------------------------------ | ---------------------------------------------- |
| 根据电脑的CPU核心数创建线程池              | 根据IO线程的大小创建线程池 大于io线程的2倍为宜 |
| Runtime.getRuntime().availableProcessors() | ——                                             |



semaphore信号量
---

> 抢车位原理：只提供3个车位，6辆车交替停车

```java
package Thread_T;

import java.util.concurrent.Semaphore;
import java.util.concurrent.TimeUnit;

public class semaphoreTest {
        public static void main(String[] args) {
            final Semaphore semaphore = new Semaphore(3);
            for (int i = 1; i <= 6; i++) {

                new Thread(new Runnable() {

                    @Override
                    public void run() {
                        try {
                            semaphore.acquire();//获得车位 -1 操作 并且进入等待状态
                            System.out.println(Thread.currentThread().getName());
                            TimeUnit.SECONDS.sleep(1);
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }finally {
                            semaphore.release();//释放操作 唤醒所有等待状态的线程
                        }
                    }
                }).start();

            }
        }
}
```

ReadWriteLock 读写锁
---

> 是RenntrantLock 下的更加细粒度的锁 	独占锁:写锁     共享锁：读锁

```java
package Thread_T;

import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class ReadWrite {
    public static void main(String[] args) {
        readandwrite r = new readandwrite();
        for (int i = 0; i < 5; i++) {
            final int te = i;
            new Thread(() ->
            {
                r.write(String.valueOf(te), te);
            }).start();
        }
        for (int i = 0; i < 5; i++) {
            final int te = i;
            new Thread(() ->
            {
                r.read(String.valueOf(te));
            }).start();
        }
    }
}

class readandwrite {
    Map x = new HashMap();
    ReadWriteLock readWriteLock = new ReentrantReadWriteLock();

    void read(String ss) {
        readWriteLock.readLock().lock();

        Object o;
        try {
            o = x.get(ss);
            System.out.println(Thread.currentThread().getName() + "读取" + o);
        } finally {
            readWriteLock.readLock().unlock();
        }
    }
    void write(String s, Object o) {
        readWriteLock.writeLock().lock();
        try {
            System.out.println(Thread.currentThread().getName() + "写入" + s);
            x.put(s, o);
            System.out.println(Thread.currentThread().getName() + "写入ok" + s);
        } finally {
            readWriteLock.writeLock().unlock();
        }

    }
}

```

BlockingQueue阻塞队列--四组API
---

| 方式     | 抛出异常  | 有返回值，不抛异常 | 阻塞等待 | 超时等待 |
| -------- | --------- | ------------------ | -------- | -------- |
| 添加     | add()     | offer()            | put()    | offer()  |
| 取出     | remove()  | poll()             | take()   | poll()   |
| 检测队首 | element() | peek()             | -        | -        |

1. ```java
   public class BlockingQueue {
           public static void main (String[]args){
               ArrayBlockingQueue queue = new ArrayBlockingQueue(3);
               System.out.println(queue.add("a"));
               System.out.println(queue.add("b"));
               System.out.println(queue.add("c"));
               System.out.println(queue.add("d"));
           }
   }
   //--------------------------
   true
   true
   true
   Exception in thread "main" java.lang.IllegalStateException: Queue full
   	at java.util.AbstractQueue.add(AbstractQueue.java:98)
   	at java.util.concurrent.ArrayBlockingQueue.add(ArrayBlockingQueue.java:312)
   	at Thread_T.BlockingQueue.main(BlockingQueue.java:11)
   
   ```

2. ```java
   public class BlockingQueue {
           public static void main (String[]args){
               ArrayBlockingQueue queue = new ArrayBlockingQueue(3);
               System.out.println(queue.offer("a"));
               System.out.println(queue.offer("v"));
               System.out.println(queue.offer("b"));
               System.out.println(queue.offer("c"));
               System.out.println(queue.poll());
           }
   }
   //----------------
   true
   true
   true
   false
   a
   ```

3. ```java
   public class BlockingQueue {
           public static void main (String[]args) throws InterruptedException {
               ArrayBlockingQueue queue = new ArrayBlockingQueue(3);
                queue.put("a");
           queue.put("b");
           queue.put("c");
           System.out.println(queue.take());
           queue.put("d");//会进行阻塞等待状态。等待被取出。后面的不会执行
           }
   }
   
   ```

4. ```java
   public class BlockingQueue {
           public static void main (String[]args) throws InterruptedException {
               ArrayBlockingQueue queue = new ArrayBlockingQueue(3);
           System.out.println(queue.offer("a"));
           System.out.println(queue.offer("v"));
           System.out.println(queue.offer("b"));
           queue.offer("c",2, TimeUnit.SECONDS)；
   }
   
   ```

   

SynchronousQueue 同步队列
---

> 一次只能添加一个数据，当取出的时候才能往下添加。和semaphore差不多

```java
SynchronousQueue<String> o = new SynchronousQueue<>();
        new Thread(() ->
        {
            try {
                o.put("a" );
                System.out.println("t1添加完成");
                o.put("b" );
                System.out.println("t1添加完成");
                o.put("c" );
                System.out.println("t1添加完成");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"t1").start();
        new Thread(() ->
        {
            try {
                TimeUnit.SECONDS.sleep(2);
                System.out.println( o.take());
                TimeUnit.SECONDS.sleep(2);
                System.out.println( o.take());
                TimeUnit.SECONDS.sleep(2);
                System.out.println( o.take());
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"t2").start();

```



ForkJoin
---

> 多个线程将任务分成几个小任务，再将结果合并
>
> 特点：工作窃取。一个线程执行完毕后会窃取其他还未执行完毕的线程的任务。双端队列。

```java
package Thread_T;

import java.time.Duration;
import java.time.Instant;
import java.util.concurrent.*;
import java.util.stream.LongStream;

public class CountTaskForkJoinTest2 extends RecursiveTask<Long> {
    private long start;
    private long end;

    public CountTaskForkJoinTest2(long start, long end) {
        this.start = start;
        this.end = end;
    }

    @Override
    protected Long compute() {
        long x = 0;
        if (end - start < 10000L) {
            for (long i = start; i <= end; i++) {
                x += i;
            }
        } else {
            long mi = (end - start) / 2;
            CountTaskForkJoinTest c1 = new CountTaskForkJoinTest(start, mi);
            CountTaskForkJoinTest c2 = new CountTaskForkJoinTest(mi + 1, end);
            c1.fork();
            c2.fork();
            Long o = c1.join();
            Long t = c2.join();
            x = o + t;
        }
        return x;
    }


//        public static void main(String[] args) {
//        long start_index = 0L;
//        long end_index = 1000000000L;
//
//        CountTaskForkJoinTest2 t2 = new CountTaskForkJoinTest2(start_index, end_index);
//        ForkJoinPool forkJoinPool = new ForkJoinPool();
//        ForkJoinTask<Long> submit = forkJoinPool.submit(t2);
//        try {
//            Long aLong = submit.get();
//            System.out.println("result: " + aLong);
//        } catch (InterruptedException e) {
//            e.printStackTrace();
//        } catch (ExecutionException e) {
//            e.printStackTrace();
//        }
//
//    }
    ----------------------------------------------------
//    public static void main(String[] args) {
//        long x=0;
//        long l = System.currentTimeMillis();
//        for (long i = 0; i <=1000000000L ; i++) {
//            x+=i;
//        }
//        long l2 = System.currentTimeMillis();
//
//        System.out.println(l2-l);
//        System.out.println(x);
//    }
        、、    ----------------------------------------------------
public static void main(String[] args) {
    long l = System.currentTimeMillis();
    long reduce = LongStream.rangeClosed(0L, 1000000000L).parallel().reduce(0, Long::sum);
    System.out.println(reduce);
    long l2 = System.currentTimeMillis();
    System.out.println(l2-l);
    }
}

```

异步回调
---

```java
package Thread_T;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.TimeUnit;

public class CompletableTest {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //无返回值异步回掉
//        CompletableFuture<Void> c = CompletableFuture.runAsync(() -> {
//                try {
//                    TimeUnit.SECONDS.sleep(3);
//                    System.out.println("线程异步回掉");
//                } catch (InterruptedException e) {
//                    e.printStackTrace();
//                }
//
//        });
//        System.out.println("111111");
//        c.get();//获取线程执行结果



//        ----------------------------------
//        有返回值异步回掉
/*public static <U> CompletableFuture<U> supplyAsync(Supplier<U> supplier) {
	是供给型接口  
 */
        CompletableFuture<Integer> completableFuture =
                CompletableFuture.supplyAsync(() -> {
                    try {
                        TimeUnit.SECONDS.sleep(3);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName() + "supplyAsync=>Integer");

                    return 1024;
                });
        System.out.println("主线程继续执行");
        System.out.println(completableFuture.whenComplete((t, u) -> {//会在此阻塞
            System.out.println("t=>" + t); // 正常的返回结果
            System.out.println("u=>" + u); // 错误信息：java.util.concurrent.CompletionException:java.lang.ArithmeticException: /byzero
        }).exceptionally((e) -> {
            System.out.println(e.getMessage());
            return 233; // 可以获取到错误的返回结果
        }).get());
    }
}
```



JMM
---

<img src="image-20201230153823864.png" alt="image-20201230153823864" style="zoom:50%;" />

内存交互操作有8种，虚拟机实现必须保证每一个操作都是原子的，不可在分的（对于double和long类型的变量来说，load、store、read和write操作在某些平台上允许例外）

- lock   （锁定）：作用于主内存的变量，把一个变量标识为线程独占状态

- unlock （解锁）：作用于主内存的变量，它把一个处于锁定状态的变量释放出来，释放后的变量才可以被其他线程锁定
- read  （读取）：作用于主内存变量，它把一个变量的值从主内存传输到线程的工作内存中，以便随后的load动作使用
- load   （载入）：作用于工作内存的变量，它把read操作从主存中变量放入工作内存中
- use   （使用）：作用于工作内存中的变量，它把工作内存中的变量传输给执行引擎，每当虚拟机遇到一个需要使用到变量的值，就会使用到这个指令
- assign （赋值）：作用于工作内存中的变量，它把一个从执行引擎中接受到的值放入工作内存的变量副本中
- store  （存储）：作用于主内存中的变量，它把一个从工作内存中一个变量的值传送到主内存中，以便后续的write使用
- write 　（写入）：作用于主内存中的变量，它把store操作从工作内存中得到的变量的值放入主内存的变量中

　　==JMM对这八种指令的使用，制定了如下规则：==

- - 不允许read和load、store和write操作之一单独出现。即使用了read必须load，使用了store必须write
  - 不允许线程丢弃他最近的assign操作，即工作变量的数据改变了之后，必须告知主存
  - 不允许一个线程将没有assign的数据从工作内存同步回主内存
  - 一个新的变量必须在主内存中诞生，不允许工作内存直接使用一个未被初始化的变量。就是怼变量实施use、store操作之前，必须经过assign和load操作
  - 一个变量同一时间只有一个线程能对其进行lock。多次lock后，必须执行相同次数的unlock才能解锁
  - 如果对一个变量进行lock操作，会清空所有工作内存中此变量的值，在执行引擎使用这个变量前，必须重新load或assign操作初始化变量的值
  - 如果一个变量没有被lock，就不能对其进行unlock操作。也不能unlock一个被其他线程锁住的变量
  - 对一个变量进行unlock操作之前，必须把此变量同步回主内存

## Volatile

> 1. 保证可见性
> 2. 不保证原子性
> 3. 禁止指令重排

1. 可见性：在工作内存中可以和主存保持一致
2. 如下：

```java
public class TVolatile {
    private static int x = 0;

    static  void add() {
        x++;
    }

    public static void main(String[] args) {
        for (int i = 0; i < 20; i++) {
            new Thread(() -> {
                for (int ii = 0; ii < 1000; ii++) {
                    add();
                }
            }).start();
        }
        while (Thread.activeCount()>2){
            Thread.yield();
        }
        System.out.println(x);
    }
}
```

为了保证原子性，可以在方法上添加Synchronized 、lock锁

另外也可以使用原子类解决原子性问题：

```java

public class TVolatile {
    private static AtomicInteger x = new AtomicInteger();

    static  void add() {
        x.getAndAdd(1);
    }

    public static void main(String[] args) {
        for (int i = 0; i < 20; i++) {
            new Thread(() -> {
                for (int ii = 0; ii < 1000; ii++) {
                    add();
                }
            }).start();
        }
        while (Thread.activeCount()>2){
            Thread.yield();
        }
        System.out.println(x);
    }
}

```

单例模式
---

### 懒汉式

```java
//懒汉式
public class Lazyman {

    public static Lazyman lazyman;
    public static Lazyman getLazyman(){
        return lazyman=new Lazyman();
    }
```

> 高并发下懒汉式会有问题，以下为DCL懒汉式（双重检测锁），但是也有问题

```java
package Thread_T.Single;


//懒汉式
public class Lazyman {

    public static volatile Lazyman lazyman;
    public static Lazyman getLazyman(){
        if (lazyman==null){
            synchronized (Lazyman.class){
                if (lazyman==null){
                    System.out.println(Thread.currentThread().getName());
                    lazyman=new Lazyman();// 问题是：此处不是原子性操作。可能会指令重排，所以要将变量保证禁止指令重排 （+Volatile）
                }
            }
        }
        return lazyman;
    }

    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            new Thread(()->{
                Lazyman.getLazyman();
            }).start();
        }
    }

}

```

## wait()，join()，sleep()

首先需要对wait()，join()，sleep()方法进行介绍。

#### Object.wait()方法是什么？

调用wait()方法前线程必须持有对象Object的锁。线程调用wait()方法后，会释放当前的Object锁，进入锁的monitor对象的等待队列，直到有其他线程调用notify()/notifyAll()方法唤醒等待锁的线程。

需要注意的是，其他线程调用notify()方法只会唤醒单个等待锁的线程，如果有多个线程都在等待这个锁的话，不一定会唤醒到之前调用wait()方法的线程。

同样，调用notifyAll()方法唤醒所有等待锁的线程之后，也不一定会马上把时间片分给刚才放弃锁的那个线程，具体要看系统的调度。

#### Thread.join()方法是什么？

join()方法是Thread类的一个实例方法。它的作用是让当前线程陷入“等待”状态，等join的这个线程threadA执行完成后，再继续执行当前线程。

实现原理是join()方法本身是一个sychronized修饰的方法，也就是调用join()这个方法需要先获取threadA的锁，获得锁之后再调用wait()方法来进行等待，一直到threadA执行完成后，threadA会调用notify_all()方法,唤醒所有等待的线程，当前线程才会结束等待。

```java
Thread threadA = new Thread();
threadA.join();
```

join()方法的源码：

```java
public final void join() throws InterruptedException {
    join(0);//0的话代表没有超时时间一直等下去
}
public final synchronized void join(long millis)
throws InterruptedException {
    long base = System.currentTimeMillis();
    long now = 0;

    if (millis < 0) {
        throw new IllegalArgumentException("timeout value is negative");
    }

    if (millis == 0) {
        while (isAlive()) {
            wait(0);
        }
    } else {
        while (isAlive()) {
            long delay = millis - now;
            if (delay <= 0) {
                break;
            }
            wait(delay);
            now = System.currentTimeMillis() - base;
        }
    }
}
```

这是jvm中Thead的源码，在线程执行结束后会调用notify_all来唤醒等待的线程。

```java
//一个c++函数：
void JavaThread::exit(bool destroy_vm, ExitType exit_type) ；
//里面有一个贼不起眼的一行代码
ensure_join(this);

static void ensure_join(JavaThread* thread) {
  Handle threadObj(thread, thread->threadObj());

  ObjectLocker lock(threadObj, thread);

  thread->clear_pending_exception();

  java_lang_Thread::set_thread_status(threadObj(),        java_lang_Thread::TERMINATED);
  java_lang_Thread::set_thread(threadObj(), NULL);
  //同志们看到了没，别的不用看，就看这一句
  //thread就是当前线程，是啥？就是刚才例子中说的threadA线程
  lock.notify_all(thread);
  thread->clear_pending_exception();
}
```

#### sleep()方法是什么？

sleep方法是Thread类的一个静态方法。它的作用是让当前线程睡眠一段时间。：**sleep方法是不会释放当前线程持有的锁，而wait方法会。**

sleep与wait方法的区别：

- wait可以指定时间，也可以不指定；而sleep必须指定时间。
- wait释放cpu资源，同时释放锁；sleep释放cpu资源，但是不释放锁，所以易死锁。（调用join()方法也不会释放锁）
- wait必须放在同步块或同步方法中，而sleep可以再任意位置。



可重入锁
---

# JAVA8

## lamda

**函数式接口”是指仅仅只包含一个抽象方法,但是可以有多个非抽象方法(也就是上面提到的默认方法)的接口。** 

> 访问局部变量

如果变量没有被final也可以被访问，但是访问的值在后面不能被改变

```java
final int num = 1;
Converter<Integer, String> stringConverter =
        (from) -> String.valueOf(from + num);

stringConverter.convert(2);     // 3


int num = 1;
Converter<Integer, String> stringConverter =
        (from) -> String.valueOf(from + num);

stringConverter.convert(2);     // 3

============以上两种都是可以的，下面这种不允许
    
int num = 1;
Converter<Integer, String> stringConverter =
        (from) -> String.valueOf(from + num);
num = 3;//在lambda表达式中试图修改num同样是不允许的。
```

> 访问实例变量、静态变量

都是可以的

```java
class Lambda4 {
    static int outerStaticNum;
    int outerNum;

    void testScopes() {
        Converter<Integer, String> stringConverter1 = (from) -> {
            outerNum = 23;
            return String.valueOf(from);
        };

        Converter<Integer, String> stringConverter2 = (from) -> {
            outerStaticNum = 72;
            return String.valueOf(from);
        };
    }
}
```

> 无法访问接口中的默认方法



函数式接口
===

```java
!package ThreadTest;

import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

public class Stream {
    public static void main(String[] args) {
         Predicate<String> predicate=(str)->{
             System.out.println("判断型接口");
             return str.isEmpty();
         };
        System.out.println(predicate.test("d"));
        //========================================
        Function function=(str)->{
            System.out.println("函数型接口");
            return str;
        };
        System.out.println(function.apply("asdf"));
        //========================================
        Consumer consumer=(str)->{
            System.out.println("消费型接口");
        };
        consumer.accept("");
        //========================================
        Supplier<Object> supplier=()->{
            System.out.println("供给型接口");
            return "hello";
        };
        System.out.println(supplier.get());
    }

}

```





# Stream

> Stream是对一组元素进行一系列操作序列，分为最终操作和中间操作。中间操作会返回Stream本身，所以可以连续操作。最终操作可以将Stream转换为指定对象

### Map(映射)

中间操作 map 会将元素根据指定的 Function 接口来依次将元素转成另外的对象。

下面的示例展示了将字符串转换为大写字符串。你也可以通过map来将对象转换成其他类型，map返回的Stream类型是根据你map传递进去的函数的返回值决定的。

```
        // 测试 Map 操作
        stringList
                .stream()
                .map(String::toUpperCase)
                .sorted((a, b) -> b.compareTo(a))
                .forEach(System.out::println);// "DDD2", "DDD1", "CCC", "BBB3", "BBB2", "AAA2", "AAA1"
```

### Match(匹配)

Stream提供了多种匹配操作，允许检测指定的Predicate是否匹配整个Stream。所有的匹配操作都是 **最终操作** ，并返回一个 boolean 类型的值。

```java
        // 测试 Match (匹配)操作
        boolean anyStartsWithA =
                stringList
                        .stream()
                        .anyMatch((s) -> s.startsWith("a"));
        System.out.println(anyStartsWithA);      // true

        boolean allStartsWithA =
                stringList
                        .stream()
                        .allMatch((s) -> s.startsWith("a"));

        System.out.println(allStartsWithA);      // false

        boolean noneStartsWithZ =
                stringList
                        .stream()
                        .noneMatch((s) -> s.startsWith("z"));

        System.out.println(noneStartsWithZ);      // true
```

### Count(计数)

计数是一个 **最终操作**，返回Stream中元素的个数，**返回值类型是 long**。

```java
      //测试 Count (计数)操作
        long startsWithB =
                stringList
                        .stream()
                        .filter((s) -> s.startsWith("b"))
                        .count();
        System.out.println(startsWithB);    // 3
```

### Reduce(规约)

这是一个 **最终操作** ，允许通过指定的函数来将stream中的多个元素规约为一个元素，规约后的结果是通过Optional 接口表示的：

```java
        //测试 Reduce (规约)操作
        Optional<String> reduced =
                stringList
                        .stream()
                        .sorted()
                        .reduce((s1, s2) -> s1 + "#" + s2);

        reduced.ifPresent(System.out::println);//aaa1#aaa2#bbb1#bbb2#bbb3#ccc#ddd1#ddd2
```

这个方法的主要作用是把 Stream 元素组合起来。它提供一个起始值（种子），然后依照运算规则（BinaryOperator），和前面 Stream 的第一个、第二个、第 n 个元素组合。从这个意义上说，字符串拼接、数值的 sum、min、max、average 都是特殊的 reduce。例如 Stream 的 sum 就相当于`Integer sum = integers.reduce(0, (a, b) -> a+b);`也有没有起始值的情况，这时会把 Stream 的前面两个元素组合起来，返回的是 Optional。

```java
// 字符串连接，concat = "ABCD"
String concat = Stream.of("A", "B", "C", "D").reduce("", String::concat); 
// 求最小值，minValue = -3.0
double minValue = Stream.of(-1.5, 1.0, -3.0, -2.0).reduce(Double.MAX_VALUE, Double::min); 
// 求和，sumValue = 10, 有起始值
int sumValue = Stream.of(1, 2, 3, 4).reduce(0, Integer::sum);
// 求和，sumValue = 10, 无起始值
sumValue = Stream.of(1, 2, 3, 4).reduce(Integer::sum).get();
// 过滤，字符串连接，concat = "ace"
concat = Stream.of("a", "B", "c", "D", "e", "F").
 filter(x -> x.compareTo("Z") > 0).
 reduce("", String::concat);
```

上面代码例如第一个示例的 reduce()，第一个参数（空白字符）即为起始值，第二个参数（String::concat）为 BinaryOperator。这类有起始值的 reduce() 都返回具体的对象。而对于第四个示例没有起始值的 reduce()，由于可能没有足够的元素，返回的是 Optional，请留意这个区别。

# Optional



```java
//of（）：为非null的值创建一个Optional
Optional<String> optional = Optional.of("bam");
// isPresent（）： 如果值存在返回true，否则返回false
optional.isPresent();           // true
//get()：如果Optional有值则将其返回，否则抛出NoSuchElementException
optional.get();                 // "bam"
//orElse（）：如果有值则将其返回，否则返回指定的其它值
optional.orElse("fallback");    // "bam"
//ifPresent（）：如果Optional实例有值则为其调用consumer，否则不做处理
optional.ifPresent((s) -> System.out.println(s.charAt(0)));     // "b"
```

```java
Optional optional=OptionalTest();//调用方法得到容器
optional.ifPresent(x-> System.out.println(x)); //即使为空也不需要进行判断，不会出现异常。为空不执行
optional.get() //可能会出现NoSuchElementException异常


private Optional OptionalTest() {
    // return Optional.of(new String("cxzczv")); 创建新的非空容器（必须添加数据），向容器中添加数据，并返回
    //return null; 但是直接返回null会空指针异常
    //return Optional.ofNullable("null"); //既可以为空又可以不为空
      return Optional.empty(); //创建新的空容器 ，不会空指针异常
}
```

`类名 :: 方法名`是 Java 8 引入的语法，方法名后面是没有 `()` 的，表明该方法并不一定会被调用。

```java
  	String name = null;
    System.out.println("orElse");
    String name2 = Optional.ofNullable(name).orElse(getDefaultValue()); //为空时使用默认值orElse()中的；

    System.out.println("orElseGet");
    String name3 = Optional.ofNullable(name).orElseGet(OrElseOptionalDemo::getDefaultValue);//为空执行表达式OrElseOptionalDemo::getDefaultValue。可以结合:: 取值 
}
```

```
		List<String> list=new ArrayList<>();
        list.add("22222");
        list.add("11111");
        Optional<String> reduce = list.stream().reduce((a,b) -> a+b);
        String xgw = reduce.orElse("xgw");
        System.out.println(xgw);
```



==可以通过orElseGet、orElse方法从容器中取值，不会报异常==

> stream中的方法负责计算
>
> 

> > > 得到






---