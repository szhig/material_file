## Java错误

### 一、Mybatis映射错误

1.No serializer found for class com.example.smartcity.job.model.Recruit and no properties discovered to create BeanSerializer

原因：没有set方法

解决：添加set方法



2.Error resolving JdbcType. Cause: java.lang.IllegalArgumentException: No enum constant org.apache.ibatis.type.JdbcType.DATETIME

原因：Java和数据库的数据类型映射错误，

解决：将DATETIME改为DATE就行



3.Result Maps collection already contains value for com.example.smartcity.activity.mapping.ActivitySlideshowMapper.BaseResultMap

原因：结果集中属性错误

解决：将结果集的属性改正



4.Invalid bound statement (not found): com.example.smartcity.activity.mapping.ActivityMapper.find

原因：mapper文件和java接口映射错误

解决：将mapper的命名空间或sql标签的方法名更改，或者调整mapper文件的位置



5.Unsupported conversion from LONG to java.sql.Timestamp

原因：数据库和bean的数据类型转换错误

解决：改变数据库或bean的数据类型



### 二、spring boot整合swagger错误

1.Failed to start bean 'documentationPluginsBootstrapper';

解决：

```java
package com.example.smartcity.config;


import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurationSupport;

@Configuration
public class ServletWebMvcConfig extends WebMvcConfigurationSupport {
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/**").addResourceLocations(
                "classpath:/static/");
        registry.addResourceHandler("swagger-ui.html").addResourceLocations(
                "classpath:/META-INF/resources/");
        registry.addResourceHandler("/webjars/**").addResourceLocations(
                "classpath:/META-INF/resources/webjars/");
        super.addResourceHandlers(registry);
    }
}

```

