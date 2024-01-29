

# 常用api

| **Object**           | **LocalTime**     | **Set**             | **FileOutputStream**    | **Properties**             |
| -------------------- | ----------------- | ------------------- | ----------------------- | -------------------------- |
| **objects**          | **LocalDateTime** | **HashSet**         | **Reader**              | **Thread**                 |
| **Integer**          | **Duration**      | **LinkedHashSet**   | **FileReader**          | **Runnable**               |
| **StringBuilder**    | **Period**        | **TreeSet**         | **Writer**              | **Callable**               |
| **StringBuffer**     | **ZoneId**        | Map                 | **FileWriter**          | **ExecutorService**        |
| **Math**             | **ZonedDateTime** | **HashMap**         | **BufferdInputStream**  | **ThreadPoo****lExecutor** |
| **System**           | **Arrays**        | **LinkedHashMap**   | **BufferdOutputStream** | **Socket**                 |
| **Runtime**          | **Comparable**    | **TreeMap**         | **BufferedReader**      | **ServerSocket**           |
| **BigDecimal**       | **Comparator**    | Iterator            | **BufferedWriter**      | **Class**                  |
| **Date**             | **Collection**    | **Stream**          | **PrintStream**         | **Method**                 |
| **SimpleDateFormat** | **List**          | **InputStream**     | **PrintWriter**         | **Constructor**            |
| **Calendar**         | **ArrayList**     | **FileInputStream** | **ObjectInputStream**   | **Field**                  |
| **LocalDate**        | **LinkedList**    | **OutputStream**    | **ObjectOutputStream**  | **Proxy ...**              |





## Object

**Object类常见方法**

| 方法名                          | 说明                       |
| ------------------------------- | -------------------------- |
| public String toString()        | 返回对象的字符串表示形式。 |
| public boolean equals(Object o) | 判断两个对象是否相等。     |
| protected Object clone()        | 对象克隆                   |

### toString

```Java
public String toString()	//默认是返回当前对象的地址信息。

2、Student s  = new Student("张三",'女', 23);
System.out.println(s.toString());	//返回对象地址
System.out.println(s);	//直接输出对象名，默认是调用toString方法的
```

**toString存在的意思：**

​		默认返回对象的地址其实是没有意义的

​			**真实存在的意义是被子类重写，以便返回子类对象的内容。**

### equals

```Java
1、public boolean equals(Object o )	//默认是比较2个对象的地址是否一样，返回true 或者false
```

**equals存在的意义**

​		默认比较对象的地址其实是没有意义的，因为== 号可以更简单的完成

​			**存在的的真实意义是被子类重写，以便比较对象的内容。**





## Objects

**Objects 的常见方法**

| 方法名                                            | 说明                                           |
| ------------------------------------------------- | ---------------------------------------------- |
| public  static boolean equals(Object a, Object b) | 先做非空判断，再比较两个对象                   |
| public  static boolean isNull(Object obj)         | 判断对象是否为null，为null返回true ,反之       |
| public  static boolean nonNull(Object obj)        | 判断对象是否不为null，不为null则返回true, 反之 |

**Objects是一个工具类，提供了更安全的方式比较2个对象。**

```Java
Student  s = null;
s.equals(s2);	//空指针异常 
Objects.equals(s, s2);   //返回false
```

```java 
public static boolean equals(Object a, Object b)	//比较两个对象的，底层会先进行非空判断，从而可以避免空指针异常。在进行equals比较

    public static Boolean isNull(Object obj)		//判断变量是否为null，为null返回true，反之
    
    源码分析
    public static Boolean equals(Object a ,Object b){
    	return (a == b) || (a != null && a.equals(b));
}
```





## 包装类

| **基本数据类型** | **对应的包装类（引用数据类型）** |
| ---------------- | -------------------------------- |
| byte             | Byte                             |
| short            | Short                            |
| int              | Integer                          |
| long             | Long                             |
| char             | Character                        |
| float            | Float                            |
| double           | Double                           |
| boolean          | Boolean                          |

