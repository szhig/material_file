## Spring Boot

### 一、基础

```Java
/*创建Spring boot项目*/
/**创建Spring Boot工程
 * 1.idea联网创建,默认从spring官网下载：https://start.spring.io
 * 2.spring官网创建：
 *      Project---》Spring Boot ---》Spring Initializr ---》 Generate
 * 3.阿里云创建：
 *      创建时，将网址改为阿里云：https://start.aliyun.com
 * */
```

#### 1.Spring Boot从创建到运行

##### 1.Maven过程改Spring boot工程

```xml
<!--1.添加spring boot父依赖-->
<parent>
    <artifactId>spring-boot-starter-parent</artifactId>
    <groupId>org.springframework.boot</groupId>
    <version>2.6.4</version>
</parent>
```

```java
/*添加引导类*/
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(Application.class);
        System.out.println(context.APPLICATION_STARTUP_BEAN_NAME);
    }
}

/**引导类：
 * 1.@SpringBootApplication注解
 * 2.使用SpringApplication的静态方法run将引导类的字节码文件传入进去，作为上下文对象
 * */
```

##### 2.隐藏文件或文件夹

```
File ---》 Editor ---》 File Types ---》 Ignored File and Folders
```

##### 3.依赖

```xml
<!--spring boot的依赖都会由spring-boot-starter-parent来做统一依赖版本号管理-->
<parent>
    <artifactId>spring-boot-starter-parent</artifactId>
    <groupId>org.springframework.boot</groupId>
    <version>2.6.4</version>
</parent>

<!--
    通过查看spring-boot-starter-parent可以看出，在spring-boot-starter-parent中有导入了一个父依赖spring-boot-dependencies，
    而在spring-boot-dependencies中做了很多依赖的版本号管理,也就是说，在使用Spring boot导入依赖时并不需要去写版本号，在spring-boot-dependencies中做了统一版本号管理
-->
```

##### 4.启动器(starter)

```java
/**/
```

##### 5.引导类：

```java
/*
	注解：@SpringBootApplication和SpringBootApplication类：
	SpringBootApplication：
		org.springframework.boot.SpringApplication		属于：spring-boot依赖
	@SpringBootApplication注解：
		org.springframework.boot.autoconfigure.SpringBootApplication	属于：spring-boot-autoconfigure依赖
	
	而在spring-boot-starter启动器中包括了这两个依赖
	spring-boot-starter启动器又被包含在spring-boot-starter-web启动器中
	
	关于tomcat服务器：在spring-boot-starter-web中包含了tomcat的启动器：spring-boot-starter-tomcat
	
	spring-mvc依赖：spring-web
	
	
*/
```

##### 6.更换服务器

```xml
<!--先排除Tomcat服务器，在导入Jetty服务器-->
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-tomcat</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jetty</artifactId>
    </dependency>
</dependencies>

<!--Spring Boot支持的三种内置服务器：
	1.Tomcat
	2.Jetty
	3.Undertow
-->
```

#### 2.REST开发

```java
/**REST：表现形式状态转换
 *  优点：隐藏资源的访问形式，书写简化
 *      REST风格通过不同的请求方式区分对资源的操作
 * */

/**四种请求方式
1.GET：
	传参：parame(路径参数)
		/users/{id}
	接收
		修饰符 返回值 方法名(@PathVariable Integer id)
2.POST
3.PUT
4.DELETE
*/

/**接收参数注解：
	1.@ReqeustBody：接json参数
	2.@ReqeustParam：接url参数
	3.@PathVariable：接路径参数
*/
```

#### 3.配置

##### 1.属性配置方式

```properties
#Spring Boot默认配置文件：application.properties

#修改端口号
server.port = 8088
#修改banner：logo
spring.main.banner-mode=console
spring.banner.image.location=box.png

#日志类型的级别
logging.level.sql = info

#查看Application.properties所有配置：官网 ---》 Project ---》 Spring Boot ---》 LEARN ---》 Reference Doc. ---》 Application.properties
#里面包括了application.properties中所有的配置
```

##### 2.配置文件格式

```java
/**配置文件格式：
 * 1.properties
 * 2.yml
 * 3.yaml
 *
 * 注：三种格式共存，优先级由properties ---》 yml ---》 yaml
 * */
```

