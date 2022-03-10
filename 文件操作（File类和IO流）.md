## 文件操作（File类和IO流）

### 一、FIle类

#### 1.静态变量

```java
/**java.io.File
*Java中对文件和目录路径名的抽象表示形式
*Java把电脑中的文件和目录封装为一个File类，我们可以对其进行一些操作：
*		文件/目录的创建
*		文件/目录的删除
*		文件/目录的获取
*		文件/目录的判断
*		目录的遍历
*		获取文件大小
*/

/**java.io.File的四个静态变量
*static String pathSeparator;		//系统默认路径分隔符：String
*static char pathSeparatorChar;		//系统默认路径分隔符：char	
*Windows下为;分号	Linux下为:冒号
*
*static String separator;			//系统默认目录分隔符：String
*static char separatorChar;			//系统默认目录分隔符：char
*Windows下为\反斜杠	Linux下为/正斜杠
*/
```

#### 2.路径

```java
/**路径
*绝对路径：
*	绝对路径是指从盘符开始写的路径
*	如：C://User
*		D://test//a.txt
*
*相对路径：
*	相对路径是本项目的根目录开始的，可以简化路径的书写
* 	如：D://smart_city//a.txt ---> a.txt
*	
*注意：
*1.路径是不区分大小写的
*2.路径中Windows下的文件名称分隔符为/反斜杠，Linux下的文件名称分隔符为\正斜杠
*/


```

#### 3.构造方法

```java
/**File(String pathname);
*通过路径名创建一个File实例
*
*参数：
*1.路径名可以是一个目录也可以是一个文件
*2.路径可以使用相对路径也可以使用绝对路径
*3.路径可以是存在也可以是不存在
*/


/**File(String parent,String child)
*通过将父路径parent和子路径child拼接在一起创建一个新的File对象
*
*好处：
*	父路径和子路径分离可以使得父路径和子路径灵活多变
*/


/**File(File parent,String child)
*通过将父路径parent和子路径child拼接在一起创建一个新的File对象
*而父路径为一个File对象
*
*好处：
*	父路径和子路径分离可以使得父路径和子路径灵活多变
*	可以使用File的方法来对父路径进行处理
*/
```

#### 4.常用方法

##### 1.获取功能的方法

```java
/**获取功能的方法
*1.String getAbsolutePath()
*2.String getPath()
*3.String getName()
*4.Long length()
**/

/**getAbsolutePath()
*获取构造方法中传递的路径，无论是相对路径还是绝对路径，都返回绝对路径
**/

/**getPath()
*获取构造方法中传递的路径，返回的路径类型则取决于构造方法中的路径，传递的是绝对路径*则返回绝对路径，相对路径则返回相对路径
*/

/**getName()
*获取路径的目录名或文件名，获取的是路径最后一节的名字
**/

/**length()
*获取文件的大小，如果路径不存在或是文件夹则返回0，
**/
```

##### 2.判断功能的方法

```java
/**判断功能的方法
*1.boolean exists()
*2.boolean isDirectory
*3.boolean isFile
**/

/**File.exists()
*用于判断构造方法中的路径是否存在，存在则返回true，不存在返回false
*/

/**File.idDirectoy()
*用于判断构造方法中的路径所指是否为目录
*/

/**File.isFile()
*用户判断构造方法中路径所指的是否是文件
*/
```

##### 3.创建和删除功能的方法

```java
/**创建和删除功能的方法
*1.boolean createNewFile()
*2.boolean mkdir()
*3.boolean mkdirs()
*4.boolean delete()
*/

/**createNewFile()
*用于创建路径所指的文件
*注意：
*1.路径不存在抛出异常
*2.文件已存在返回false 
*3.文件创建成功返回true
*/

/**mkdir()
*用于创建单极目录，也就是最后一级目录
*注意：
*1.当路径不存在或目录已存在时时返回false
*2.当目录不存在且成功创建时返回true
*/

/**mkdirs()
*用于创建多级目录
*/

/**delete()
*用于删除构造方法中所指的文件或目录
*注意：delete方法是直接删除的硬盘上的文件，不会进入回收站
*/
```

##### 4.遍历功能的方法

```java
/**遍历功能的方法
*String[] list()
*File[] listFiles()
*/

/**list()
*获取构造方法所指的目录下的子目录以及文件的名称放到字符串数组中
*注意：
*1.当路径不存在时会报空指针异常
*2.当路径所指的不是目录时会报空指针异常
*/

/**listFiles()
*获取构造方法所指的目录下的子目录以及文件作为File实例放到文件数组中
*/
```

#### 5.文件过滤器

