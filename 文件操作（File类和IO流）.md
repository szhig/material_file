## 文件操作（File类和IO流）

javaAPI文档地址：https://www.matools.com/api/java8

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

#### 5.Properties类

```java
/**Properties**/
/**	java.util.Properties集合 extends Hashtable<k,v> implements Map<k,v>
 *	Properties类表示一组持久的属性。 Properties可以保存到流中或从流中加载。 属性列表中的每个键及其对应的值都是一个字符串。
 *	Properties是唯一一个与IO流相结合的集合：
 *		可以使用Properties集合中的方法store，把集合中的临时数据，持久化写入到硬盘中存取
 *		可以使用Properties集合中的方法load，把硬盘中保存的文件（键对值），读取到集合中使用
 *	属性列表中每个键所对的值都是字符串。
 *		Properties集合是一个双列集合，key和value都是字符串。
 */

/**Properties操作属性列表的特有方法：
 * 	setProperty(String key, String value)
 * 		调用Hashtable的方法 put 。
 * 	getProperty(String key)
 * 		使用此属性列表中指定的键搜索属性。
 * 	getProperty(String key, String defaultValue)
 * 		使用此属性列表中指定的键搜索属性，通过key找到value值，相当于Map集合中的get方法。
 * 	stringPropertyNames()
 * 		返回此属性列表中的一组键，其中键及其对应的值为字符串，包括默认属性列表中的不同键，如果尚未从主属性列表中找到相同名称的键,返回一个包含所有键的Set列表。
 * 		相当于Map集合中的keyset方法	
 * */

@Test
void testProperties() throws Exception {
    Properties prop = new Properties();
    Properties prop = new Properties();
    prop.setProperty("dataOne","张三");
    prop.setProperty("dataTwo","李四");
    prop.setProperty("dataThree","王五");
    Set<String> sets = prop.stringPropertyNames();
    for (String set:sets){
        System.out.println(set);
    }
}
```

#### 6.持久化Properties集合

```Java
/**store方法**/
/**持久化Properties：使用Properties集合中的方法store将Properties集合从内存中存入到硬盘中：
 * 	store(OutputStream out, String comments)
 * 		将此属性列表（键和元素对）写入此 Properties表中，以适合于使用 load(InputStream)方法加载到 Properties表中的格式输出流。
 * 	store(Writer writer, String comments)
 * 		将此属性列表（键和元素对）写入此 Properties表中，以适合使用 load(Reader)方法的格式输出到输出字符流。
 *
 * 	OutputStream out：以字节流写入到硬盘中，不能输入中文
 * 	Writer writer：以字符流写入到硬盘中，可以输入中文
 * 	comments：注释。
 *
 * 	使用步骤：
 * 		1.创建Properties集合对象，添加数据
 * 		2.创建字符输出流/字节输出流对象
 * 		3.使用Properties集合中的store方法，持久化写入到硬盘中存储
 * 		4.释放资源
 * */
@Test
void addProperties() throws Exception{
    Properties prop = new Properties();
    prop.setProperty("dataOne","张三");
    prop.setProperty("dataTwo","李四");
    prop.setProperty("dataThree","王五");

    FileWriter fis = new FileWriter("src/main/resources/application.properties",true);

    prop.store(fis,"saveData");
    fis.close();
}
```

#### 7.读取为Properties集合

```java
/**读取为Properties集合
 * 	可以使用Properties集合中的方法load，把硬盘中保存的文件（键对值），读取到集合中使用
 * 	load(InputStream inStream)
 * 		从输入字节流读取属性列表（键和元素对）。
 *	load(Reader reader)
 * 		以简单的线性格式从输入字符流读取属性列表（关键字和元素对）。
 *
 * 参数：
 * 		InputStream：以字节流读入到Properties结合对象中，不能读取含有中文的键值对
 * 		Reader reader：以字符流读入到Properties集合对象中，能读取含有中文的键值对
 *
 * 	使用步骤：
 * 		1.创建Properties集合对象
 * 		2.创建字符输入流/字节输入流对象
 * 		3.使用Properties集合中的load方法，读取保存键值对的文件
 * */
@Test
void testProperties() throws Exception {
    Properties prop = new Properties();
    FileReader reader = new FileReader("src/main/resources/application.properties");
    prop.load(reader);
    Set<String> sets = prop.stringPropertyNames();
    for (String set:sets){
        System.out.println(set + "=" + prop.getProperty(set));
    }
}
```