| **基本类型的数据包装成对象的方案**                           |
| ------------------------------------------------------------ |
| public Integer(int value)：**已过时**                        |
| public static Integer **valueOf**(int **i**)   //**推荐使用这个，就不用记那么多了** |

**自动装箱：**基本数据类型可以自动转换为包装类型。

**自动拆箱：**包装类型可以自动转换为基本数据类型。

```Java
// 泛型和集合不支持基本数据类型，只能支持引用数据类型。
// ArrayList<int> list = new ArrayList<>();
ArrayList<Integer> list = new ArrayList<>();
list.add(12); // 自动装箱
list.add(13); // 自动装箱
```

​		l**可以把基本类型的数据转换成字符串类型。**

| public static String toString(double d) |
| --------------------------------------- |
| public String **toString**()            |

​		l**可以把字符串类型的数值转换成真实的数据类型。**

| public static int parseInt(String s)        |
| ------------------------------------------- |
| public static Integer **valueOf**(String s) |





## StringBuilder  、StringBuffer

**StringBuilder称为可变字符串容器，操作字符串的性能由于String类。**

| 构造器                               | 说明                                           |
| ------------------------------------ | ---------------------------------------------- |
| public **StringBuilder**()           | 创建一个空白的可变的字符串对象，不包含任何内容 |
| public **StringBuilder**(String str) | 创建一个指定字符串内容的可变字符串对象         |

| 方法名称                                  | 说明                                                |
| ----------------------------------------- | --------------------------------------------------- |
| public StringBuilder **append**(任意类型) | 添加数据并返回StringBuilder对象本身                 |
| public StringBuilder **reverse**()        | 将对象的内容反转                                    |
| public int **length**()                   | 返回对象内容长度                                    |
| public String **toString**()              | 通过toString()就可以实现把StringBuilder转换为String |

**注意：**

​		StringBuffer**的用法与** **StringBuilder是一模一样的**

​		**但StringBuilder是线程不安全的StringBuffer是线程安全的**

```java 
StringBuilder 构造器
    
	public  StringBuilder()		//创建一个空白可变的字符串对象，不包含任何内容
	public StringBuilder(String str)		//创建一个指定字符串内容的可变字符串对象
    
StringBuilder 常用方法
    
    public StringBuilder append (任意类型)		//添加数据并返回StringBuilder对象本身
    public StringBuilder reverse()			//将对象的内容反转
    public int length()						//返回对象内容长度
    public String toString()			//通过toString()就可以实现把StringBuilder转换为String
```

​		**StringBuilder拼接操作字符串的手段：性能好**

​			**String才是结果数据的类型：目的**

**StringBuilder代表可变字符串对象**，相当于是一个容器，它里面装的字符串是可以改变的，就是用来操作字符串的。

**好处**：StringBuilder比String更适合做字符串的修改操作，效率会更高，代码也会更简洁。



## StringJoiner

​		JDK8开始才有的，跟StringBuilder一样，也是用来操作字符串的，也可以看成是一个容器，创建之后里面的内容是可变的。

​		好处：不仅能提高字符串的操作效率，并且在有些场景下使用它操作字符串，代码会更简洁

| 构造器                                                 | 说明                                                         |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| public **StringJoiner (间隔符号)**                     | 创建一个StringJoiner对象，指定拼接时的间隔符号               |
| public **StringJoiner (间隔符号，开始符号，结束符号)** | 创建一个StringJoiner对象，指定拼接时的间隔符号、开始符号、结束符号 |

| 方法名称                                  | 说明                                         |
| ----------------------------------------- | -------------------------------------------- |
| public  StringJoiner **add** (添加的内容) | 添加数据，并返回对象本身                     |
| public int  **length**()                  | 返回长度 ( 字符出现的个数)                   |
| public  String **toString**()             | 返回一个字符串（该字符串就是拼接之后的结果） |



## Math

**数学操作类，提供的都是一些静态方法，用于完成数学计算的。**

