---
title: spring
comments: true
tags:
  - spring
categories:
  - SPRING
date: 2017-09-09 17:43:35
update: 2017-09-09 17:43:35
---


# Spring


为什么要使用Spring？
Spring主要两个有功能为我们的业务对象管理提供了非常便捷的方法：

1. DI（Dependency Injection，依赖注入）
2. AOP（Aspect Oriented Programming，面向切面编程）

## Java Bean

1. 必须是个公有(public)类
2. 有无参构造函数
3. 用公共方法暴露内部成员属性(getter,setter)

实现这样规范的类，被称为Java Bean。即是一种可重用的组件。

## 声明Bean

以下是声明Bean的注解：
1. @Component 组件，没有明确的角色
2. @Service 在业务逻辑层使用
3. @Repository 在数据访问层使用
4. @Controller 在展现层使用(MVC -> Spring MVC)使用

>在这里，可以指定bean的id名：Component("yourBeanName").同时，Spring支持将@Named作为@Component注解的替代方案。两者之间有一些细微的差异，但是在大多数场景中，它们是可以互相替换的。

## 依赖注入
注入Bean的注解

@Autowired Spring提供的注解

不仅仅是对象，还有在构造器上，还能用在属性的Setter方法上。

不管是构造器、Setter方法还是其他的方法，Spring都会尝试满足方法参数上所声明的依赖。假如有且只有一个bean匹配依赖需求的话，那么这个bean将会被装配进来。

如果没有匹配的bean，那么在应用上下文创建的时候，Spring会抛出一个异常。为了避免异常的出现，你可以将@Autowired的required属性设置为false。

将required属性设置为false时，Spring会尝试执行自动装配，但是如果没有匹配的bean的话，Spring将会让这个bean处于未装配的状态。但是，把required属性设置为false时，你需要谨慎对待。如果在你的代码中没有进行null检查的话，这个处于未装配状态的属性有可能会出现NullPointerException。

@Inject注解来源于Java依赖注入规范，该规范同时还为我们定义了@Named注解。在自动装配中，Spring同时支持@Inject和@Autowired。尽管@Inject和@Autowired之间有着一些细微的差别，但是在大多数场景下，它们都是可以互相替换的。

@Autowired是最常见的注解之一，但在老项目中，你可能会看到这些注解，它们的作用和@Autowired相近：

@Inject 是JSR-330提供的注解
@Resource 是JSR-250提供的注解


### 限定自动装配的bean
@Qualifier注解是使用限定符的主要方式。它可以与@Autowired和@Inject协同使用，在注入的时候指定想要注入进去的是哪个bean。为@Qualifier注解所设置的参数就是想要注入的bean的ID

```
@Autowired
@Qualifier("iceCream")
public void setDessert(Dessert dessert){
  this.dessert = dessert;
}
```