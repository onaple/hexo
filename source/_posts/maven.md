---
title: maven
comments: true
tags:
  - maven
categories:
  - MAVEN
date: 2017-09-09 10:56:08
update: 2017-09-09 10:56:08

---
# 常用难记命令
1. mvn clean install -D maven.test.skip=true   
2. mvn clean package -U -DfailIfNoTests=false -f pom.xml


1. 创建Maven的普通java项目： 
   mvn archetype:create  -DgroupId=packageName -DartifactId=projectName  
2. 创建Maven的Web项目：   
    mvn archetype:create -DgroupId=packageName    -DartifactId=webappName  -DarchetypeArtifactId=maven-archetype-webapp    

7. 生成eclipse项目：mvn eclipse:eclipse  
8. 生成idea项目：mvn idea:idea 
11. 跳过测试:  mvn install -Dmaven.test.skip=true  
11. 指定端口:  mvn -Dmaven.tomcat.port=9090


# Jar包冲突：
ClassNotFoundException，NoSuchFieldException，NoSuchMethodException

解决jar包冲突

```
  mvn dependency:tree -Dverbose
```

当遇到jar包冲突时，我们首先确定是哪个jar包冲突了，这个很容易，看我们调用的类或方法，是属于哪个Jar包。然后就是要找出冲突了，我这里使用命令

```
mvn dependency:tree -Dverbose -Dincludes=<groupId>:<artifactId>
```

填写上Jar包的groupId和artifactId，可以只有一个，但是中间的冒号不要少，这样就会输出依赖树，而且是仅包含这个Jar包的依赖树，这样那些地方依赖了这个Jar包的那个版本就一目了然了。
例如，我的项目中notify-common包存在冲突，我们使用命令

```
mvn dependency:tree -Dverbose -Dincludes=:notify-common
```
加上Dincludes或者Dexcludes说出你喜欢或讨厌，dependency:tree就会帮你过滤出来： 
过滤串使用groupId:artifactId:version的方式进行过滤，可以不写全啦，如： 

Java代码  
```
mvn dependency:tree -Dverbose -Dincludes=asm:asm  
```

排除不要的jar包。在依赖包中排除相应的包。在POM排除掉依赖，OK了

```
1.     <exclusions>  
2.         <!-- 这个就是我们要加的片断 -->  
3.         <exclusion>  
4.             <artifactId>asm</artifactId>  
5.             <groupId>asm</groupId>  
6.         </exclusion>  
7.     </exclusions>  
```

