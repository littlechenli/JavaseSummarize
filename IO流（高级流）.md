# IO流（高级流）

# 缓冲流	

一般不用多态形式，以便能够使用新增的方法。

## 字节缓冲流

**作用：提高字节流读写数据的性能**

+ 原理：字节缓冲输入流自带8kb的缓冲池；字节缓冲输出路也自带8kb缓冲池

| **构造器**                                       | **说明**                                                     |
| ------------------------------------------------ | ------------------------------------------------------------ |
| public **BufferedInputStream(InputStream is)**   | 把低级的字节输入流包装成一个高级的缓冲字节输入流，从而提高读数据的性能 |
| public **BufferedOutputStream(OutputStream os)** | 把低级的字节输出流包装成一个高级的缓冲字节输出流，从而提高写数据的性能 |

```Java
public static void main(String[] args) {
    try (
            InputStream is = new FileInputStream("文件路径");//原始的字节输入流
            // 1、定义一个字节缓冲输入流包装原始的字节输入流
            InputStream bis = new BufferedInputStream(is);

            OutputStream os = new FileOutputStream("文件路径");//原始的字节输出流
            // 2、定义一个字节缓冲输出流包装原始的字节输出流
            OutputStream bos = new BufferedOutputStream(os);
    ){

        byte[] buffer = new byte[1024];
        int len;
        while ((len = bis.read(buffer)) != -1){
            bos.write(buffer, 0, len);
        }
        System.out.println("复制完成！！");

    } catch (Exception e) {
        e.printStackTrace();
    }
}
```







## 字符缓冲流

### BufferedReader	(字符缓冲输入流)

+ 作用：自带8k的字符缓冲池，可以提高字符输入流字符数据的性能。

| **构造器**                           | **说明**                                                     |
| ------------------------------------ | ------------------------------------------------------------ |
| public  **BufferedReader(Reader r)** | 把低级的字符输入流包装成字符缓冲输入流管道，从而提高字符输入流读字符数据的性能 |

**字符缓冲输入流新增的功能：按照行读取字符**

| **方法**                      | **说明**                                         |
| ----------------------------- | ------------------------------------------------ |
| public  String **readLine()** | 读取一行数据返回，如果没有数据可读了，会返回null |

```Java
public static void main(String[] args)  {
        try (
                Reader fr = new FileReader("文件路径");
                // 创建一个字符缓冲输入流包装原始的字符输入流
                BufferedReader br = new BufferedReader(fr);
        ){
//            char[] buffer = new char[3];
//            int len;
//            while ((len = br.read(buffer)) != -1){
//                System.out.print(new String(buffer, 0, len));
//            }
//            System.out.println(br.readLine());
//            System.out.println(br.readLine());
//            System.out.println(br.readLine());
//            System.out.println(br.readLine());

            String line; // 记住每次读取的一行数据
            while ((line = br.readLine()) != null){
                System.out.println(line);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```







### BufferedWriter	(字符缓冲输出流)

+ 作用：自带8k的字符缓冲池，可以提高字符输出流写字符数据的性能。

| **构造器**                           | **说明**                                                     |
| ------------------------------------ | ------------------------------------------------------------ |
| public  **BufferedWriter(Writer r)** | 把低级的字符输出流包装成一个高级的缓冲字符输出流管道，从而提高字符输出流写数据的性能 |

字符缓冲输出流新增的功能：换行

| **方法**                   | **说明** |
| -------------------------- | -------- |
| public  void **newLine()** | 换行     |

```Java
public static void main(String[] args) {
    try (
            Writer fw = new FileWriter("路径", true);
            // 创建一个字符缓冲输出流管道包装原始的字符输出流
            BufferedWriter bw = new BufferedWriter(fw);
    ){

        bw.write('a');
        bw.write(97);
        bw.write('磊');
        bw.newLine();

        bw.write("我爱你中国abc");
        bw.newLine();

    } catch (Exception e) {
        e.printS tackTrace();
    }
}
```



# 转换流



## InputStreamReader （字符输入转换流）



