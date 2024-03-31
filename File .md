# File

# 1、File类

​		File是 `java.io.File`包下的类， File类的对象，用于代表当前操作系统的文件（可以是文件、或文件夹）。

​	**注意**：File类只能对文件本身进行操作，**不能读写文件里面存储的数据。**

## 1.1、创建File类的文件

| **构造器**                                   | **说明**                                           |
| -------------------------------------------- | -------------------------------------------------- |
| public **File(String pathname)**             | 根据文件路径创建文件对象                           |
| public **File(String parent, String child)** | **根据父路径和子路径名字创建文件对象**             |
| public **File(File   parent, String child)** | **根据父路径对应文件对象和子路径名字创建文件对象** |

​	**注意**

+ File对象既可以代表文件、也可以代表文件夹。

+ File封装的对象仅仅是一个路径名，这个路径是可以存在的、也允许是不存在的。

```Java
//存在的路径
File f1 = new File("D:/resource/ab.txt");
File f1 = new File("D:\\resource\\ab.txt");
//或者可以使用下边的File.separator  来获得系统的路径分割符
File f1 = new File("D:" + File.separator +"resource" + 							File.separator + "ab.txt");//File.separator用来获取当前系统的分割符
System.out.println(f1.length()); // 文件大小

//可以指定一个不存在的文件路径
File f2 = new File("D:\\resource\\aaaa.txt"); //不存在的路径
System.out.println(f2.length());//0
System.out.println(f2.exists());//false	用来判断文件路径是否存在
//不存在的话可以调用   方法来创建文件
下面有详细解析
```

//这点内容在下方有

| 用来创建文件/路径的方法            | 说明                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| Public boolean **createNewFile()** | 这个方法尝试在文件系统中创建一个新文件，如果文件已经存在，则返回 `false`。 |
| public boolean **mkdir()**         | `mkdir()` 创建单层目录，如果目录已存在或创建失败，则返回 `false`。 |
| public boolean **mkdir()**         | `mkdirs()` 创建多层目录，包括所有不存在的父目录。            |



**绝对路径、相对路径**

```Java
绝对路径：从盘符开始
File file1 = new File(“D:\\itheima\\a.txt”); 
相对路径：不带盘符，默认直接在当前工程下的目录寻找文件。
File file3 = new File(“名\\a.txt”); 
```



### File提供的判断文件类型、获取文件信息功能

| **方法名称**                        | **说明**                                                     |
| ----------------------------------- | ------------------------------------------------------------ |
| public boolean **exists()**         | 判断当前文件对象，对应的文件路径是否存在，存在返回true       |
| public boolean **isFile()**         | 判断当前文件对象指代的是否是文件，是文件返回true，反之。     |
| public boolean **isDirectory()**    | 判断当前文件对象指代的是否是文件夹，是文件夹返回true，反之。 |
| public String **getName()**         | 获取文件的名称（包含后缀）                                   |
| public long **length()**            | 获取文件的大小，返回字节个数                                 |
| public long **lastModified()**      | 获取文件的最后修改时间。                                     |
| public String **getPath()**         | 获取创建文件对象时，使用的路径                               |
| public String **getAbsolutePath()** | 获取绝对路径                                                 |

```Java
// 1.创建文件对象，指代某个文件
File f1 = new File("D:/resource/ab.txt");
//File f1 = new File("D:/resource/");

// 2、public boolean exists()：判断当前文件对象，对应的文件路径是否存在，存在返回true.
System.out.println(f1.exists());

// 3、public boolean isFile() : 判断当前文件对象指代的是否是文件，是文件返回true，反之。
System.out.println(f1.isFile());//是否是文件

// 4、public boolean isDirectory()  : 判断当前文件对象指代的是否是文件夹，是文件夹返回true，反之。
System.out.println(f1.isDirectory());//是否是文件夹

// 5.public String getName()：获取文件的名称（包含后缀）
System.out.println(f1.getName());

// 6.public long length()：获取文件的大小，返回字节个数
System.out.println(f1.length());

// 7.public long lastModified()：获取文件的最后修改时间。
long time = f1.lastModified();//返回时间毫秒值
SimpleDateFormat sdf = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");//格式
System.out.println(sdf.format(time));

// 8.public String getPath()：获取创建文件对象时，使用的路径
File f2 = new File("D:\\resource\\ab.txt");
File f3 = new File("file-io-app\\src\\itheima.txt");
System.out.println(f2.getPath());
System.out.println(f3.getPath());

// 9.public String getAbsolutePath()：获取绝对路径
System.out.println(f2.getAbsolutePath());
System.out.println(f3.getAbsolutePath());
```



### File类提供的创建文件的功能

