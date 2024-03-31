# 一、前置知识：字符集

**标准ASCI字符集**

+ ASCII(American Standard Code for Information Interchange)： 美国信息交换标准代码，包括了英文、符号等。（二进制首位都是0）

**GBK（汉字内码扩展规范，国标）**

+ 汉字编码字符集，包含了2万多个汉字等字符，GBK中一个中文字符编码成两个字节的形式存储。

+ 注意：GBK兼容了ASCII字符集。（汉字的二进制的第一字节首位为1）

**UTF-8**

+ 是Unicode字符集的一种编码方案，采取可变长编码方案，共分四个长度区：1个字节，2个字节，3个字节，4个字节
+ **英文字符、数字等只占1个字节（兼容标准ASCII编码），汉字字符占用3个字节。**

| **UTF-8编码方式(二进制)**                           |
| --------------------------------------------------- |
| **0**xxxxxxx （ASCII码）                            |
| **110**xxxxx **10**xxxxxx                           |
| **1110**xxxx **10**xxxxxx **10**xxxxxx              |
| **11110**xxx **10**xxxxxx **10**xxxxxx **10**xxxxxx |

**注意一：**字符码时使用的字符集，和解码时使用的字符集必须一致，**否则会出现乱码。**

**注意二：**英文数字一般不会乱码，因为很多字符集都兼容了ASCII编码



## 1、Java代码完成对字符的编码

| **String提供了如下方法**                | 说明                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| byte[] **getBytes()**                   | 使用平台的默认字符集将该 String编码为一系列字节，将结果存储到新的字节数组中 |
| byte[] **getBytes(String charsetName)** | 使用指定的字符集将该 String编码为一系列字节，将结果存储到新的字节数组中 |



```Java
//1.编码
	String data = "a我b";
	byte[] bytes = data.getBytes();//默认是按照平台字符集(UTF-8)，来进行编码。
	//按照指定的字符集进行编码
	byte[] bytes1 = data.getBytes("GBK");

//2.解码
	String s1 = new String(bytes);////默认是按照平台字符集(UTF-8)，来进行编码。
	//指定
	String s2 = new String(bytes1,"GBK");
```

## 2、Java代码完成对字符的解码

| **String提供了如下方法**                     | 说明                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| **String(byte[] bytes)**                     | 通过使用平台的默认字符集解码指定的字节数组来构造新的  String |
| **String(byte[] bytes, String charsetName)** | 通过指定的字符集解码指定的字节数组来构造新的 String          |







# 二、iO流

+ 用于读写数据的 
+ **i - 指Input，称为输入流；负责将数据读到内存去**
+ **O - 指Output，称为输出流；负责写数据出去到（硬盘，网络...）**



## 1、总结流的四大类

**字节输入流**：以内存为基准，来自磁盘文件/网络中的数据**以字节的形式读入到内存**中去的流

**字节输出流**：以内存为基准，把内存中的数据**以字节写出到磁盘文件或者网络**中去的流。

**字符输入流**：以内存为基准，来自磁盘文件/网络中的数据**以字符的形式读入到内存**中去的流。

**字符输出流**：以内存为基准，把内存中的数据**以字符写出到磁盘文件或者网络介质中**去的流。









## 2、IO流的体系

**字节流**

+ 字节输入流
  - [ ] **InputStream	字节输入流（抽象类）**	--->
    - [ ] **FileInputStream	文件字节输入流（实现类）（低级流/原始流）**
    - [ ] **BufferedInfutStream	 字节缓冲输入流（包装流/处理流）**
    - [ ] 无
    - [ ] 无
    - [ ] **DataInputStream    数据输入流**
    - [ ] **ObjectInputStream    对象字节输入流**

    

+ 字节输出流
  - [ ] **OutputSteam	字节输出流（抽象类）**	--->
    - [ ] **FileOutputStream	文件字节输出流（实现类）（低级流/原始流）**
    - [ ] **BufferedOutputStream 	字节缓冲输出流**
    - [ ] 无
    - [ ] **PrintStream    打印流**
    - [ ] **DataOutputStream    数据输出流**
    - [ ] **Object OutputStream    对象字节输出流**



**字符流**

+ 字符输入流
  - [ ] **Reader	字符输入流（抽象类）**	--->
    - [ ] **FllieReader	文件字符输入流（实现类）（低级流/原始流）**
    - [ ] **BufferedPeader  	字符缓冲输入流 **
    - [ ] **InputStreamReader    字符输入转换流**
    - [ ] 无