+ 解决不同编码时，字符流读取文本内容乱码的问题
+ 解决思路：先获取文件的原始字节流，再将其按真实的字符集编码转成字符输出流，这样字符输入流中的字符就不乱码了

| **构造器**                                                   | **说明**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public InputStreamReader(InputStream is)                     | 把原始的字节输入流，按照代码默认编码转成字符输入流（与直接用FileReader的效果一样） |
| public **InputStreamReader(InputStream is ,String charset)** | **把原始的字节输入流，按照指定的字符集编码成字符输入流（重点）** |



```Java
public static void main(String[] args) {
    try (
            // 1、得到文件的原始字节流（GBK的字节流形式）
            InputStream is = new FileInputStream("文件路径");
            // 2、把原始的字节输入流按照指定的字符集编码转换成字符输入流
            Reader isr = new InputStreamReader(is, "GBK");
            // 3、把字符输入流包装成缓冲字符输入流
            BufferedReader br = new BufferedReader(isr);
            ){
        String line;
        while ((line = br.readLine()) != null){
            System.out.println(line);
        }


    } catch (Exception e) {
        e.printStackTrace();
    }
}
```





## OutputStreamWrite  （字符输出转换流）

+ 作用：可以控制写出去的字符使用什么字符集编码。 

+ 解决思路：获取字节输出流，再按照指定的字符集编码将其转换成字符输出流，以后写出去的字符就会用该字符集编码了。

| 构造器                                                      | 说明                                                       |
| ----------------------------------------------------------- | ---------------------------------------------------------- |
| public OutputStreamWriter(OutputStream os)                  | 可以把原始的字节输出流，按照代码默认编码转换成字符输出流。 |
| public OutputStreamWriter(OutputStream is ，String charset) | 可以把原始的字节输出流，按照指定编码转换成字符输出流(重点) |

```java 
public static void main(String[] args) {
    // 指定写出去的字符编码。
    try (
            // 1、创建一个文件字节输出流
            OutputStream os = new FileOutputStream("文件路径");
            // 2、把原始的字节输出流，按照指定的字符集编码转换成字符输出转换流。
            Writer osw = new OutputStreamWriter(os, "GBK");
            // 3、把字符输出流包装成缓冲字符输出流
            BufferedWriter bw = new BufferedWriter(osw);
            ){
        bw.write("我是中国人abc");
        bw.write("我爱你中国123");

    } catch (Exception e) {
        e.printStackTrace();
    }
}
```





# 打印流

**PrintStream/printWriter（打印流）**

+ 作用：打印流可以实现更方便、更高效的打印数据出去，能实现打印啥出去就是啥出去。



## PrintStream  

| **构造器**                                                   | **说明**                                 |
| ------------------------------------------------------------ | ---------------------------------------- |
| public  **PrintStream(OutputStream/File/String)**            | 打印流直接通向字节输出流/文件/文件路径   |
| public **PrintStream(String fileName, Charset charset)**     | 可以指定写出去的字符编码                 |
| public **PrintStream(OutputStream  out,  boolean autoFlush)** | 可以指定实现自动刷新                     |
| public **PrintStream(OutputStream out,  boolean autoFlush, String encoding)** | 可以指定实现自动刷新，并可指定字符的编码 |



| **方法**                                        | **说明**                   |
| ----------------------------------------------- | -------------------------- |
| public  void **println(Xxx  xx)**               | 打印任意类型的数据出去     |
| public  void **write(int/byte[]/byte[]一部分)** | 可以支持写**字节**数据出去 |

```java 
 public static void main(String[] args) {
        try (
                // 1、创建一个打印流管道
//                PrintStream ps =
//                        new PrintStream("文件路径", Charset.forName("GBK"));
//                PrintStream ps =
//                        new PrintStream("文件路径");
                PrintWriter ps =
                        new PrintWriter(new FileOutputStream("文件路径", true));
                ){
                ps.println(97);
                ps.println('a');
                ps.println("我爱你中国abc");
                ps.println(true);
                ps.println(99.5);

                // ps.write(97); // 'a'

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```





## PrintWriter