| 方法名称                           | 说明                     |
| ---------------------------------- | ------------------------ |
| public boolean **createNewFile()** | 创建一个新的空的**文件** |
| public boolean **mkdir()**         | 只能创建一级**文件夹**   |
| public boolean **mkdirs()**        | 可以创建多级文件夹       |



### File类提供的删除文件的功能

| 方法名称                     | 说明               |
| ---------------------------- | ------------------ |
| public  boolean **delete()** | 删除文件、空文件夹 |

**注意：delete方法默认只能删除文件和空文件夹**，删除后的文件不会进入回收站。



### File类提供的遍历文件夹的功能

| **方法名称**                  | **说明**                                                     |
| ----------------------------- | ------------------------------------------------------------ |
| public String[] **list()**    | 获取当前目录下所有的"一级文件名称"到一个字符串数组中去返回。 |
| public File[] **listFiles()** | **获取当前目录下所有的"一级文件对象"到一个文件对象数组中去返回（重点）** |

```Java
File f1 = new File("文件路径")；
String[] names = f1.list();//获取一级文件名称

File[] files = f1.listFiles();//用来获取一级文件对象(重点)

```



### 使用 listFiles 方法时要注意的事项

* 当主调是文件，或者路径不存在时，返回null

* 当主调是空文件夹时，返回一个长度为0的属组
* **当主调时一个有内容的文件夹时，将里面的所有一级文件的路径放到一个File数组中返回**
* 当主调是一个文件夹，且里面有隐藏文件时，将里面所有文件和文件夹的路径放在File数组中返回，包含隐藏文件
* 当主调是一个文件夹，但是没有权限访问该文件夹时，返回null







## 递归	一种算法

​	**什么是递归**

* 递归是一种算法，在程序设计语言中广泛应用。
* 从形式上说：方法调用自身的形式称为方法递归（recursion）

**递归的形式**

* 直接递归：方法自己指向自己
* 间接递归：方法调用其他方法，其他方法又回调方法自己。

**使用方法递归时需要注意的问题**

* 递归如果没有控制好终止，就会出现递归死循环，导致栈内存溢出错误。

```java 
public static void main (String args){
    //猴子案例，每天吃桃子的一半＋ 1个；第十天还剩 1个，球第一天
    System.out.println(f(1));

}
public static int f(int n){
    if (n == 10){
        return 1;
    }else {
        return 2*f(n+1)+2;
    }
}
```



**案例2**，，文件搜索

```Java
public class RecursionTest3 {
    public static void main(String[] args) throws Exception {
          searchFile(new File("E:/") , "QQ.exe");
    }

    /**
     * 去目录下搜索某个文件
     * @param dir  目录
     * @param fileName 要搜索的文件名称
     */
    public static void searchFile(File dir, String fileName) throws Exception {
        // 1、把非法的情况都拦截住
        if(dir == null || !dir.exists() || dir.isFile()){
            return; // 代表无法搜索
        }

        // 2、dir不是null,存在，一定是目录对象。
        // 获取当前目录下的全部一级文件对象。
        File[] files = dir.listFiles();

        // 3、判断当前目录下是否存在一级文件对象，以及是否可以拿到一级文件对象。
        if(files != null && files.length > 0){
            // 4、遍历全部一级文件对象。
            for (File f : files) {
                // 5、判断文件是否是文件,还是文件夹
                if(f.isFile()){
                    // 是文件，判断这个文件名是否是我们要找的
                    if(f.getName().contains(fileName)){
                        System.out.println("找到了：" + f.getAbsolutePath());
                        Runtime runtime = Runtime.getRuntime();
                        runtime.exec(f.getAbsolutePath());
                    }
                }else {
                    // 是文件夹，继续重复这个过程（递归）
                    searchFile(f, fileName);
                }
            }
        }
    }
```

**案例3**，，文件删除

```Java
package DiGui;

import java.io.File;

public class Test5 {
    public static void main(String[] args) {
        File f = new File("D:\\wwww - 副本");
        deleteFile(f);

    }
    public static void deleteFile (File dir) {
        if (dir == null || !dir.exists()){
            //判断是否为null , 或者文件夹是否纯在
            return;
        }
        if (dir.isFile()){
            //用来判断是否为文件，是直接删除
            dir.delete();
            return;
        }
        //用来获取文件夹中的一级文件名；
        File[] f = dir.listFiles();
        if (f == null){
            return;
        }

        //2.这是一个有内容的文件夹，直接删除其中的内容在干掉自己
        for (File file : f) {
            if (file.isFile()) {
                file.delete();
            }else {
                deleteFile(file);
            }

        }
        dir.delete();


    }
}
```

