| 方法名                                          | 说明                                  |
| ----------------------------------------------- | ------------------------------------- |
| public static int **abs**(int a)                | 获取参数绝对值                        |
| public static double  **ceil**(double a)        | 向上取整                              |
| public static double  **floor**(double a)       | 向下取整                              |
| public static int **round**(float a)            | 四舍五入                              |
| public static int **max**(int a,int b)          | 获取两个int值中的较大值               |
| public static double **pow**(double a,double b) | 返回a的b次幂的值                      |
| public static double **random**()               | 返回值为double的随机值，范围[0.0,1.0) |



```Java
// 目标：看看Math类的方法就行了。
        // 1、取绝对值（拿到的结果一定是正数）
        System.out.println(Math.abs(-12));    // 12
        System.out.println(Math.abs(-12.2)); // 12.2
        System.out.println(Math.abs(1443));  // 1443

        // 2、向上取整
        System.out.println(Math.ceil(3.000001)); // 4.0
        System.out.println(Math.ceil(4.0)); // 4.0

        // 3、向下取整
        System.out.println(Math.floor(3.9999999)); // 3.0
        System.out.println(Math.floor(3.0)); // 3.0

        // 4、四舍五入
        System.out.println(Math.round(3.45555)); // 3
        System.out.println(Math.round(3.500001)); // 4

        // 5、取较大值
        System.out.println(Math.max(10, 20));  // 20

        // 6、取次方
        System.out.println(Math.pow(2, 4)); // 2^4 == 16.0
        System.out.println(Math.pow(3, 2)); // 3^2 == 9.0

        // 7、取随机数（用的少）
        System.out.println(Math.random()); // [0.0 - 1.0)
```





## System

**作用：代表系统类，提供的都是一些静态方法，用于操作系统相关的信息的。**

| 方法名                                      | 说明                         |
| ------------------------------------------- | ---------------------------- |
| public  static void **exit**(int status)    | 终止当前运行的Java虚拟机。   |
| public  static long **currentTimeMillis**() | 返回当前系统的时间毫秒值形式 |

```Java
   // 目标：了解下System类的几个方法。
        // 1、获取系统的全部信息
        // public static long currentTimeMillis();（重点）
        // 获取当前系统的时间毫秒值（从1970-1-1 00:00:00 走到此刻总的毫秒值）
        long time = System.currentTimeMillis(); // 做性能分析，做时间运算！
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss EEE a");
        System.out.println(sdf.format(time));

        // 2、获取系统全部属性信息
        Properties properties = System.getProperties();
        System.out.println(properties);

        // 3、干掉JVM虚拟机（程序全部死亡了，不要用，跟删库跑路一个性质~~）
        // System.exit(0); // 0是正常终止！

        // 4、进行数组拷贝（了解）
        int[] arr1 = {10, 20, 30, 40, 50, 60, 70, 80};
        int[] arr2 = new int[6]; // arr2 = [0, 0, 0, 0, 0, 0] ==> [0, 0, 50, 60, 70, 0]
     /*   arraycopy(Object src,int  srcPos, Object dest, int destPos,int length)
          参数一：原数组
          参数二：从哪个索引位置开始拷贝
          参数三：目标数组
          参数四：目标数组粘贴元素的起始索引位置。
          参数五：拷贝几个元素
        */
        System.arraycopy(arr1, 4, arr2, 2, 3);
        System.out.println(Arrays.toString(arr2));

        System.out.println("程序结束。。。。");
```



### Runtime

| 方法名                                  | 说明                                   |
| --------------------------------------- | -------------------------------------- |
| public  static **Runtime** getRuntime() | 返回与当前Java应用程序关联的运行时对象 |
| public void **exit**(int status)        | 终止当前运行的虚拟机                   |
| public int **availableProcessors**()    | 返回Java虚拟机可用的处理器数。         |
| public long **totalMemory**()           | 返回Java虚拟机中的内存总量             |
| public long **freeMemory**()            | 返回Java虚拟机中的可用内存             |
| public **Process exec**(String command) | 启动某个程序，并返回代表该程序的对象   |



## BigDecimal

**封装大数据（Double）完成一些精度运算的。**

​	为什么要用BigDecimal