| **构造器**                                                   | **说明**                                 |
| ------------------------------------------------------------ | ---------------------------------------- |
| public  **PrintWriter(OutputStream/Writer/File/String**)     | 打印流直接通向字节输出流/文件/文件路径   |
| public  **PrintWriter(String fileName,  Charset charset)**   | 可以指定写出去的字符编码                 |
| public  **PrintWriter(OutputStream out/Writer, boolean autoFlush)** | 可以指定实现自动刷新                     |
| public  **PrintWriter(OutputStream out, boolean autoFlush,  String encoding)** | 可以指定实现自动刷新，并可指定字符的编码 |

| **方法**                                     | **说明**               |
| -------------------------------------------- | ---------------------- |
| public  void **println(Xxx  xx)**            | 打印任意类型的数据出去 |
| public  void **write(int/String/char[]/..)** | 可以支持写字符数据出去 |



**PrintStream和PrintWriter的区别**

+ 打印数据的功能上是一模一样的：都是使用方便，性能高效（核心优势）

+ PrintStream继承自字节输出流OutputStream，因此支持写字节数据的方法。

+ PrintWriter继承自字符输出流Writer，因此支持写字符数据出去。



```Java
public static void main(String[] args) {
    System.out.println("老骥伏枥");
    System.out.println("志在千里");

    try ( PrintStream ps = new PrintStream("文件地址"); ){

        // 把系统默认的打印流对象改成自己设置的打印流
        System.setOut(ps);

        System.out.println("烈士暮年");
        System.out.println("壮心不已");
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```

### 改变打印流向

`System.out`就是`PrintStream`类型的，只不过它的流向是系统规定的，打印在控制台上。不过，既然是流对象，我们就可以玩一个"小把戏"，改变它的流向。

```java
public class PrintDemo {
    public static void main(String[] args) throws IOException {
		// 调用系统的打印流,控制台直接输出97
        System.out.println(97);
      
		// 创建打印流,指定文件的名称
        PrintStream ps = new PrintStream("ps.txt");
      	
      	// 设置系统的打印流流向,输出到ps.txt
        System.setOut(ps);
      	// 调用系统的打印流,ps.txt中输出97
        System.out.println(97);
    }
}
```

# 

# 数据流

## DateOutputStream    (数据输出流)

+ 允许把数据和其类型一并写出去

| **构造器**                                     | **说明**                             |
| ---------------------------------------------- | ------------------------------------ |
| public  **DataOutputStream(OutputStream out)** | 创建新数据输出流包装基础的字节输出流 |

| **方法**                                                     | **说明**                                          |
| ------------------------------------------------------------ | ------------------------------------------------- |
| public  final void **writeByte(int v) throws IOException**   | 将byte类型的数据写入基础的字节输出流              |
| public  final void **writeInt(int v)**  throws  IOException  | 将int类型的数据写入基础的字节输出流               |
| public  final void **writeDouble(Double v)**  throws  IOException | 将double类型的数据写入基础的字节输出流            |
| public  final void **writeUTF(String str)**  throws IOException | 将字符串数据以UTF-8编码成字节写入基础的字节输出流 |
| public  void **write(int/byte[]/byte[]一部分)**              | 支持写字节数据出去                                |

```Java
public static void main(String[] args) {
    try (
            // 1、创建一个数据输出流包装低级的字节输出流
         DataOutputStream dos =
              new DataOutputStream(new FileOutputStream("路径"));
            ){
        dos.writeInt(97);
        dos.writeDouble(99.5);
        dos.writeBoolean(true);
        dos.writeUTF("程序员666！");

    } catch (Exception e) {
        e.printStackTrace();
    }
}
```





## DataInputSstream    （数据输入流）



| **构造器**                                  | **说明**                             |
| ------------------------------------------- | ------------------------------------ |
| public  **DataInputStream(InputStream is)** | 创建新数据输入流包装基础的字节输入流 |

| **方法**                                                   | **说明**                    |
| ---------------------------------------------------------- | --------------------------- |
| Public  final byte **readByte()** throws IOException       | 读取字节数据返回            |
| public  final int **readInt()**  throws  IOException       | 读取int类型的数据返回       |
| public  final double **readDouble()**  throws  IOException | 读取double类型的数据返回    |
| public  final String **readUTF()**  throws IOException     | 读取字符串数（UTF-8）据返回 |
| public  int **readInt()/read(byte[])**                     | 支持读字节数据进来          |