```java
package com.company.File;

/**
 * File[] listFiles(FileFilter filter)
 * FileFilter:      java.io.FileFilter接口：用于抽象路径名（file对象）的过滤器
 *      ：过滤文件
 *      ：抽象方法----》boolean accept(file pathname)
 *
 *
 * File[] listFiles(FilenameFilter filter)
 * FilenameFilter:  java.io.FilenameFilter
 *      ：过滤文件名称
 *      ：抽象方法----》boolean accept(File dir,String name)
 *
 * 注意：两个过滤器都没有实现类，需要我们自己写实现类，重写过滤的方法accept
 * */


import java.io.File;
import java.io.FileFilter;

/**
 * 实现过滤器接口，重现accept方法，定义过滤规则
 * */
public class MyFileFilter implements FileFilter {
    @Override
    public boolean accept(File pathname) {
        if(pathname.getName().toString().endsWith(".png")){
            System.out.println(1);
            return false;
        }
        return true;
    }
}


/**
 * listFiles所做的三件事：
 * 1.listFiles会对传递的目录进行遍历，然后将目录中的每一个文件/文件夹封装为一个File对象
 * 2.listFiles会调用参数传递的过滤器的accept方法
 * 3.listFiles会将封装的File传递给pathname
 * */

/**accept方法，accept方法返回的是一个布尔值
 * true：会将封装的File对象保存到File数组中去
 * false：不会将封装的File对象保存到File数组中去
 * */


package com.company.File;

import java.io.File;

/**
 * 文件搜索
 * */
public class FileSearch {
    public static void main(String[] args) {
        File file = new File("C://Users/PJM");
        if(file.isDirectory()){
            filePrint(file.listFiles(new MyFileFilter()));
        }
    }

    public static void filePrint(File[] files){
        for(File file : files){
            if(file.isDirectory()){
                filePrint(file.listFiles(new MyFileFilter()));
            } else {
                if(file.getName().endsWith(".png")){
                    System.out.println(file.getAbsoluteFile());
                }
            }
        }
    }
}
```

### 二、IO

```java
/**
*Input(读入)
*output(写出)
*数据流(字节，字符) 1字符 = 2字节 = 8位
*/

/**顶层流
*字节：OutputStream、InputStream
*字符：Reader、Writer
*/
```

#### 1.字节输出流(OutputStream)

```Java
/*******输出流：OutputStream*********/

/**
*OutputStream：所有字节输出流类的超类，是一个抽象类，定义了共性方法
*    void	close()
*    关闭此输出流并释放与此流相关联的任何系统资源。
*    void	flush()
*    刷新此输出流并强制任何缓冲的输出字节被写出。
*    void	write(byte[] b)
*    将 b.length字节从指定的字节数组写入此输出流。
*    void	write(byte[] b, int off, int len)
*    从指定的字节数组写入 len个字节，从偏移 off开始输出到此输出流。
*    abstract void	write(int b)
*    将指定的字节写入此输出流。
*/

/**
*FileOutputStream：文件字节输出流，OutputStream的子类，
*构造方法：
	FileOutputStream(File file)
    	创建文件输出流以写入由指定的 File对象表示的文件。
    FileOutputStream(String name)
    
数据写出的过程：
Java程序---->JVM---->OS(操作系统)---->OS调用写入文件的方法---->把数据写入到文件中去
*/

/**步骤:
*1.创建写出到文件的字节输出流FileOutputStream
*2.使用方法write将数据写入到目的文件
*3.使用close方法释放资源清空内存
*/

package com.company.FileOutput;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutput {
    public static void main(String[] args) throws IOException {
        File file = new File("a.txt");
        FileOutputStream fos = new FileOutputStream(file);
        fos.write(77);
        fos.close();
    }
}
/**构造方法的三个作用：
*1.创建一个FileOutputStream对象
*2.会根据构造方法中传递过来的文件/文件路径，创建一个空的文件
*3.会把FileOutputStream对象指向创建好的文件
*/




/***追加写***/
/**
FileOutputStream(String name, boolean append)
创建文件输出流以指定的名称写入文件。
FileOutputStream(File file, boolean append)
创建文件输出流以写入由指定的 File对象表示的文件。

append：追加写开关！
换行符号：
	Windows：\r\n
	Linux:/n
	max:/r
**/

```

#### 2.字节输入流(InputStream)