​		因为double类型的数据运算会出现失真：0.1 + 0.2 ==0.30000000000000004....

​		BigDecimal可以解决精度失真问题

**DigDecaimal第一步：封装浮点型数据成为BigDecimal对象**

```Java
  // 1、调用BigDecimal的方法，封装浮点型数据成为大数据对象
        //  public static BigDecimal valueOf(double val)
        BigDecimal a1 = BigDecimal.valueOf(a);
        BigDecimal b1 = BigDecimal.valueOf(b);
```

**DigDecaimal第二步**		调用功能进行运算

```Java
public BigDecaimal add (BigDecaimal b)	//加法
public BigDecaimal subtract (BigDecaimal b)	//减法
public BigDecaimal multiply (BigDecaimal b)	//乘法
public BigDecaimal divide (BigDecaimal b)	//除法
public BigDecaimal divide(另一个BigDecaimal对象,精确到几位，舍入模式 )
```

```Java
        // BigDecimal是解决精度问题的手段。
        // double才是开发的目的。
        // public double doubleValue(): 把BigDecimal又转回成double
        double m2 = c1.doubleValue();
        System.out.println(m2);
```



| **构造器**                                                 | **说明**                   |
| ---------------------------------------------------------- | -------------------------- |
| public **BigDecimal**(double val) **注意：不推荐使用这个** | 将 double转换为 BigDecimal |
| public **BigDecimal**(String val)                          | 把String转成BigDecimal     |

| **方法名**                                                   | **说明**                     |
| ------------------------------------------------------------ | ---------------------------- |
| public static BigDecimal **valueOf**(double val)             | 转换一个 double成 BigDecimal |
| public BigDecimal **add**(BigDecimal b)                      | 加法                         |
| public BigDecimal **subtract**(BigDecimal b)                 | 减法                         |
| public BigDecimal **multiply**(BigDecimal b)                 | 乘法                         |
| public BigDecimal **divide**(BigDecimal b)                   | 除法                         |
| public BigDecimal **divide** (另一个BigDecimal对象，精确几位，舍入模式) | 除法、可以控制精确到小数几位 |
| public double **doubleValue**()                              | 将BigDecimal转换为double     |



## JDK8 前的 日期与时间

### Date

**作用：代表当前此刻日期和时间的。**

| 构造器                     | 说明                                             |
| -------------------------- | ------------------------------------------------ |
| public **Date**()          | 创建一个Date对象，代表的是系统当前此刻日期时间。 |
| public **Date**(long time) | 把时间毫秒值转换成Date日期对象。                 |

| 常见方法                           | 说明                                              |
| ---------------------------------- | ------------------------------------------------- |
| public long **getTime**()          | 返回从1970年1月1日   00:00:00走到此刻的总的毫秒数 |
| public void **setTime**(long time) | 设置日期对象的时间为当前时间毫秒值对应的时间      |

​	构建对象

```java 
Date d = new Date();		//public Date();
long time = d.getTime();	//public long getTime() : 获取时间毫秒值：从1970-1-1 00:00:00开始走到此刻的总毫秒数
public Date(long time)
Date d2 = new Date(time);	//把时间毫秒值转换成日期对象。
public void setTime(long time): //设计日期对象为当前时间毫秒值对应的日期。
```



### SimpleDateFormat	（jdk8 以后会用DateTimeFormatter 代替）

**作用：格式化、解析时间的**

| 常见构造器                                   | 说明                                     |
| -------------------------------------- | ---------------------------------------- |
| public **SimpleDateFormat**(String  pattern) | 创建简单日期格式化对象，并封装时间的格式 |

| 格式化时间的方法                               | 说明                              |
| ---------------------------------------------- | --------------------------------- |
| public final String **format** **(Date date)** | 将日期格式化成日期/时间字符串     |
| public final String **format**(Object time)    | 将时间毫秒值式化成日期/时间字符串 |

| 解析方法                             | 说明                       |
| ------------------------------------ | -------------------------- |
| public Date **parse(String source)** | 把字符串时间解析成日期对象 |