### 三、缓冲流

```java
//缓冲流在基本流的基础上创建的
```

#### 1.字节缓冲输入流(BufferedOutputStream)

```java
/**字节缓冲输出流：BufferedOutputStream
 * 给基本的字节输出流增加了一个缓冲区(数组)提高了基本的字节输出流的读取效率
 * BufferedOutputStream(new FileOutputStream())
 * 
 * java.io.BufferedOutputStream extends java.io.FilterOutputStream implements java.io.OutputStream
 *
 * 继承自父类的共性方法：
 * 	void close()
 * 		关闭此输出流并释放与此流相关联的任何系统资源。
 * 	void flush()
 * 		刷新此输出流并强制任何缓冲的输出字节被写出。
 * 	void write(byte[] b)
 * 		将 b.length字节从指定的字节数组写入此输出流。
 *	void write(byte[] b, int off, int len)
 * 		从指定的字节数组写入 len个字节，从偏移 off开始输出到此输出流。
 * 	abstract void write(int b)
 * 		将指定的字节写入此输出流。
 * */

/**构造方法：
 *	BufferedOutputStream(OutputStream out)
 * 		创建一个新的缓冲输出流，以将数据写入指定的底层输出流。
 * 	BufferedOutputStream(OutputStream out, int size)
 * 		创建一个新的缓冲输出流，以便以指定的缓冲区大小将数据写入指定的底层输出流。
 *
 * 	参数：
 * 		OutputStream out：字节输出流
 *		int size：指定缓冲流内部缓冲区的大小，不指定默认：1024
 * */

package com.company.Buffered;

import java.io.BufferedOutputStream;
import java.io.FileOutputStream;

public class BufferedFileOutputStream {
    public static void main(String[] args) throws Exception{
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("a.txt"));
        bos.write("我嫩爹".getBytes());
        bos.close();
    }
}

```

#### 2.字节缓冲输出流(BufferedInputStream)

```java
/**字节缓冲输出流：BufferedInputStream**/
/**字节缓冲输出流：BufferedInputStream
 * 给基本的字节输入流增加了一个缓冲区(数组)提高了基本的字节输入流的读取效率
 * BufferedOutputStream(new FileOutputStream())
 * 
 * java.io.BufferedOutputStream extends java.io.FileInputStream implements java.io.InputStream
 *
 * 继承自父类的共性方法：
*	close()
*		关闭此输入流并释放与流相关联的任何系统资源。
*	read()
*		从输入流读取数据的下一个字节。
*	read(byte[] b)
*		从输入流读取一些字节数，并将它们存储到缓冲区 b 。
* */

/**构造方法：
 *	BufferedInputStream(InputStream in)
 * 		创建一个 BufferedInputStream并保存其参数，输入流 in ，供以后使用。
 * 	BufferedInputStream(InputStream in, int size)
 * 		创建 BufferedInputStream具有指定缓冲区大小，并保存其参数，输入流 in ，供以后使用。
 *
 * 	参数：
 *  	OutputStream out：字节输出流
 *  	int size：指定字节输入缓冲流内部的缓冲区大小，不指定默认
 * */
package com.company.Buffered;

import java.io.BufferedInputStream;
import java.io.FileInputStream;
import java.util.Arrays;

public class MyBufferedInputStream {
    public static void main(String[] args) throws Exception{
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream("a.txt"));
        byte [] bytes = new byte[20];
        int len = bis.read(bytes);
        System.out.println(new String(bytes,0,len));
        System.out.println(len);
        bis.close();
    }
}

```