```Java
public static void main(String[] args) {
    try (
            DataInputStream dis =
                    new DataInputStream(new FileInputStream("文件路径"));
            ){
        int i = dis.readInt();//与输入必须一致dos.writeInt(97);
        System.out.println(i);

        double d = dis.readDouble();//dos.writeDouble(99.5);
        System.out.println(d);

        boolean b = dis.readBoolean();// dos.writeBoolean(true);
        System.out.println(b);

        String rs = dis.readUTF();//dos.writeUTF("程序员666！");
        System.out.println(rs);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```





# 序列化流



## ObjectOutputStream    （对象字节输出流)

| **构造器**                                       | **说明**                                 |
| ------------------------------------------------ | ---------------------------------------- |
| public  **ObjectOutputStream(OutputStream out)** | 创建对象字节输出流，包装基础的字节输出流 |

| **方法**                                                     | **说明**     |
| ------------------------------------------------------------ | ------------ |
| public  final void **writeObject(Object o)** throws  IOException | 把对象写出去 |

**注意：对象如果要参与序列化，必须实现序列化接口（java.io.Serializable）**


user对象

```Java
// 注意：对象如果需要序列化，必须实现序列化接口。
public class User implements Serializable {
    private String loginName;
    private String userName;
    private int age;
    // transient 这个成员变量将不参与序列化。
    private transient String passWord;
```

目标：掌握对象字节输出流的使用：序列化对象。

```Java
public static void main(String[] args) {
    try (
            // 2、创建一个对象字节输出流包装原始的字节 输出流。
            ObjectOutputStream oos =
                    new ObjectOutputStream(new FileOutputStream("io-app2/src/itheima11out.txt"));
            ){
        // 1、创建一个Java对象。
        User u = new User("admin", "张三", 32, "666888xyz");

        // 3、序列化对象到文件中去
        oos.writeObject(u);
        System.out.println("序列化对象成功！！");

    } catch (Exception e) {
        e.printStackTrace();
    }
}
```






## ObjectInputStream    (对象字节输入流)

+ 可以把Java对象进行反序列化：把存储在文件中的Java对象读入到内存中来。

| **构造器**                                    | **说明**                                 |
| --------------------------------------------- | ---------------------------------------- |
| public  **ObjectInputStream(InputStream is)** | 创建对象字节输入流，包装基础的字节输入流 |

| **方法**                              | **说明**                       |
| ------------------------------------- | ------------------------------ |
| public  final Object **readObject()** | 把存储在文件中的Java对象读出来 |







目标：掌握对象字节输入流的使用：反序列化对象。

```Java
public static void main(String[] args) {
    try (
            // 1、创建一个对象字节输入流管道，包装 低级的字节输入流与源文件接通
            ObjectInputStream ois = new ObjectInputStream(new FileInputStream("io-app2/src/itheima11out.txt"));
            ){
        User u = (User) ois.readObject();
        System.out.println(u);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```



 

# 压缩流/解压流

压缩流：

​	负责压缩文件或者文件夹

解压缩流：

​	负责把压缩包中的文件和文件夹解压出来