​		代码案例：

```Java
构建对象：public SimpleDateFormat(String pattern)
	public String format(Date d)	//格式化日期对象
	public String format(Object o)	//格式化时间毫秒值
	public Date parse(String date):	//把字符串时间解析成日期对象
```

```Java
        // 目标：掌握简单日期格式化类：SimpleDateFormat的使用。
        // 1、创建一个简单日期格式化对象：封装时间格式。
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss EEE a");

        // 2、创建日期对象
        Date d = new Date();
        System.out.println(d);

        // 3、开始使用简单日期格式化对象负责格式化日期成为我们喜欢的字符串时间形式
        String rs = sdf.format(d);
        System.out.println(rs);

        // 4、可以格式化时间毫秒值的哦
        long time = d.getTime() + 121 * 1000;
        System.out.println(sdf.format(time));
```

```Java
public class SimpleDateFormatDemo2 {
    public static void main(String[] args) throws ParseException {
        // 目标2：掌握简单日期格式化的解析操作。
        // 需要：把字符串时间解析成日期对象
        String dateStr = "2022-11-11 11:11:12";
        // 1、创建简单日期格式化对象。
        // 注意、注意、注意: 解析时间的格式必须与被解析时间的格式一模一样，否则报错！
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

        // 2、开始解析了(会报错的，把异常抛出去，什么意思，后面会讲的)
        Date d = sdf.parse(dateStr);
        System.out.println(d);
    }
}
```



### Calendar		是可变对象

**作用：代表日历，获取信更丰富**

​		**通过它可以单独获取，修改时间中的年、月、日、时、分、秒 等。**

| 方法名                                    | 说明                        |
| ----------------------------------------- | --------------------------- |
| public  static Calendar **getInstance**() | 获取当前日历对象            |
| public int **get(int field)**             | 获取日历中的某个信息。      |
| public final Date **getTime()**           | 获取日期对象。              |
| public long **getTimeInMillis()**         | 获取时间毫秒值              |
| public void **set(int field,int value)**  | 修改日历的某个信息。        |
| public void **add(int field,int amount)** | 为某个信息增加/减少指定的值 |

```Java
创建对象  
// 目标：掌握日历类的使用。
        // 1、得到日历对象
        Calendar c = Calendar.getInstance();
        System.out.println(c);

        // 2、获取信息：public int get(int field):
        int year = c.get(Calendar.YEAR);
        System.out.println(year);

        int days = c.get(Calendar.DAY_OF_YEAR);
        System.out.println(days);

        // 3、获取日期对象（了解）
        Date d = c.getTime();
        System.out.println(d);

        // 4、时间毫秒值（了解）
        long time = c.getTimeInMillis();
        System.out.println(time);

        // 5、修改日历的时间（需求：问89天后是什么日子）
        // 参数一：信息字段：一年中的第几天
        // 参数二：往后加多少天。
        c.add(Calendar.DAY_OF_YEAR, 89);
        Date d1 = c.getTime();
        System.out.println(d1);

        c.set(Calendar.DAY_OF_YEAR, 364); // 直接修改日历到某一天！
        Date d2 = c.getTime();
        System.out.println(d2);
```

​		**注意：** **calendar**  **是可变对象，一旦修改后其对象本身表示的时间将产生变化。**

## JDK 8 后新增加的时间api

Tip:

1秒=1000毫秒；

1毫秒=1000微秒；

1微秒=1000纳秒；

**代替Calender**

## LocalDate   LocalTime  LocalDateTime

**LocalDate：代表本地日期 (年、月、日、星期 )**

**LocalTime：代表本地时间(时、分、秒、纳秒)**

**LocalDateTime：代表本地日期、时间(年、月、日、星期、时、分、秒、纳秒)**