+ 字符输出流
  - [ ] **Writer	字符输出流（抽象类）**	--->
    - [ ] **FileWriter	文件字符输出流（实现类）（低级流/原始流）**
    - [ ] **BufferedWriter    字符缓冲输出流**
    - [ ] **OutputStreamWriter    字符输出转换流**
    - [ ] **PrintWriter    打印流**



# 【1】字节流

## 1、InputStream （**字节输入流**）



## 2、FileInputStream （文件字节输入流）

+ 作用：以内存为基准，可以把磁盘文件中的数据以字节的形式读到内存中去。

  

| **构造器**                                 | **说明**                                         |
| ------------------------------------------ | ------------------------------------------------ |
| public **FileInputStream(File file)**      | 创建字节输入流管道与源文件接通                   |
| public **FileInputStream(Stringpathname)** | 创建字节输入流管道与源文件接通  （一般使用这个） |

| **方法名称**                                        | **说明**                                                     |
| --------------------------------------------------- | ------------------------------------------------------------ |
| public int **read()**                               | **每次读取一个字节返回**，如果发现没有数据可读会返回-1.      |
| public int **read(byte[]  buffer)**                 | **每次用一个字节数组去读取数据，返回字节数组读取了多少个字节，如果发现没有数据可读会返回-1.** |
| public byte[] **readAllBytes() throws IOException** | 直接将当前字节输入流对应的文件对象的字节数据装到一个字节数组返回 |

**注意：使用FileInputStream每次读取一个字节，读取性能较差，并且读取汉字输出会出现乱码。**

```Java
///1、创建文件字节输入管道，与源文件接通
//  InputStream is = new FileputStream(new File("文件路径"));一般不用这个
//推荐使用这个
	InputStream is = new FileInputStream("文件路径");

///2、开始读取文件的字节数据(2.1读取一个字节)
//public int read();每次读取一个字节返回，如果没有数据了，返回-1;
	int b1 = is.read();
	System.out.println((char)b1);
//使用循环来改善代码
	int  b;
	while((b ==is.read()) != -1){
   	 	System.out.println((char)b);
	}
////这个方案读取数据的性能很差，因为会频繁的调用系统资源
////读取汉字会乱码，并且无法避免
////流使用完毕后，必须要关闭！释放系统资源！
	is.close();

```

```java 
InputStream is=new FileInputStream("文件路径");
///2、开始读取文件中的字节数（每次读取多个字节）
	byte[] buffer = new byte[3];//当作桶，3代表每次最多能读3个字节
	int len = is.read( buffer );//用来记录读了多少个字节，没有就返回-1
	/String rs = new String(buffer);
///改造
	byte[] buffer = new byte[3];
	int len;//记住每次读取了多少个字节
	while((len =is.read(buffer)) != -1){
  	  String rs = new String(buffer, 0 ,len)//从0开始读多少倒多少（处理buffer数组）
	        System.out.print(rs);
	}
//性能得到明显提升！！
//但也不能避免读取汉字出现乱码的问题
	is.close();//关闭流
```





## 3、OutputStream	（字节输出流）



## 4、FileOutputStream	(文件字节输出流)

+ 作用：以内存为基准，把内存中的数据以字节的形式写出到文件中去。

| **构造器**                                                   | **说明**                                       |
| ------------------------------------------------------------ | ---------------------------------------------- |
| public **FileOutputStream(File file)**                       | 创建字节输出流管道与源文件对象接通             |
| public **FileOutputStream(String filepath)**                 | 创建字节输出流管道与源文件路径接通             |
| public **FileOutputStream(File file，boolean append)**       | 创建字节输出流管道与源文件对象接通，可追加数据 |
| public **FileOutputStream(String filepath，boolean append)** | 创建字节输出流管道与源文件路径接通，可追加数据 |

| **方法名称**                                             | **说明**                     |
| -------------------------------------------------------- | ---------------------------- |
| public void **write(int a)**                             | 写一个字节出去               |
| public void **write(byte[] buffer)**                     | **写一个字节数组出去**       |
| public void **write(byte[] buffer , int pos , int len)** | 写一个字节数组的一部分出去。 |
| public void **close() throws IOException**               | 关闭流。                     |

