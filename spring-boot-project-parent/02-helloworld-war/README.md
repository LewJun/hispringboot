# 02-helloworld-war

[TOC]

## 对项目进行打包部署到独立的tomcat 容器

首先**必须**加入依赖`spring-boot-maven-plugin`
* 将packing由jar改为war
* 修改spring-boot-starter-tomcat scope为provided，以避免和独立 tomcat 容器的冲突.
* 修改App，继承自SpringBootServletInitializer，重写configure，添加注解@ServletComponentScan
```java
@SpringBootApplication
@ServletComponentScan
@RestController
public class App extends SpringBootServletInitializer {

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
        return builder.sources(App.class);
    }

    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }

    @GetMapping("/hello")
    public String hello() {
        return "hello world!";
    }
}
```

* mvn clean package -Dmaven.test.skip=true
* 或者 mvn clean package -Dmaven.test.skip=true spring-boot:repackage
* 准备tomcat
    - 注意版本要对应 可以在pom.xml中展开依赖tomcat来查看使用的版本
* mv 02-helloworld-war-0.0.1-SNAPSHOT.war /Softs/tomcat位置/webapps/ROOT.war

如上步骤怪麻烦的。