| 方法名                                                     | 示例                                                         |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| public static Xxxx **now**(): 获取系统当前时间对应的该对象 | **LocaDate** ld = LocalDate.now(); <br />**LocalTime** lt = LocalTime.now(); <br />**LocalDateTime** ldt = LocalDateTime.now(); |
| public static Xxxx **of**(…)：获取指定时间的对象           | **LocalDate** localDate1 = LocalDate.of(2099 , 11,11);<br /> **LocalTime** localTime1 = LocalTime.of(9, 8, 59);<br /> **LocalDateTime** localDateTime1 = LocalDateTime.of(2025, 11, 16, 14, 30, 01); |

#### 	**LocalDate的常用API（都是处理年、月、日、星期相关的）。**

| **方法名**                              | **说明**                                     |
| --------------------------------------- | -------------------------------------------- |
| public int **geYear**()                 | 获取年                                       |
| public int **getMonthValue**()          | 获取月份（1-12）                             |
| public int **getDayOfMonth**()          | 获取日                                       |
| public int **getDayOfYear**()           | 获取当前是一年中的第几天                     |
| Public **DayOfWeek** **getDayOfWeek**() | 获取星期几：**ld.getDayOfWeek().getValue()** |

| **方法名**                                             | **说明**                                 |
| ------------------------------------------------------ | ---------------------------------------- |
| **withYear、withMonth、withDayOfMonth、withDayOfYear** | 直接**修改**某个信息，**返回新日期对象** |
| **plusYears、plusMonths、plusDays、plusWeeks**         | 把某个信息**加多少**，**返回新日期对象** |
| **minusYears、minusMonths、minusDays，minusWeeks**     | 把某个信息**减多少**，**返回新日期对象** |
| equals **isBefore isAfter**                            | 判断两个日期对象，是否相等，在前还是在后 |



#### 	**LocalTime的常用API（都是处理时、分、秒、纳秒相关的）。**

| **方法名**                 | **说明** |
| -------------------------- | -------- |
| public int **getHour**()   | 获取小时 |
| public int **getMinute**() | 获取分   |
| public int **getSecond**() | 获取秒   |
| public int **getNano**()   | 获取纳秒 |

| **方法名**                                             | **说明**                                |
| ------------------------------------------------------ | --------------------------------------- |
| **withHour、withMinute、withSecond、withNano**         | **修改时间，返回新时间对象**            |
| **plusHours、plusMinutes、plusSeconds、plusNanos**     | 把某个信息**加多少，返回新时间对象**    |
| **minusHours、minusMinutes、minusSeconds、minusNanos** | 把某个信息**减多少，返回新时间对象**    |
| equals **isBefore isAfter**                            | 判断2个时间对象，是否相等，在前还是在后 |



#### 		**LocalDateTime的常用API（可以处理年、月、日、星期、时、分、秒、纳秒等信息）**

| **方法名**                                                   | **说明**                                 |
| ------------------------------------------------------------ | ---------------------------------------- |
| **getYear、getMonthValue、getDayOfMonth、getDayOfYear  getDayOfWeek、getHour、getMinute、getSecond、getNano** | **获取年月日、时分秒、纳秒等**           |
| **withYear、withMonth、withDayOfMonth、withDayOfYear  withHour、withMinute、withSecond、withNano** | **修改某个信息，返回新日期时间对象**     |
| **plusYears、plusMonths、plusDays、plusWeeks  plusHours、plusMinutes、plusSeconds、plusNanos** | **把某个信息加多少，返回新日期时间对象** |
| **minusYears、minusMonths、minusDays、minusWeeks  minusHours、minusMinutes、minusSeconds、minusNanos** | **把某个信息减多少，返回新日期时间对象** |
| equals **isBefore isAfter**                                  | 判断2个时间对象，是否相等，在前还是在后  |



​		**LocalDateTime的转换成LocalDate、LocalTime**

| 方法名                              | 说明                        |
| ----------------------------------- | --------------------------- |
| public **LocalDate toLocalDate()**  | 转换成一个**LocalDate对象** |
| public  **LocalTime toLocalTime()** | 转换成一个**LocalTime对象** |

### ZoneId   ：时区id

​	**ZoneId 时区的常见方法**

