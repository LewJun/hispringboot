# 01-helloworld

[TOC]

## 对项目进行打包使用

首先**必须**加入依赖`spring-boot-maven-plugin`

* mvn clean package -Dmaven.test.skip=true
* 或者 mvn clean package -Dmaven.test.skip=true spring-boot:repackage
* java -jar target/01-*.jar