```java
/**同一文件复制**/
//普通流：复制文件共耗时：1178毫秒
//缓冲流：复制文件所消耗的时间：272毫秒
//程序：普通流
package com.company.File;

import java.io.FileInputStream;
import java.io.FileOutputStream;

public class FileCopy {
    public static void main(String[] args) throws Exception{
        long s = System.currentTimeMillis();
        FileInputStream fis = new FileInputStream("jdk.zip");

        FileOutputStream fos = new FileOutputStream("new.zip");

        Integer len;
        byte [] bytes = new byte[1024];
        while((len = fis.read(bytes)) != -1){
            fos.write(bytes,0,len);
        }
        fos.close();
        fis.close();
        long e = System.currentTimeMillis();
        System.out.println(e);
        System.out.println("复制文件共耗时："+(e-s)+"毫秒");
    }
}

//缓冲流：
package com.company.Buffered;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;

public class BufferedCopy {

    public static void main(String[] args) throws Exception{
        long s = System.currentTimeMillis();
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream("jdk.zip"));
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("new.zip"));
        int len = 0;
        byte [] bytes = new byte[1024];
        while ((len = bis.read(bytes)) != -1){
            bos.write(bytes,0,len);
        }
        bis.close();
        bos.close();
        long e = System.currentTimeMillis();
        System.out.println("复制文件所消耗的时间："+(e-s)+"毫秒");
    }
}

```

#### 3.字符缓冲输入流(BufferedReader)

```java
/**字符缓冲输入流：BufferedReader**/
/**字符缓冲输入流：BufferedReader
 * 给基本的字符输入流增加了一个缓冲区(数组)提高了基本的字符输入流的读取效率
 * BufferedReader(new FileReader())
 * 
 * java.io.BufferedReader extends java.io.FileReader implements java.io.Reader
 *
 * 继承自父类的共性方法：
 *方法：
 *	read()
 *   	读一个字符
 *   read(char[] cbuf)
 *		将字符读入数组。
 *	read(char[] cbuf, int off, int len)
 *		将字符读入数组的一部分。
 *	close()
 *		关闭流并释放与之相关联的任何系统资源。
 */

/**构造方法：
 *  BufferedReader(Reader in)
 *      创建使用默认大小的输入缓冲区的缓冲字符输入流。
 *  BufferedReader(Reader in, int sz)
 *      创建使用指定大小的输入缓冲区的缓冲字符输入流。
 *
 *  参数：
 *      Writer out：字符输出流
 *      int size：用于指定字符缓冲输出流内部的缓冲区大小，不指定默认
 *
 *  特有方法：
 *      readLine()
 *          读一行文字,如果达到流的末尾返回null。
 * */
package com.company.Buffered;

import java.io.BufferedReader;
import java.io.FileReader;

public class BufferedFileReader {
    public static void main(String[] args) throws Exception{
        BufferedReader reader = new BufferedReader(new FileReader("d.txt"));
        char [] chars = new char[1024];
        String line = "";
//        System.out.println(new String(chars,0,len));
//        System.out.println(len);
//        System.out.println(line);
        while ((line = reader.readLine()) != null){
            System.out.println(line);
        }
        reader.close();
    }
}

```



#### 4.字符缓冲输出流(BufferedWriter)