| 方法名                                               | 说明                     |
| ---------------------------------------------------- | ------------------------ |
| public static **Set<String>  getAvailableZoneIds()** | 获取Java中支持的所有时区 |
| public static **ZoneId systemDefault()**             | 获取系统默认时区         |
| public static **ZoneId of(String zoneId)**           | 获取一个指定时区         |

​	**ZonedDateTime  带时区的时间  常见方法**

| 方法名                                                       | 说明                            |
| ------------------------------------------------------------ | ------------------------------- |
| public static **ZonedDateTime now()**                        | 获取当前时区的ZonedDateTime对象 |
| public static **ZonedDateTime now(ZoneId zone)**             | 获取指定时区的ZonedDateTime对象 |
| **getYear、getMonthValue、getDayOfMonth、getDayOfYeargetDayOfWeek、getHour、getMinute、getSecond、getNano** | 获取年月日、时分秒、纳秒等      |
| public **ZonedDateTime withXxx(时间)**                       | 修改时间系列的方法              |
| public **ZonedDateTime minusXxx(时间)**                      | 减少时间系列的方法              |
| public **ZonedDateTime plusXxx(时间)**                       | 增加时间系列的方法              |





**代替 Date**

### Instant	时间线上的某个时刻/时间戳（代替Date）

​		**通过获取Instant的对象可以拿到此刻的时间，该时间由两部分组成：从1970-01-01 00:00:00 开始走到此刻的总秒数 + 不够1秒的纳秒数**

| 方法名                                  | 说明                                        |
| --------------------------------------- | ------------------------------------------- |
| public static Instant now()             | 获取当前时间的Instant对象（标准时间）       |
| public long **getEpochSecond()**        | 获取从1970-01-01T00：00：00开始记录的秒数。 |
| public int **getNano()**                | 从时间线开始，获取从第二个开始的纳秒数      |
| **plusMillis plusSeconds plusNanos**    | 判断系列的方法                              |
| **minusMillis minusSeconds minusNanos** | 减少时间系列的方法                          |
| equals、**isBefore、isAfter**           | 增加时间系列的方法                          |

​		**作用：可以用来记录代码的执行时间，或用于记录用户操作某个事件的时间点。**

​	**传统的Date类，只能精确到毫秒，并且是可变对象；**

​	**新增的Instant类，可以精确到纳秒，并且是不可变对象，推荐用Instant代替Date。**

### DateTimeFormatter ：格式化器，用于时间的格式化、解析（线程安全）（代替SimpleDateFormattat 【线程不安全】）

#### 新增补充  Period （一段时期）  Duration（持续时间）

​		**Period（一段时期）**

* 可以用于计算两个 LocalDate对象 相差的年数、月数、天数。

| 方法名                                                       | 说明                            |
| ------------------------------------------------------------ | ------------------------------- |
| public static **Period between**(**LocalDate** start, **LocalDate** end) | 传入2个日期对象，得到Period对象 |
| public  int **getYears**()                                   | 计算隔几年，并返回              |
| public  int **getMonths**()                                  | 计算隔几个月，年返回            |
| public  int **getDays**()                                    | 计算隔多少天，并返回            |

​		**Duration（持续时间）**

* 可以用于计算两个时间对象相差的天数、小时数、分数、秒数、纳秒数；支持LocalTime、LocalDateTime、Instant等时间。

| 方法名                                                       | 说明                              |
| ------------------------------------------------------------ | --------------------------------- |
| public  static Duration between(开始时间对象1,截止时间对象2) | 传入2个时间对象，得到Duration对象 |
| public  long **toDays**()                                    | 计算隔多少天，并返回              |
| public  long **toHours**()                                   | 计算隔多少小时，并返回            |
| public  long **toMinutes**()                                 | 计算隔多少分，并返回              |
| public  long **toSeconds**()                                 | 计算隔多少秒，并返回              |
| public  long **toMillis**()                                  | 计算隔多少毫秒，并返回            |
| public  long **toNanos**()                                   | 计算隔多少纳秒，并返回            |

## 





## Arrays 

* **用来操作数组的一个工具类**

**Arrays类提供的的常见方法**

