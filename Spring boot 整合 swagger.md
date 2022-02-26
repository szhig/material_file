## Spring boot 整合 swagger

### 1.导入依赖

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
```

### 2.配置文件

```java
package com.example.smartcity.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
public class SwaggerConfig{

    @Bean
    public Docket createRestApi() {
        return new Docket(DocumentationType.SWAGGER_2)
            .apiInfo(apiInfo())
            .select()
            .apis(RequestHandlerSelectors.basePackage("com.example.smartcity"))
            .paths(PathSelectors.any())
            .build();
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
            .title("智慧城市 API")
            .description("")
            .termsOfServiceUrl("http://blog.csdn.net/itguangit")
            .contact("itguang")
            .version("2.0")
            .build();
    }

}

```

### 3.解决Failed to start bean 'documentationPluginsBootstrapper';错误

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

### 4.swagger注解

##### 1.@APi



##### 5.问题

1.No mapping for GET /swagger-ui.html

原因：当程序中出现了继承自WebMvcConfigurationSupport的配置类则swagger的配置会失效，需要重新制定静态资源文件

```java
package com.example.smartcity.config;

import com.example.smartcity.interceptor.AdminInterceptor;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurationSupport;

@Configuration
public class InterceptorConfig extends WebMvcConfigurationSupport {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {

        InterceptorRegistration registration = registry.addInterceptor(new AdminInterceptor());
//        registration.addPathPatterns("/**");
        registration.addPathPatterns("/prod-api/api/takeout/address/list");
        registration.addPathPatterns("/prod-api/api/takeout/address");
        registration.addPathPatterns("/prod-api/api/takeout/address/change");
        registration.addPathPatterns("/prod-api/api/takeout/order/create");
        registration.addPathPatterns("/prod-api/api/takeout/collect");
        registration.addPathPatterns("/prod-api/api/takeout/collect/check");
        registration.addPathPatterns("/prod-api/api/takeout/collect/list");
        registration.addPathPatterns("/prod-api/api/hospital/patient/list");
        registration.addPathPatterns("/prod-api/api/hospital/patient");
        registration.addPathPatterns("/prod-api/api/hospital/patient");
        registration.addPathPatterns("/prod-api/api/hospital");
        registration.addPathPatterns("/prod-api/api/hospital/reservation");
        registration.addPathPatterns("/prod-api/api/hospital/reservation/list");
        registration.addPathPatterns("/prod-api/api/job/profession/list");
        registration.addPathPatterns("/prod-api/api/job/resume/queryResumeByUserId");
        registration.addPathPatterns("/prod-api/api/job/deliver");
        registration.addPathPatterns("/prod-api/api/job/deliver/list");
        registration.addPathPatterns("/prod-api/api/activity/comment");
        registration.addPathPatterns("/prod-api/api/activity/signup");
        registration.addPathPatterns("/prod-api/api/activity/signup/check");
        registration.addPathPatterns("/prod-api/api/movie/film/like");
        registration.addPathPatterns("/prod-api/api/movie/film/comment");
        registration.addPathPatterns("/prod-api/api/movie/film/comment/like");
        registration.excludePathPatterns("/swagger-ui.html");
    }

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