```java
/*
*   解压缩流
*
* */
public class ZipStreamDemo1 {
    public static void main(String[] args) throws IOException {

        //1.创建一个File表示要解压的压缩包
        File src = new File("D:\\aaa.zip");
        //2.创建一个File表示解压的目的地
        File dest = new File("D:\\");

        //调用方法
        unzip(src,dest);

    }

    //定义一个方法用来解压
    public static void unzip(File src,File dest) throws IOException {
        //解压的本质：把压缩包里面的每一个文件或者文件夹读取出来，按照层级拷贝到目的地当中
        //创建一个解压缩流用来读取压缩包中的数据
        ZipInputStream zip = new ZipInputStream(new FileInputStream(src));
        //要先获取到压缩包里面的每一个zipentry对象
        //表示当前在压缩包中获取到的文件或者文件夹
        ZipEntry entry;
        while((entry = zip.getNextEntry()) != null){
            System.out.println(entry);
            if(entry.isDirectory()){
                //文件夹：需要在目的地dest处创建一个同样的文件夹
                File file = new File(dest,entry.toString());
                file.mkdirs();
            }else{
                //文件：需要读取到压缩包中的文件，并把他存放到目的地dest文件夹中（按照层级目录进行存放）
                FileOutputStream fos = new FileOutputStream(new File(dest,entry.toString()));
                int b;
                while((b = zip.read()) != -1){
                    //写到目的地
                    fos.write(b);
                }
                fos.close();
                //表示在压缩包中的一个文件处理完毕了。
                zip.closeEntry();
            }
        }
        zip.close();
    }
}
```

```java
public class ZipStreamDemo2 {
    public static void main(String[] args) throws IOException {
        /*
         *   压缩流
         *      需求：
         *          把D:\\a.txt打包成一个压缩包
         * */
        //1.创建File对象表示要压缩的文件
        File src = new File("D:\\a.txt");
        //2.创建File对象表示压缩包的位置
        File dest = new File("D:\\");
        //3.调用方法用来压缩
        toZip(src,dest);
    }

    /*
    *   作用：压缩
    *   参数一：表示要压缩的文件
    *   参数二：表示压缩包的位置
    * */
    public static void toZip(File src,File dest) throws IOException {
        //1.创建压缩流关联压缩包
        ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(new File(dest,"a.zip")));
        //2.创建ZipEntry对象，表示压缩包里面的每一个文件和文件夹
        //参数：压缩包里面的路径
        ZipEntry entry = new ZipEntry("aaa\\bbb\\a.txt");
        //3.把ZipEntry对象放到压缩包当中
        zos.putNextEntry(entry);
        //4.把src文件中的数据写到压缩包当中
        FileInputStream fis = new FileInputStream(src);
        int b;
        while((b = fis.read()) != -1){
            zos.write(b);
        }
        zos.closeEntry();
        zos.close();
    }
}
```

```java
public class ZipStreamDemo3 {
    public static void main(String[] args) throws IOException {
        /*
         *   压缩流
         *      需求：
         *          把D:\\aaa文件夹压缩成一个压缩包
         * */
        //1.创建File对象表示要压缩的文件夹
        File src = new File("D:\\aaa");
        //2.创建File对象表示压缩包放在哪里（压缩包的父级路径）
        File destParent = src.getParentFile();//D:\\
        //3.创建File对象表示压缩包的路径
        File dest = new File(destParent,src.getName() + ".zip");
        //4.创建压缩流关联压缩包
        ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(dest));
        //5.获取src里面的每一个文件，变成ZipEntry对象，放入到压缩包当中
        toZip(src,zos,src.getName());//aaa
        //6.释放资源
        zos.close();
    }

    /*
    *   作用：获取src里面的每一个文件，变成ZipEntry对象，放入到压缩包当中
    *   参数一：数据源
    *   参数二：压缩流
    *   参数三：压缩包内部的路径
    * */
    public static void toZip(File src,ZipOutputStream zos,String name) throws IOException {
        //1.进入src文件夹
        File[] files = src.listFiles();
        //2.遍历数组
        for (File file : files) {
            if(file.isFile()){
                //3.判断-文件，变成ZipEntry对象，放入到压缩包当中
                ZipEntry entry = new ZipEntry(name + "\\" + file.getName());//aaa\\no1\\a.txt
                zos.putNextEntry(entry);
                //读取文件中的数据，写到压缩包
                FileInputStream fis = new FileInputStream(file);
                int b;
                while((b = fis.read()) != -1){
                    zos.write(b);
                }
                fis.close();
                zos.closeEntry();
            }else{
                //4.判断-文件夹，递归
                toZip(file,zos,name + "\\" + file.getName());
                //     no1            aaa   \\   no1
            }
        }
    }
}
```





# 6. 工具包（Commons-io）

介绍：

​	Commons是apache开源基金组织提供的工具包，里面有很多帮助我们提高开发效率的API