byte[] bytes = "我爱你中国abc"**.getBytes();将字符串转换成字节数组**

```Java
 // 1、创建一个字节输出流管道与目标文件接通。
        // 覆盖管道：覆盖之前的数据
//        OutputStream os =
//                new FileOutputStream("文件路径");
        // 追加数据的管道
        OutputStream os =
                new FileOutputStream("文件路径", true);

        // 2、开始写字节数据出去了
        os.write(97); // 97就是一个字节，代表a
        os.write('b'); // 'b'也是一个字节
        // os.write('磊'); // [ooo] 默认只能写出去一个字节

        byte[] bytes = "我爱你中国abc".getBytes();
        os.write(bytes);
        os.write(bytes, 0, 15);

        // 换行符
        os.write("\r\n".getBytes());
        os.close(); // 关闭流
```



### 4.1、案例：文件复制

```Java
// 需求：复制照片。
// 1、创建一个字节输入流管道与源文件接通
	InputStream is = new FileInputStream("文件路径");
// 2、创建一个字节输出流管道与目标文件接通。
	OutputStream os = new FileOutputStream("文件路径");

// 3、创建一个字节数组，负责转移字节数据。
	byte[] buffer = new byte[1024]; // 1KB.
// 4、从字节输入流中读取字节数据，写出去到字节输出流中。读多少写出去多少。
	int len; // 记住每次读取了多少个字节。
	while ((len = is.read(buffer)) != -1){
    	os.write(buffer, 0, len);
	}
	os.close();
	is.close();
	System.out.println("复制完成！！");
```











# 【2】字符流



## 1、Reader	（字符输入流）



## 2、FileReader	（文件字符输入流）

+ 作用：以内存为基准，可以把文件中的数据以字符的形式读到内存中去。

| **构造器**                             | **说明**                       |
| -------------------------------------- | ------------------------------ |
| public **FileReader(File file)**       | 创建字符输入流管道与源文件接通 |
| public **FileReader(String pathname)** | 创建字符输入流管道与源文件接通 |

| **方法名称**                        | **说明**                                                     |
| ----------------------------------- | ------------------------------------------------------------ |
| public int **read()**               | 每次读取一个字符返回，如果发现没有数据可读会返回-1.          |
| public int **read(char[]  buffer)** | 每次用一个字符数组去读取数据，返回字符数组读取了多少个字符，如果发现没有数据可读会返回-1. |



```Java
 public static void main(String[] args)  {
        try (
                // 1、创建一个文件字符输入流管道与源文件接通
                Reader fr = new FileReader("文件路径");
                ){
            // 2、读取文本文件的内容了。
//            int c; // 记住每次读取的字符编号。
//            while ((c = fr.read()) != -1){
//                System.out.print((char) c);
//            }
            // 每次读取一个字符的形式，性能肯定是比较差的。

            // 3、每次读取多个字符。
            char[] buffer = new char[3];
            int len; // 记住每次读取了多少个字符。
            while ((len = fr.read(buffer)) != -1){
                // 读取多少倒出多少
                System.out.print(new String(buffer, 0, len));
            }
            // 性能是比较不错的！
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```













## 3、Writer	（字符输出流）

**字符输出流写出数据后，必须刷新流，或者关闭流，写出去的数据才能生效**

| **方法名称**                                | **说明**                                             |
| ------------------------------------------- | ---------------------------------------------------- |
| public  void **flush() throws IOException** | 刷新流，就是将内存中缓存的数据立即写到文件中去生效！ |
| public  void **close() throws IOException** | 关闭流的操作，包含了刷新！                           |



## 4、FileWriter	（文件字符输出流）

+ 作用：以内存为基准，把内存中的数据以字符的形式写到文件中去。

| **构造器**                                             | **说明**                                       |
| ------------------------------------------------------ | ---------------------------------------------- |
| public **FileWriter(File file)**                       | 创建字节输出流管道与源文件对象接通             |
| public **FileWriter(String filepath)**                 | 创建字节输出流管道与源文件路径接通             |
| public **FileWriter(File file，boolean append)**       | 创建字节输出流管道与源文件对象接通，可追加数据 |
| public **FileWriter(String filepath，boolean append)** | 创建字节输出流管道与源文件路径接通，可追加数据 |