```java
/*******输入流：InputStream*********/

/**InputStream：所有字节输入流类的超类，是一个抽象类，定义了共性方法
	close()
		关闭此输入流并释放与流相关联的任何系统资源。
	read()
		从输入流读取数据的下一个字节。
	read(byte[] b)
		从输入流读取一些字节数，并将它们存储到缓冲区 b 。
**/

/**FileInputStream：
	java.io.InputStream extends InputStream
构造方法：
    FileInputStream(File file)
    	通过打开与实际文件的连接创建一个 FileInputStream ，该文件由文件系统中的 File对象 file命名。
    FileInputStream(String name)
		通过打开与实际文件的连接来创建一个 FileInputStream ，该文件由文件系统中的路径名 name命名。
		
构造方法所做的事：
	1.会创建一个FileInputStream对象
	2.会将FileInputStream对象指向传递过来的文件
	
	
注意：1.当读取到文件末尾时会返回-1


read(byte[] b)：b为读取到的字节，其长度则为所需要读取的字节个数，且返回的值为一次读取到的有效个数
read()：无参，返回值为所读取到的字节
**/

package com.company.FileInput;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.util.Arrays;

public class FileInput {
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream(new File("b.txt"));
//        Integer name = fis.read();
//        System.out.println(name);

        Integer name;
        byte [] bytes = new byte[20];
//        while((name = fis.read(bytes)) != -1){
//            System.out.println(name);
//        }
        name = fis.read(bytes);
        System.out.println(Arrays.toString(bytes));
		System.out.println(new String(bytes));				//将字节数组转为字符串

        name = fis.read(bytes);
        System.out.println(Arrays.toString(bytes));
        System.out.println(name);
        fis.close();
    }
}
/**读取：
Java程序----》JVM----》OS----》OS调用读取文件的方法----》读取文件
**/
```

#### 3.字符输入流(Reader)

```java
/**
*注意：在使用字节流读取文件时会用中文乱码问题，而使用字符流则不会
**/

/**
*Reader：是一个抽象类，定义了所有子类的共性方法
    read()
    	读一个字符
    read(char[] cbuf)
		将字符读入数组。
	read(char[] cbuf, int off, int len)
		将字符读入数组的一部分。
	close()
		关闭流并释放与之相关联的任何系统资源。
*/
/**子类：FileReader
*构造方法：
	FileReader(File file)
		创建一个新的 FileReader ，给出 File读取。
	FileReader(String fileName)
		创建一个新的 FileReader ，给定要读取的文件的名称。
*/
package com.company.FileReader;

import java.io.File;
import java.io.FileReader;
import java.io.IOException;

public class MyFileReader {
    public static void main(String[] args) throws IOException {
        File file = new File("b.txt");
        FileReader reader = new FileReader("a.txt");

        int len;
        char [] chars = new char[1024];
        while ((len = reader.read(chars)) != -1) {
            System.out.println(new String(chars,0,len));
        }

        reader.close();
    }
}


```

#### 4.字符输出流(Writer)

```java
/**Writer:抽象类，字符输出流的超类，定义了所有子类的共性方法
*方法：
	close()
		关闭流，先刷新。
	write(int c)
		写一个字符
	write(char[] cbuf, int off, int len)
		写入字符数组的一部分。
	write(char[] cbuf)
		写入一个字符数组。
	write(String str)
		写一个字符串
	write(String str, int off, int len)
		写一个字符串的一部分。
	flush()
		刷新流。
*/

/**FileWriter：文件字符输出流，将内存中地字符写入到文件中
*构造方法：
	FileWriter(File file)
		给一个File对象构造一个FileWriter对象。
	FileWriter(File file, boolean append)
		给一个File对象构造一个FileWriter对象。
	FileWriter(String fileName)
		构造一个给定文件名的FileWriter对象。
	FileWriter(String fileName, boolean append)
		构造一个FileWriter对象，给出一个带有布尔值的文件名，表示是否附加写入的数据。
*/

/**字符输出流的使用步骤：
*1.创建FileWriter对象，构造方法绑定要写入数据的目的地
*2.使用FileWriter对象的write方法，把数据写入到数据缓冲区去（字符转换为字节的过程）
*3.使用FileWrite对象的flush方法，把内存缓冲区的数据刷新的文件中去
*4.释放资源(会先把内存缓存区的数据刷新到文件中去)
*/
package com.company.MyFileWriter;

import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

public class MyFileWriter {
    public static void main(String[] args) throws IOException {
        File file = new File("c.txt");
        FileWriter writer = new FileWriter(file,true);

        String c = "你是傻逼";
        writer.write(c);

        writer.close();
    }
}
/**
*close方法：刷新缓冲区，然后通知系统释放资源，流就不可以再使用了
*flush方法：刷新缓冲区，流还可以继续使用
*/

```