比如：

​	StringUtils   字符串工具类

​	NumberUtils   数字工具类 

​	ArrayUtils   数组工具类  

​	RandomUtils   随机数工具类

​	DateUtils   日期工具类 

​	StopWatch   秒表工具类 

​	ClassUtils   反射工具类  

​	SystemUtils   系统工具类  

​	MapUtils   集合工具类

​	Beanutils   bean工具类

​	Commons-io io的工具类

​	等等.....

其中：Commons-io是apache开源基金组织提供的一组有关IO操作的开源工具包。

作用：提高IO流的开发效率。

使用方式：

1，新建lib文件夹

2，把第三方jar包粘贴到文件夹中

3，右键点击add as a library

代码示例：

```java
public class CommonsIODemo1 {
    public static void main(String[] args) throws IOException {
        /*
          FileUtils类
                static void copyFile(File srcFile, File destFile)                   复制文件
                static void copyDirectory(File srcDir, File destDir)                复制文件夹
                static void copyDirectoryToDirectory(File srcDir, File destDir)     复制文件夹
                static void deleteDirectory(File directory)                         删除文件夹
                static void cleanDirectory(File directory)                          清空文件夹
                static String readFileToString(File file, Charset encoding)         读取文件中的数据变成成字符串
                static void write(File file, CharSequence data, String encoding)    写出数据

            IOUtils类
                public static int copy(InputStream input, OutputStream output)      复制文件
                public static int copyLarge(Reader input, Writer output)            复制大文件
                public static String readLines(Reader input)                        读取数据
                public static void write(String data, OutputStream output)          写出数据
         */


        /* File src = new File("myio\\a.txt");
        File dest = new File("myio\\copy.txt");
        FileUtils.copyFile(src,dest);*/


        /*File src = new File("D:\\aaa");
        File dest = new File("D:\\bbb");
        FileUtils.copyDirectoryToDirectory(src,dest);*/

        /*File src = new File("D:\\bbb");
        FileUtils.cleanDirectory(src);*/



    }
}

```

# 7. 工具包（hutool）

介绍：

​	Commons是国人开发的开源工具包，里面有很多帮助我们提高开发效率的API

比如：

​	DateUtil  日期时间工具类 

​	TimeInterval  计时器工具类 

​	StrUtil  字符串工具类

​	HexUtil   16进制工具类

​	HashUtil   Hash算法类

​	ObjectUtil  对象工具类

​	ReflectUtil   反射工具类

​	TypeUtil  泛型类型工具类

​	PageUtil  分页工具类

​	NumberUtil  数字工具类

使用方式：

1，新建lib文件夹

2，把第三方jar包粘贴到文件夹中

3，右键点击add as a library

代码示例：

```java
public class Test1 {
    public static void main(String[] args) {
    /*
        FileUtil类:
                file：根据参数创建一个file对象
                touch：根据参数创建文件

                writeLines：把集合中的数据写出到文件中，覆盖模式。
                appendLines：把集合中的数据写出到文件中，续写模式。
                readLines：指定字符编码，把文件中的数据，读到集合中。
                readUtf8Lines：按照UTF-8的形式，把文件中的数据，读到集合中

                copy：拷贝文件或者文件夹
    */


       /* File file1 = FileUtil.file("D:\\", "aaa", "bbb", "a.txt");
        System.out.println(file1);//D:\aaa\bbb\a.txt

        File touch = FileUtil.touch(file1);
        System.out.println(touch);


        ArrayList<String> list = new ArrayList<>();
        list.add("aaa");
        list.add("aaa");
        list.add("aaa");

        File file2 = FileUtil.writeLines(list, "D:\\a.txt", "UTF-8");
        System.out.println(file2);*/

      /*  ArrayList<String> list = new ArrayList<>();
        list.add("aaa");
        list.add("aaa");
        list.add("aaa");
        File file3 = FileUtil.appendLines(list, "D:\\a.txt", "UTF-8");
        System.out.println(file3);*/
        List<String> list = FileUtil.readLines("D:\\a.txt", "UTF-8");
        System.out.println(list);
    }
}
```

