| **方法名称**                                   | **说明**             |
| ---------------------------------------------- | -------------------- |
| void  **write(int c)**                         | 写一个字符           |
| void  **write(String str)**                    | 写一个字符串         |
| void  **write(String str, int off, int len)**  | 写一个字符串的一部分 |
| void  **write(char[] cbuf)**                   | 写入一个字符数组     |
| void  **write(char[] cbuf, int off, int len)** | 写入字符数组的一部分 |

```Java
public static void main(String[] args) {
    try (
            // 0、创建一个文件字符输出流管道与目标文件接通。
            // 覆盖管道
            // Writer fw = new FileWriter("文件路径");
            // 追加数据的管道
            Writer fw = new FileWriter("文件路径", true);
            ){
        // 1、public void write(int c):写一个字符出去
        fw.write('a');
        fw.write(97);
        //fw.write('磊'); // 写一个字符出去
        fw.write("\r\n"); // 换行

        // 2、public void write(String c)写一个字符串出去
        fw.write("我爱你中国abc");
        fw.write("\r\n");

        // 3、public void write(String c ,int pos ,int len):写字符串的一部分出去
        fw.write("我爱你中国abc", 0, 5);
        fw.write("\r\n");

        // 4、public void write(char[] buffer):写一个字符数组出去
        char[] buffer = {'很','c','hao'}
        fw.write(buffer);
        fw.write("\r\n");

        // 5、public void write(char[] buffer ,int pos ,int len):写字符数组的一部分出去
        fw.write(buffer, 0, 2);
        fw.write("\r\n");
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```





























# 释放资源的方式

## try-catch-finally

```java 
try {
	...
    ... 	
} catch (IOException e) {
   	e.printStackTrace();
}finally{

}
```

+ **finally代码区的特点：无论try中的程序是正常执行了，还是出现了异常，最后都一定会执行finally区，除非JVM终止。**

+ **作用：一般用于在程序执行完成后进行资源的释放操作（专业级做法）。**



```Java
public static void main(String[] args)  {
    InputStream is = null;
    OutputStream os = null;
    try {
        //System.out.println(10 / 0);不要再流开始前出现错误
        // 1、创建一个字节输入流管道与源文件接通
        is = new FileInputStream("文件路径");
        // 2、创建一个字节输出流管道与目标文件接通。
        os = new FileOutputStream("文件路径");

        System.out.println(10 / 0);

        // 3、创建一个字节数组，负责转移字节数据。
        byte[] buffer = new byte[1024]; // 1KB.
        // 4、从字节输入流中读取字节数据，写出去到字节输出流中。读多少写出去多少。
        int len; // 记住每次读取了多少个字节。
        while ((len = is.read(buffer)) != -1){
            os.write(buffer, 0, len);
        }
        System.out.println("复制完成！！");
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        // 释放资源的操作
        try {
            if(os != null) os.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            if(is != null) is.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```





## try-with-resource

+ ​	JDK7 	开始

```java 
try(定义资源1;定义资源2;…）{
	可能出现异常的代码;
}catch(异常类名 变量名){
	异常的处理代码;
} 

```

**该资源使用完毕后，会自动调用其close()方法，完成对资源的释放！**

+ () 中只能放置资源，否则报错

+ 什么是资源呢？

+ 资源一般指的是最终实现了AutoCloseable接口。

```Java
public static void main(String[] args)  {
    try (
            // 1、创建一个字节输入流管道与源文件接通
            InputStream is = new FileInputStream("文件路径");
            // 2、创建一个字节输出流管道与目标文件接通。
            OutputStream os = new FileOutputStream("文件路径");

            // 注意：这里只能放置资源对象。（流对象）
            // int age = 21;
            // 什么是资源呢？资源都是会实现AutoCloseable接口。资源都会有一个close方法，并且资源放到这里后
            // 用完之后，会被自动调用其close方法完成资源的释放操作。
            MyConnection conn = new MyConnection();
            ){

        // 3、创建一个字节数组，负责转移字节数据。
        byte[] buffer = new byte[1024]; // 1KB.
        // 4、从字节输入流中读取字节数据，写出去到字节输出流中。读多少写出去多少。
        int len; // 记住每次读取了多少个字节。
        while ((len = is.read(buffer)) != -1){
            os.write(buffer, 0, len);
        }
        System.out.println(conn);
        System.out.println("复制完成！！");

    } catch (Exception e) {
        e.printStackTrace();
    }
}
```