| **方法名**                                                   | **说明**                       |
| ------------------------------------------------------------ | ------------------------------ |
| public static String **toString**(类型[] arr)                | 返回数组的内容                 |
| public static int[] **copyOfRange**(类型[] arr, 起始索引, 结束索引) | 拷贝数组（指定范围）           |
| public static **copyOf**(类型[] arr,  int newLength)         | 拷贝数组                       |
| public static **setAll**(double[] array,   **IntToDoubleFunction** generator) | 把数组中的原数据改为新数据     |
| public  static void **sort**(类型[] arr)                     | 对数组进行排序(默认是升序排序) |

代码案例

```Java
public static void main(String[] args) {
    // 1、public static String toString(类型[] arr): 返回数组的内容
    int[] arr = {10, 20, 30, 40, 50, 60};
    System.out.println(Arrays.toString(arr));

    // 2、public static 类型[] copyOfRange(类型[] arr, 起始索引, 结束索引) ：拷贝数组（指定范围，包前不包后）
    int[] arr2 = Arrays.copyOfRange(arr, 1, 4);
    System.out.println(Arrays.toString(arr2));

    // 3、public static copyOf(类型[] arr, int newLength)：拷贝数组，可以指定新数组的长度。
    int[] arr3 = Arrays.copyOf(arr, 10);
    System.out.println(Arrays.toString(arr3));

    // 4、public static setAll(double[] array, IntToDoubleFunction generator)：把数组中的原数据改为新数据又存进去。
    double[] prices = {99.8, 128, 100};
    //                  0     1    2
    // 把所有的价格都打八折，然后又存进去。
    Arrays.setAll(prices, new IntToDoubleFunction() {
        @Override
        public double applyAsDouble(int value) {
            // value = 0  1  2
            return prices[value] * 0.8;
        }
    });
    System.out.println(Arrays.toString(prices));

    // 5、public static void sort(类型[] arr)：对数组进行排序(默认是升序排序)
    Arrays.sort(prices);
    System.out.println(Arrays.toString(prices));
}
```

**对数组中的数据进行排序**

```java 
double[] pricer = {99.8, 128, 100};
Arrays.sort(prices);
System.out.println(Arrays.toString(peices)); //[99.8, 100.0, 128.0]
```



**如果数组中存储的是对象，如何排序？**

```java 
Student[] students = new Student[4];
students[0] = new Student("蜘蛛精", 169.5, 23);
students[1] = new Student("紫霞", 163.8, 26);
students[2] = new Student("紫霞", 163.8, 26);
students[3] = new Student("至尊包", 167.5, 24);
```

* **方式一：**让该对象的类实现Comparable(比较规则)接口，然后重写compareTo方法，自己来制定比较规则。
* **方式二：**使用下面这个sort方法，创建Comparator比较器接口的匿名内部类对象，然后自己制定比较规则。

| public static <T> void  sort(T[] arr,  Comparator<? super T> c) | 对数组进行排序(支持自定义排序规则） |
| ------------------------------------------------------------ | ----------------------------------- |
|                                                              |                                     |

​		**自定义排序规则时，需要遵循的官方约定如下**

**升序**

如果认为左边对象 **大于** 右边对象 应该**返回正整数**

如果认为左边对象 **小于** 右边对象 应该**返回负整数**

如果认为左边对象 **等于** 右边对象 应该**返回0整数**

```Java
Arrays.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                // 制定比较规则了：左边对象 o1   右边对象 o2
                // 约定1：认为左边对象 大于 右边对象 请您返回正整数
                // 约定2：认为左边对象 小于 右边对象 请您返回负整数
                // 约定3：认为左边对象 等于 右边对象 请您一定返回0
//                if(o1.getHeight() > o2.getHeight()){
//                    return 1;
//                }else if(o1.getHeight() < o2.getHeight()){
//                    return -1;
//                }
//                return 0; // 升序
                 return Double.compare(o1.getHeight(), o2.getHeight()); // 升序
                // return Double.compare(o2.getHeight(), o1.getHeight()); // 降序
            }
        });
        System.out.println(Arrays.toString(students));
```

