## 文件操作（File类和IO流）

### 一、FIle类

### 1.静态变量

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

### 2.路径

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

### 3.构造方法

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

### 4.常用方法

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