```java
/**字符缓冲输出流：BufferedWriter**/
/**字符缓冲输出流：BufferedWriter
 * 给基本的字符输出流增加了一个缓冲区(数组)提高了基本的字符输出流的读取效率
 * BufferedWriter(new FileWriter())
 * 
 * java.io.BufferedWriter extends java.io.FileWriter implements java.io.Writer
 *
 * 继承自父类的共性方法：
 *方法：
 *	close()
 * 		关闭流，先刷新。
 *	write(int c)
 *		写一个字符
 *	write(char[] cbuf, int off, int len)
 *		写入字符数组的一部分。
 *	write(char[] cbuf)
 *		写入一个字符数组。
 *	write(String str)
 *		写一个字符串
 *	write(String str, int off, int len)
 *		写一个字符串的一部分。
 *	flush()
 *		刷新流。
 */

/**构造方法：
 *  BufferedWriter(Writer out)
 *      创建使用默认大小的输出缓冲区的缓冲字符输出流。
 *  BufferedWriter(Writer out, int sz)
 *      创建一个新的缓冲字符输出流，使用给定大小的输出缓冲区。
 *
 *  参数：
 *      Writer out：字符输出流
 *      int size：用于指定字符缓冲输出流内部的缓冲区大小，不指定默认
 *
 *  特有方法：
 *      newLine()
 *          写一行行分隔符，会根据不同的操作系统，获取不同的换行符。
 */

package com.company.Buffered;

import java.io.BufferedWriter;
import java.io.FileWriter;

public class BufferedFileWriter {
    public static void main(String[] args) throws Exception{
        BufferedWriter writer = new BufferedWriter(new FileWriter("d.txt"));
        String s = "我嫩爹";
        writer.write(s);
        writer.close();
    }
}

```

### 四、转换流

#### 1.字符编码和字符集

```java
/**字符编码：就是一套自然语言的字符与二进制数之间的对应规则
 *  编码：按照某种规则将字符存储到计算机中，称为编码
 *  解码：将计算机中的二进制按照某种规则解析显示出来，称为解码
 *  编码表：生活中文字和计算机中二进制的对应规则
 *
 *  字符集：也叫编码表
 * */


```

#### 2.编码引起的问题

```java
/**编码引起的问题
 *  当使用FileReader字符流读取文件时，如果文件是IDE的默认编码方式不会有问题，
 *  而当读取的文件的编码方式与IDE的编码方式不同时，读取文件就会有乱码问题
 *
 *  字节的读取是没有编码问题的，主要是字符的读取
 * */


```

#### 3.转换流

##### 1.InputStreamReader

```java
/*
阅读字符文件的便利课。 该类的构造函数假定默认字符编码和默认字节缓冲区大小是适当的。 要自己指定这些值，请在FileInputStream上构造一个InputStreamReader。
注意：在FileReader的底层源码实际用的还是FileInputStream来读取文件，FileInputStream将文件以字节的方式读出后，再通过FileReader将字节转换为字符
*/

/**InputStreamReader
 *  InputStreamReader是字符的桥梁流以字节流：向其写入的字符编码成使用指定的字节charset 。 它使用的字符集可以由名称指定，也可以被明确指定，或者可以接受平台的默认字符集。
 *  可以指定编码表，也就是解码的方式
 *
 * java.io.InputStreamReader 是 Reader的子类 implements java.io.Reader
 * 可以使用Reader的共性方法：
 * 方法：
 *       read()
 *           读一个字符
 *       read(char[] cbuf)
 *           将字符读入数组。
 *       read(char[] cbuf, int off, int len)
 *           将字符读入数组的一部分。
 *       close()
 *           关闭流并释放与之相关联的任何系统资源。
 *
 *  构造方法:
 *      InputStreamReader(InputStream in)
 *			创建一个使用默认字符集的InputStreamReader。
 *      InputStreamReader(InputStream in, String charsetName)
 *			创建一个使用命名字符集的InputStreamReader。
 * */
package com.company.transform;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class Transform {
    public static void main(String[] args) throws Exception{

        char [] chars = new char[1024];
        InputStreamReader isr = new InputStreamReader(new FileInputStream("a.txt"),"GBK");
        int len = isr.read(chars);
        System.out.println(new String(chars,0,len));


//        OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("a.txt"),"GB2312");
//        osw.write("我嫩爹");
//        osw.close();
    }
}
```

##### 2.OutputStreamWriter

