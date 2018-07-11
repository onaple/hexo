---
title: Spring IOC
comments: true
tags:
  - Spring
  - IOC
categories:
  - SPRING
date: 2017-09-11 08:39:59
update: 2017-09-11 08:39:59

---

## Spring是什么

* Spring是一个容器，负责对象的创建。
* Spring的核心是控制反转(IoC)和面向切面(AOP)。
* 简单来说，Spring 是一个分层的 JavaSE/EEfull-stack(一站式) 轻量级 开源框架。

## Spring的优势
1. 方便解耦，简化开发：
Spring就是一个大工厂，可以将所有对象创建和依赖关系维护，交给 Spring 管理。
2. AOP编程的支持：Spring提供面向切面编程，可以方便的实现对程序进行权限拦截、运行监控等功能。
3. 声明式事务的支持：只需要通过配置就可以完成对事务的管理，而无需手动编程。
4. 方便程序的测试：Spring对Junit4支持，可以通过注解方便的测试Spring程序。
5. 方便集成各种优秀框架：Spring不排斥各种优秀的开源框架，其内部提供了对各种优秀框架(如:Struts、Hibernate、MyBatis、Quartz 等)的直接支持 降低 JavaEE API 的使用难度。          
Spring对JavaEE开发中非常难用的一些API(JDBC、JavaMail、远程调用等)，都提供了封装，使这些 API 应用难度大大降低。

## IOC 
1. IOC控制反转,将对象的创建权交给了Spring。
2. DI Dependency Injection 依赖注入，需要有 IOC 的环境，Spring创建这个类的过程中,Spring将类的依赖的属性设置进去.

## BeanFactory 和 ApplicationContext 的区别
1. BeanFactory（已过时）:Spring原始接口。针对原始接口的实现类功能较为单一；BeanFactory接口实现类的容器。特点是每次在获得对象时才会创建对象，适应与手机端这种内存小的环境。
2. ApplicationContext（继承与BeanFactory）: 在加载applicationContext.xml(容器启动)时候就会创建。适用于web项目。
3. ApplicatioContext 接口有两个实现类:每次容器启动时就会创建容器中配置的所有对象.并提供更多功能。
 * ClassPathXmlApplicationContext :加载类路径下Spring的配置文件。
 * FileSystemXmlApplicationContext :加载本地磁盘下Spring的配置文件。

 
## bean的配置
1. id :Bean起个名字；在约束中采用ID的唯一约束。必须以字母开始，可以使用字母、数字、连字符、下划线、句号、冒号。 **id:不能出现特殊字符**。
2. name:Bean起个名字；没有采用ID的约束。name:出现特殊字符.如果<bean>没有id的话 , name可以当做id使用。推荐使用name。

## scope 属性:Bean 的作用范围
* singleton:默认值，单例的。
* prototype:多例的。
* request:WEB项目中，Spring创建一个Bean的对象,将对象存入到request域中。
* session :WEB项目中，Spring创建一个Bean的对象，将对象存入到session域中。
* globalSession :WEB项目中,应用在Porlet环境.如果没有Porlet环境globalSession相当于session.

## Bean 的生命周期的配置
通过配置<bean>标签上的 init-method 作为 Bean的初始化的时候执行的方法，配置destroy-method作为Bean的销毁的时候执行的方法。销毁方法想要执行，需要是单例创建的 Bean 而且在工厂关闭的时候，Bean 才会被销毁。

##  Spring 生成 Bean 的时候三种方式
```
 <!-- 方式一:无参数的构造方法的实例化 -->
 <bean id="bean1" class="spring.demo3.Bean1"></bean>

 <!-- 方式二:静态工厂实例化 Bean -->
 <bean id="bean2" class="spring.demo3.Bean2Factory" factory-method="getBean2"/>

 <!-- 方式三:实例工厂实例化 Bean -->
 <bean id="bean3Factory" class="spring.demo3.Bean3Factory"></bean> 
 <bean id="bean3" factory-bean="bean3Factory" factory-method="getBean3"></bean>

```

## Spring 的 Bean 的属性注入:

```
<!-- 第一种:构造方法的方式 -->
<bean id="car" class="spring.demo4.Car">
<constructor-arg name="name" value="保时捷"/>
<constructor-arg name="price" value="1000000"/> </bean>

<!-- 第二种:set 方法的方式 -->
<bean id="car2" class="spring.demo4.Car2">
<property name="name" value="奇瑞 QQ"/>
<property name="price" value="40000"/> </bean>

<!-- p名称空间的属性注入的方式 -->
<bean id="car2" class="spring.demo4.Car2" p:name="宝马7" p:price="1200000"/>
<bean id="person" class="spring.demo4.Person" p:name="张三" p:car2-ref="car2"/>


SpEL:Spring Expression Language. 语法:#{ SpEL }
<!-- SpEL 的注入的方式 -->
<bean id="car2" class="spring.demo4.Car2">
<property name="name" value="#{'奔驰'}"/>
<property name="price" value="#{800000}"/> </bean>
<bean id="person" class="spring.demo4.Person"> 
<property name="name" value="#{'冠希'}"/>
<property name="car2" value="#{car2}"/>
</bean>

<bean id="carInfo" class="spring.demo4.CarInfo"></bean>
引用了另一个类的属性
<bean id="car2" class=" 
spring.demo4.Car2"> <!-- <property name="name" value="#{'奔驰'}"/> -->
        <property name="name" value="#{carInfo.carName}"/>
        <property name="price" value="#{carInfo.calculatePrice()}"/>
</bean>


<!-- Spring 的复杂类型的注入===================== -->
<bean id="collectionBean" class="spring.demo5.CollectionBean">
<!-- 数组类型的属性 --> 
<property name="arrs">
<list>
 <value>会希</value>
 <value>冠希</value>
 <value>天一</value>
</list>
</property>
<!-- 注入 List 集合的数据 --> <property name="list">
<list>
 <value>芙蓉</value> <value>如花</value> <value>凤姐</value>
</list>
</property>
<!-- 注入 Map 集合 --> <property name="map">
<map>
<entry key="aaa" value="111"/> <entry key="bbb" value="222"/> <entry key="ccc" value="333"/>
</map>
</property>

<!-- Properties 的注入 --> <property name="properties">
<props>
<prop key="username">root</prop>
 <prop key="password">123</prop>
</props>
</property>
</bean>



<!-- 注入对象类型的属性 -->
<bean id="person" class="spring.demo4.Person">
<property name="name" value="会希"/>
<!-- ref 属性:引用另一个 bean 的 id 或 name --> <property name="car2" ref="car2"/>
</bean>
```


## Spring 的分配置文件的开发
一种:创建工厂的时候加载多个配置文件:

```
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml","applicationContext2.xml");
```
二种:在一个配置文件中包含另一个配置文件:

```
<import resource="applicationContext2.xml"></import>
```


### Spring要导入的基础包
1. beans
2. context
3. core
4. expression
5. commons-logging
6. log4j



## 注解
1. @Component:组件.(作用在类上)Spring 中提供@Component 的三个衍生注解:(功能目前来讲是一致的)
 * @Controller * @Service * @Repository这三个注解是为了让标注类本身的用途清晰，Spring在后续版本会对其增强

2. 属性注入的注解:(使用注解注入的方式,可以不用提供 set 方法.) * @Value :用于注入普通类型. * @Autowired :自动装配: 默认按类型进行装配. 
 * 按名称注入:@Qualifier:强制使用名称注入. 
 * @Resource 相当于: @Autowired 和@Qualifier 一起使用.