```java
/**OutputStreamWriter
 *  OutputStreamWriter是字符的桥梁流以字节流：向其写入的字符编码成使用指定的字节charset 。 它使用的字符集可以由名称指定，也可以被明确指定，或者可以接受平台的默认字符集。
 *  可以指定编码表，也就是编码的方式
 *
 * java.io.OutputStreamWriter 是 Writer的子类 implements java.io.Writer
 * 可以使用Writer的共性方法：
 * 方法：
 *       close()
 *		关闭流，先刷新。
 *	write(int c)
 *		写一个字符
 *	write(char[] cbuf, int off, int len)
 *		写入字符数组的一部分。
 *	write(char[] cbuf)
 *		写入一个字符数组。
 *	write(String str)
 *		写一个字符串
 *	write(String str, int off, int len)
 *		写一个字符串的一部分。
 *	flush()
 *		刷新流。
 *
 *  构造方法:
 *      OutputStreamWriter(OutputStream out)
 *          创建一个使用默认字符编码的OutputStreamWriter。
 *      OutputStreamWriter(OutputStream out, String charsetName)
 *          创建一个使用命名字符集的OutputStreamWriter。
 * */

package com.company.transform;

import java.io.FileOutputStream;
import java.io.OutputStreamWriter;

public class Transform {
    public static void main(String[] args) throws Exception{
        OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("a.txt"),"GB2312");
        osw.write("我嫩爹");
        osw.close();
    }
}
```

### 五、序列化与反序列化

```java
/**序列化与反序列化
 * 序列化：简单来说就是将一个对象存储到文件中去
 * 反序列化：反序列化则是将文件中的对象读取出来
 * */

/**
* 对象的序列化流：ObjectOutputStream
* 对象的反序列化流：ObjectInputStream
*/

```

#### 1.序列化(ObjectOutputStream)

```java
/**java.io.ObjectOutputStream**/
/**
 * java.io.ObjectOutputStream 继承自 OutputStream
 * 同样的，继承了OutputStream的共性方法
 *
 * 作用：把对象以流的方式写入到文件中去
 *
 * 构造方法：
 * 		ObjectOutputStream()
 * 			为完全重新实现ObjectOutputStream的子类提供一种方法，不必分配刚刚被ObjectOutputStream实现使用的私有数据。
 * 		ObjectOutputStream(OutputStream out)
 * 			创建一个写入指定的OutputStream的ObjectOutputStream。
 *
 * 	参数：
 * 		OutputStream out：一个字节输出流对象
 *
 * 	特有方法：
 * 		writeObject(Object obj)
 * 			将指定的对象写入ObjectOutputStream。
 * */

/**
 * public class NotSerializableException
 * extends ObjectStreamException
 * 抛出一个实例需要一个Serializable接口。 序列化运行时或实例的类可能会抛出此异常。 参数应该是类的名称。
 * */

/**
 * public interface Serializable
 * 类的序列化由实现java.io.Serializable接口的类启用。
 * */
package com.company.object;

import com.company.model.Person;

import java.io.FileOutputStream;
import java.io.ObjectOutputStream;

public class FileObjectOutputStream {
    public static void main(String[] args) throws Exception {
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("g.txt"));
        oos.writeObject(new Person("小美女",18));
        oos.close();
    }
}

```



#### 2.反序列化(ObjectInputStream)

```java
/**java.io.ObjectInputStream**/
/**
 * java.io.ObjectInputStream 继承自 InputStream
 * 同样的，继承了InputStream的共性方法
 *
 * 作用：把对象以流的方式从文件中读取出来
 *
 * 构造方法：
 * 		ObjectInputStream(InputStream in)
 * 			创建从指定的InputStream读取的ObjectInputStream。
 *
 * 	参数：
 * 		InputStream in：一个字节输入流对象
 *
 * 	特有方法：
 * 		readObject()
 *			从ObjectInputStream读取一个对象。
 * */

/**
 * public class NotSerializableException
 * extends ObjectStreamException
 * 抛出一个实例需要一个Serializable接口。 序列化运行时或实例的类可能会抛出此异常。 参数应该是类的名称。
 * */

/**
 * public interface Serializable
 * 类的序列化由实现java.io.Serializable接口的类启用。
 * */

/**反序列化的前提：
 *  1.实体类必须实现Serializable接口
 *  2.必须存在类对应的class文件
 * */
package com.company.object;

import java.io.FileInputStream;
import java.io.InputStreamReader;
import java.io.ObjectInputStream;

public class FileObjectInputStream {
    public static void main(String[] args) throws Exception{
        FileInputStream fis = new FileInputStream("g.txt");
        InputStreamReader isr = new InputStreamReader(fis,"GBK");
        ObjectInputStream ois = new ObjectInputStream(fis);
        Object obj = ois.readObject();
        System.out.println(obj.toString());
        ois.close();
    }
}
```

#### 3.InvalidClassException异常

![Screenshot_2022-03-12-16-20-13-613_tv.danmaku.bil](http://r9adeaai2.hn-bkt.clouddn.com/img/Screenshot_2022-03-12-16-20-13-613_tv.danmaku.bil.jpg)

```java
/**反序列化异常：InvalidClassException序列化号冲突异常**/
/*
	问题：由于实现了接口Serializable接口，当进行序列化时，会给实体类一个序列号，而当序列化完成时，该序列号也会写入到文件中；反序列化时，会将实体类的序列号和文件中的序列号进行匹对，如果在反序列化时修改了类文件，则会重新编译，另外生成序列号，则会造成文件序列号和类文件的序列号不一致，从而引发InvalidClassException序列化号冲突异常
	
	解决：序列化运行时将每个可序列化的类与称为serialVersionUID的版本号相关联，该序列号在反序列化期间用于验证序列化对象的发送者和接收者是否已加载与该序列化兼容的对象的类。 如果接收方加载了一个具有不同于相应发件人类的serialVersionUID的对象的类，则反序列化将导致InvalidClassException 。 一个可序列化的类可以通过声明一个名为"serialVersionUID"的字段来显式地声明它自己的serialVersionUID，该字段必须是静态的，最终的，类型是long ：
	static final long serialVersionUID = 42L；
	手动在类文件中添加一个序列号
*/
```

#### 4.序列化集合

```java
/**序列化集合
 * 当我们想在文件中保存多个对象的时候
 * 可以把多个对象保存到一个集合中
 * 对集合进行序列化和反序列化
 *
 * 分析：
 *      1.定义一个存储对象的集合ArrayList
 *      2.往集合中添加对象
 *      3.创建序列化流ObjectOutputStream对象
 *      4.使用ObjectOutputStream对象中的方法writeObject，对集合进行序列化
 *      5.创建一个反序列化流ObjectInputStream对象
 *      6.使用ObjectInputStream对象中的方法readObject，对集合进行反序列化
 *      7.把Object类型转换为ArrayList类型
 *      8.对集合进行遍历
 *      9.释放资源
 * */

/**序列化集合**/
package com.company.object;

import com.company.model.Person;

import java.io.*;
import java.util.ArrayList;
import java.util.List;

public class CollectionObjectOutputStream {
    public static void main(String[] args) throws Exception{
        add();
    }

    public static void add() throws Exception {
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("h.txt"));
        Object obj = ois.readObject();
        ois.close();

        List<Person> people =  (ArrayList) obj;
        people.add(new Person("狗窝",18));

        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("h.txt"));
        oos.writeObject(people);
        oos.close();
    }
}

/**反序列化集合**/
package com.company.object;

import com.company.model.Person;

import java.io.FileInputStream;
import java.io.ObjectInput;
import java.io.ObjectInputStream;
import java.util.ArrayList;
import java.util.List;

public class CollectionObjectInputStream {
    public static void main(String[] args) throws Exception{
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("h.txt"));
        Object obj = ois.readObject();
        ois.close();

        List<Person> people =  (ArrayList) obj;
        for (Person person : people){
            System.out.println(person.toString());
        }

        people.add(new Person("狗窝",18));
    }
}

```

### 六、打印流(PrintStream)

```java
/**打印流：PrintStream
 * 打印流可以将输出语句输出到文件中去
 *
 * java.io.PrintStream 继承自 OutputStream
 * 继承类OutputStream的共性方法：
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
 *
 *
 * 构造方法：
 *  PrintStream(OutputStream out)
 *      创建一个新的打印流。
 *  PrintStream(String fileName)
 *      使用指定的文件名创建新的打印流，无需自动换行。
 *  PrintStream(String fileName, String csn)
 *      创建一个新的打印流，不需要自动换行，具有指定的文件名和字符集。
 *
 *  参数：
 *      OutputStream out：字节输出流
 *      String fileName:输出流的目的文件地址
 *      String csn：指定字符集
 *
 *  特有方法：
 *      print(任意数据类型)
 *      println(任意数据类型)
 *
 *
 *  注意：当使用共性方法和特有方法时会有差异
 *      使用共性方法时，输出到文件时会去查找编码表 97---》a
 *      使用特有方法则不会查找编码表  97----》97
 * */

import java.io.PrintStream;

public class FilePrintStream {

    public static void main(String[] args) throws Exception{
        PrintStream ps = new PrintStream(new FileOutputStream("i.txt"));
        ps.println("打印流");
        ps.write(97);
    }
}


/**
 * 改变输出语句的目的地(打印流的流向)
 * 输出语句，默认在控制台输出
 * 使用System.setOut方法改变输出语句的目的地为参数中传递的打印流目的地
 *      setOut(PrintStream out)
 *          重新分配“标准”输出流。
 * */
package com.company.print;

import java.io.FileOutputStream;
import java.io.PrintStream;

public class FilePrintStream {

    public static void main(String[] args) throws Exception{
        System.out.println("我在控制台打印");

        PrintStream ps = new PrintStream(new FileOutputStream("j.txt"));
        System.setOut(ps);
        System.out.println("我在文件中打印");
    }
}
```

### 七、前后端文件上传

```java
package com.example.smartcity.utils;

import org.apache.commons.codec.binary.Base64;

import java.io.*;
import java.util.Random;

public class FileRename {
    //文件命名
    public static String rename(String data){
        String fileName = "upload" + System.currentTimeMillis() + new Random().nextInt(99999);
        String suffix = data.split(":")[1].split(";")[0];
        if ( suffix.equals("image/png") ){
            fileName += ".png";
        } else if(suffix.equals("image/jpeg")) {
            fileName += ".jpg";
        } else if(suffix.equals("application/octet-stream")){
            fileName += ".rar";
        } else if (suffix.equals("application/zip")){
            fileName += ".zip";
        } else if(suffix.equals("application/msword")){
            fileName += ".doc";
        }
        return suffix;
    }

    //文件转换输出
    public static void dataOut(String data,String filename){
        File file = new File(filename);
        if(file.exists()){
            try {
                file.createNewFile();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        OutputStream os = null;
        try {
            os = new FileOutputStream(file);
            os.write(Base64.decodeBase64(data));
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                os.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }
}

//前端将文件转为base64格式的字符串
//后端将base64字符串以base64的格式转为字节数组，再将字节数组输出
```

```js
var send = (data) => {
    var xhr = new XMLHttpRequest()
    xhr.open('post','http://192.168.1.6:8081/test/api/test/file')
    //方式一
    xhr.setRequestHeader('content-Type','application/json')
    xhr.send(JSON.stringify({
        bytes:data
    }))
    xhr.onload = (data) => {
        console.log(data);
        console.log(JSON.parse(xhr.responseText))
    }
}


var file = document.querySelector('.upload')		//获取文件输入框
file.onchange = (e) => {							
    var file = e.target.files[0]					//获取文件
    var fileReader = new FileReader()				//文件读取流
    fileReader.readAsDataURL(file)					//将文件以base64的格式读出
    fileReader.onload = () => {						//开始读取文件
        send(fileReader.result)
        console.log(byte += fileReader.result)
    }
}
```

