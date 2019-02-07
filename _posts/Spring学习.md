---
title: Spring学习
date: 2017-01-20 06:20:50
tags:
---
# Spring简介

## Spring的存在是因为它自身有着得天独厚的优势：

- 它定位的领域是许多其他流行的framework没有的

- Spring是全面的和模块化的

- 它的设计是从底部榜之你编写易于测试的代码

- Spring是潜在的一站式解决方案

## Spring天生就存在如下优点：

- 低侵入式设计，代码污染极低

- Write Once, Run Anywhere
- DI有效的降低了耦合度
- AOP提供了通用任务的集中管理

- ORM和DAO简化了对数据库访问

- 高度开放性，并不强制

## Spring的优点给开发带来的好处：

- 可以有效组织中间层对象

- 使用统一的配置我呢见

- 促进良好编程习惯，减少编程代价

- 易于单元测试

- 使用EJB成为一种备选

- 为数据存取提供了一致的框架

## Spring的特点：

- 方便解耦，简化开发

- AOP编程的支持

- 声明式事务的至支持

- 方便程序的测试

- 方便集成各种优秀框架

- 降低JAVAEE API的使用难度

- Spring的源码是经典学习范例

## Spring的核心模块


![](https://i.imgur.com/zCHqMzq.png)

## Spring总结

- spring带来的复杂的J2EE开发的春天
- 他的核心是轻量级的IoC容器，他的目标是为J2EE应用提供了全方位ie的整合框架，在Spring框架下实现多个子框架的组合，这些子框架之间可以彼此独立，也可以使用其他的框架方案加以替代
- Spring系统为企业应用提供一站式的解决方案



# Spring之AOP

## 什么是AOP

面向切面的编程

AOP将应用系统分为两个：**核心业务逻辑** 和 **横向的通用逻辑**

AOP是对OOP的一种完善

## AOP的主要功能：

- 主要用于系统级别的功能
  - 日志记录
  - 性能统计
  - 安全控制
  - 事务处理
  - 异常处理
  - 等等

AOP将常用服务模块化，并且用声明的方式将这些组件使用到其他的业务组建当中去，这样做的结果是每个业务只需要关心自己的业务组件逻辑，而不需要关心常用的服务组件，这样就保证了内聚性

AOP专门用于处理系统中分布于各个模块中的交叉关注点的问题，在JavaEE应用中，常常通过AOP来处理一些具有横切性质的系统服务，如事务管理，安全检查，缓存，对象管理等，AOP已经成为一种非常常用的解决方案：



例如：

![](https://i.imgur.com/vrzW9rJ.png)

- 如果是这个样子，三个模块的相同代码段都是通过复制，粘贴其他的代码，如果有一天，复制的代码需要修改，那么就要修改三个部分



![](https://i.imgur.com/kjBYJFJ.png)

- 如果是这个样子，来调用深色区域的代码块，那么可以完成同时修改，降低后续维护的复杂度，可以解决大部分的场景

- 如果应用需要三个方法彻底与深色方法分离，那么上述两个方法就不合适了
  - 运用AOP
  - AOP专门用于处理系统模块中，分布于各个模块中的交叉关注点问题，通常使用AOP处理系统中具有横切性质的问题

AOP代理其实是AOP框架动态生成的一个对象，该对象可作为目标对象使用

![](https://i.imgur.com/2BY1GMg.png)

## 使用AOP方法中，需要程序员参与的就是：

- 定义不同业务组件
- 定义切入点
- 定义增强处理
  - 在AOP框架为普通组件植入的处理动作

代理对象的方法 = 增强处理+被对代理的方法

## AOP的关键概念的解释：

- 切面 - Aspect
  - 一个关注点的模块化，这个关注点可能会横切多个对象
  - 事务处理是一个J2EE应用中关于横切接入点的很好的例子

- 连接点 - Join Point
  - 程序执行的当中的某个特定的点，例如：某方法调用的时候，处理异常的时候
- 通知 - Advice
  - 切面某个特定的连接点上执行的动作
  - around, before, after 等通知
  - 许多AOP框架中以拦截器为同志模型
- 切入点 - Point Cut
  - 匹配连接点的断言
  - 通知和一个切入点表达式的并联，并在满足这个切入点的连接点上运行
- 引入 - Introduction
  - 用来个一个类型声明额外的方法和属性
- 目标对象 - Target Object
  - 被一个或多个切面所通知的对象，也被称作被通知对象
  - Spring AOP 是通过运行是代理实现的，那么这个对象永远是一个被代理的对象
- AOP代理 - AOP Proxy
  - AOP框架所创建的对象
- 织入 - Weaving
  - 把切面连接到其他的应用程序类型或者对象之上，并创建一个被通知的对象

## AOP通俗的理解

一个组件A，不关心其他常用的服务组件B，但是这个组件A使用组件B的时候，不是组件A自身去调用，而是通过配置的呢个其他方式，不如Spring中可以通过xml配置文件。  

这样就是的A压根就不需要知道组件B是怎样的。A只需要关心自己的业务逻辑，具体A使用B的时候，配置文集去做，与具体的A组件无关



# Spring 之 IOC

## 浅谈IOC

IOC（Inversion of Control，控制反转）是Spring的核心，贯穿始终。

所谓IOC，对于Spring框架来说，就是有Spring来负责控制对象的生命周期和对象间的关系

- 传统开发模式：对象之间互相依赖
  - 在一个对象中使用另一个对象，就必须要自己new一个对象，或者查询一个
  - 使用完之后要将对象销毁
  - 就像自己找女朋友，要自己找到一个女孩子，知道她的qq，mail，等等
- IOC开发模式：IOC容器安排对象之间的依赖
  - 就像去婚介找女朋友，提出要求，婚介会按要求匹配女朋友介绍给你
  - 对象之间的依赖关系由IOC来控制
  - 所有的类都会在Spring容器中登记，告诉它你是个什么东西，你需要什么东西
  - Spring会在系统运行的时候，在适当的时间把你需要的东西传递给你
  - 同时也会把你交给需要你的对象

## IOC理论的背景

### 传统

一个齿轮出现问题，那么整个系统就可能出现问题

![](https://i.imgur.com/WUX5cZj.png)

### IOC

把复杂系统，分解成相互协作的对象，这些对象通过内部实现，对于外部是透明的，从而降低解决问题的复杂度

![](https://i.imgur.com/nU2EtFF.png)

### 终极目标

A，B，C，D四个模块之间并没有关联。这也是Spring的终极目标

![](https://i.imgur.com/B3gzgxd.png)

### 控制反转

- 上面三张图就能很明显的观察到控制反转：
  - 初始的时候，每个对象的控制权都在自己手上，不管是创建对象或者是删除对象
  - 在引入IOC后，每个对象的控制权都在IOC容器中，当A运行的到需要B的时候，IOC容器会主动创建B对象，注入到A中
- 控制权颠倒了过来，这就是控制反转的由来

## 依赖注入（DI）

IOC的另外的名字叫做依赖注入（Dependency Injection），所谓的依赖注入，就是由IOC容器在运行期间，动态地将某种依赖关系注入到对象中。

所以，依赖注入（DI）金额控制反转（IOC）是从不同的角度的描述同一件事情，就是指通过引入IOC容器，利用依赖关系注入的方式，实现对象之间的解耦

## IOC的好处

- IOC在编程过程中不会对业务对象构成很强的侵入性，使用IOC之后，对象具有更好的可实用性，可重用性和可扩展性
  - 降低组件之间的耦合度
  - 提高开发效率和产品质量（只需要要求接口规格，每个人只需要关心自己的工作）
  - 统一的标准，提高模块的复用性
  - 模块具有热插拔特性（IOC生成方式转为外置方式，把对象的生成放在了配置文件里进行定义，这样的实现子类变得更加简单，只需要更改配置文件）



## IOC的通俗的了解

- IOC控制反转
  - 创建对象实例的控制权从代码控制剥离到IOC容器控制，实际就是你在xml文件控制，侧重于原理
- DI依赖注入
  - 创建对象实例的时候，为这个对象注入属性值或其他对象实例，侧重于实现



# Spring的配置文件浅析

## Spring的配置文件概述

Spring的配置文件是用于`指导Spring工厂进行Bean的生产，依赖关系注入及Bean实例`分发的“图纸”，它是一个或多个标准的XML文档，J2EE程序员必须学会灵活应用这份“图纸”，准确地表达自己的“生产意图“

### Spring配置文件示例

- Spring配置文件的结构一般结构如下
  - &lt;beans> 用于表示bean表示的开始或结束
    - &lt;import resource = "resource1.xml" > 用于导入其他配置文件bean的定义，可以放在beans标签下的任何位置
    - &lt;import resource = "resource2.xml"> 
    - &lt;bean id = "bean1" class="***"></bean> 使用id calss 定义了一个bean
    - &lt;bean name="bean2" class="***"></bean> 使用name class定义了一个bean
    - &lt;alias alias="bean3" name="bean2" />  定义别名，这句话的意思是 bean3 和 bean2 是同一个bean
  - &lt;/beans>

### Spring容器高层视图

- Spring容器启动基本条件
  1. Spring框架的类包
  2. Bean的配置信息
  3. Bean的实现类
- Spring启动时读取程序提供的bean的配置信息，并在Spring中生成一份相应的bean的配置注册表，然后根据注册表实例化bean，装配好bean之间的依赖关系，为上层应用提供好准备就绪的应用环境
- Bean的与元数据信息：
  - Bean的实现类
  - Bean的属性信息
  - Bean的依赖关系
  - Bean的行为配置
  - Bean的创建方式

![](https://i.imgur.com/60IVvpH.png)



### 基于XML的配置

Spring的配置文件是居于XML格式的，Spring1.0的配置文件采用DTD格式，Spring2.0以后使用Schema的格式，后者让不同类型的配置拥有了自己的命名空间，使配置文件更具有扩展性  

采用Schema的配置格式，文件头的声明会复杂一些  

例如：  

![](https://i.imgur.com/cqzt345.png)

- xmlns 默认命名空间，用于Spring Bean的定义 
- xmlns:xsi 定义了一个名为xsi的命名空间，为每个文档中命名空间指定相对应的Schema的样式文件，是标准组织定义的标准命名空间
- xmlns:aop 定义了，是Spring 配置aop的命名空间，是用户自定义的命名空间
- 命名空间步骤：
  1.  指定命名空间的名称
  2.  指定Schema文档样式名称的位置

Spring3.0的配置Schema文件分布在各模块类包中，如果模块拥有对应的Schema文件，则可以在模块类包中找到一个config目录，Schema文件就位于该目录中。

![](https://i.imgur.com/fsGKmtm.png)



## Spring Bean的命名

- 每个Bean可以有一个或多个id，我们把第一个id成为”标识符“，其余id叫做”别名“，这些id在IOC容器中必须唯一。

### Bean id 的命名方式和命名约定

- 配置全限定类名，唯一的
  - &lt;bean class="com.ctgu.spring.mode.definition.HelloworldImpl">
    - .getBean(HelloworldImpl.class);
- 指定id，唯一的
  - &lt;bean id = "helloworld" class="com.ctgu.spring.mode.definition.HelloworldImpl">
    - .getBean("helloworld", HelloworldImpl.class);
- 指定name，唯一的
  - &lt;bean name="helloworldName" class="com.ctgu.spring.mode.definition.HelloworldImpl">
    - .getBean("helloworldName", HelloworldImpl.class);
- 同时指定name和id，唯一的
  - &lt;bean id="helloworldid" name="helloworldname" class="com.ctgu.spring.mode.definition.HelloworldImpl" >
    - 同上，二选其一
- 多个name，唯一的

## Spring Bean的实例化

### Spring IOC容器如何实例化Bean呢？

传统应用程序可以通过new和反射方式进行实例化Bean。而Spring IOC 容器则需要根据Bean定义里的配置元数据使用反射机制来创建Bean。

`在Spring IOC容器中主要有以下几种创建Bean实例的方式：`

- 使用构造器实例化Bean
  - 无参构造器
  - 有参构造器
- 使用静态工厂方式实例化Bean
  - 除了指定必须的class属性，还要指定factory-method的属性
  - 允许指定方法参数
- 使用实例工厂方法实例化Bean
  - 不能指定方法参数


> HelloWorldImpl类
```java
package com.ctgu.***.HelloWorldImpl

public class HelloWorldImpl{
  private int id;
  private String name;
  private Set<String> sets;
  private List<String> list;
  private String[] strings;
  private Map<String, String> map;
  public void setId(int id){
    this.id = id;
  }
  public void setName(String name){
    this.name = name;
  }
  public int getId(){
    return this.id;
  }
  public String getName(){
    return this.name;
  }
  public HelloWorldImpl(){
    System.out.println("无参构造函数");
  }
  public HelloWorldImpl(int id, String name){
    System.out.println("有参构造函数");
  }
  public void setSets(Set<String> sets){

  }
  public Set<String> getSets(){
    return this.sets;
  }
  public void setList(List<String> list){
    this.list = list;
  }
  public List<String> getList(){
    return this.list;
  }
  public String[] getStrings(){
    return this.strings;
  }
  public void setStrings(String[] strings){
    this.strings = strings;
  }
  public void setMap(Map<String, String> map){
    this.map = map;
  }
  public Map<String, String> getMap(){
    return this.map;
  }

}

```

### 构造器实例化

构造器实例化Bean是最简单的方式，Spring IoC容器既能使用默认空间构造器，也能使用有参数构造器两种方式创建Bean。

1. 空构造器实例化

```xml
   <bean id="helloServerNoWithArgs" class="com.ctgu.***.HelloWorldImpl" />
```

2. 有参数构造器实例化
 
```xml
   <bean id="helloServerNoWithArgs" class="com.ctgu.***.HelloWorldImpl" />
     <!-- 是定构造器参数 index表示位置 value 表示值 -->
     <constructor-arg index="0" value="10" />
     <constructor-arg index="1" value="Hello Spring" />
   </bean>
```

3. 在main 函数中

```java
public static void main(String[] args){
  ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
  HelloWorldImpl hello = ac.getBean("helloServerNoWithArgs", HelloWorldImpl.class);
}
```

### 静态工厂实例化

使用静态工厂的方式除了指定必须的class属性，还要指定factory-method属性来指定实例化Bean的方法，而且使用静态工厂方法也允许指定方法参数，Spring IoC容器将调用此属性指定的方法来获取Bean

```java
// helloWorldStaticFacorty静态工厂类
// 有一个函数名叫 newInstance

static HelloWorldImpl newInstance(int id, String name){
  return new HelloWorldImpl(id, name);
}

```

```xml
<!-- 使用有参数构造参数-->
<bean id="helloServiceStaticFacory" class="com.ctgu.***.helloWorldStaticFacorty" factory-method="newInstance">
  <!-- 上述的 newInstance 就是静态工厂类的函数名 -->
  <!-- 指定构造器参数 -->
  <constructor-arg index="0" value="10"/>
  <constructor-arg index="1" value="hell static factory"/>
</bean>
```

### 实例工厂实例化

使用实例工厂的方式不能指定class属性，此时必须facroty-bean属性来指定工厂Bean，factory-method属性指定实例化Bean的方法，而且使用实例化工厂方法允许指定方法参数，方法和使用构造器一样

```xml
<bean id="beanInstanceFacory" class="com.ctgu.***.HelloWorldInstanceFactory" />
<!-- 使用实例工厂Bean创建Bean -->
<bean id="helloworldinstance" factory-bean="beanInstanceFacory" factory-mathod="newInstance">
  <constructor-arg index="0" value="10"></constructor-arg>
  <constructor-arg index="1" value="hello instnace facory!"></constructor-arg>
</bean>
```

### 设置实例化对象的参数

1. 通过构造方法来设置值

```xml
<bean id="helloServerNoWithArgs" class="com.ctgu.***.HelloWorldImpl" />
  <!-- 是定构造器参数 index表示位置 value 表示值 -->
  <constructor-arg index="0" value="10" />
  <constructor-arg index="1" value="Hello Spring" />
</bean>
```

2. 设置注入（通过set方法）

```xml
<bean id="helloServerNoWithArgs" class="com.ctgu.***.HelloWorldImpl" />
  <property name="id" value="10"></property>
  <property name="name">
    <value>test</value>
  </property>
</bean>
<!-- 上述两种赋值方法等效 -->
<!-- 通过对象的set方法设置值，name为参数名，value为设置的值 -->
  <property name = "sets">
    <set>
      <value>1</value>
      <value>2</value>
      <value>3</value>
      <value>4</value>
    </set>
  </property>
<!-- 通过上述方法对Set对象赋值 -->

  <property name="list">
    <list>
      <value>1</value>
      <value>2</value>
      <value>3</value>
      <value>4</value>
    </list>
  </property>
<!-- 通过上述方法对List对象赋值 -->

  <property name="strings">
    <array>
      <value>1</value>
      <value>2</value>
      <value>3</value>
      <value>4</value>
    </array>
  </property>
<!-- 通过上述方法对数组赋值 -->

  <property name="map">
    <map>
      <entry key="a" value="b">   </entry>
      <entry key="b" value="b">   </entry>
      <entry key="c" value="b">   </entry>
      <entry key="d" value="b">   </entry>
    </map>
  </property>
<!-- 通过上述方法对Map对象赋值 -->
```


## Spring Bean的作用域

Spring Bean中所说的作用域，在配置文件中即是“scope”这个属性。

在面向对象程序设计中一般指对象或变量之间的可见范围。而在spring容器中是指其创建的Bean对象相对于其他Bean对象的请求可见范围

1. singleton： `<bean id="userInfo" class="com.ctgu.userinfo" scope="sigleton"></bean>`
   - Spring IoC 只会创建该bean创建的唯一的实例，即Instance，单例Bean
2. prototype: `<bean id="userInfo" class="com.ctgu.userinfo" scope="prototye"><bean>`
   - 每次请求的时候，Spring IOC容器都会创建一个实例 对于
   - 对于有状态的Bean应该使用prototye，对于无状态的Bean应该使用singleton
3. request： `<bean id="userinfo" class="com.ctgu.userInfo" scope="request"></bean>`
   - 针对每次http请求，Spring容器会根据相关的Bean的定义来创建一个全新的Bean实例
   - 创建的Bean实例仅在当前的HttpRequest中有效
4. session：`<bean id="userinfo" class="com.ctgu.userInfo" scppe="session"></bean>`
   - session针对某个HttpSession来起作用的
   - Spring容器会根据该Bean的定义创建一个全新的Bean的实例
5. global-session：`<bean id="userinfo" class="com.ctgu.userInfo" scppe="globalSession"></bean>`

`singleton`作用域是指在Spring IOC容器中仅存在一个Bean的实例，Bean以单例的方式存在，单实例模式是重要的设计模式之一，在Spring中对此实现了超越，可以对那些非线程安全的对象采用单实例模式

`prototype`作用域是指每次从容器中调用Bean时，都返回一个新的实例，即每次调用getBean()时，相当于执行new Bean()的操作。在默认情况下，Spring容器在启东市实例化prototype的Bean

`当用户使用Spring的WebbApplicationContext时，还可以使用另外3中Bean的作用域，即request，session和globalSession。`在使用Web应用环境想关的Bean作用域时，必须在Web容器中进行一些额外配置

- 低版本Web容器配置 运用过滤器filter来进行相关配置

```xml
  <filter>  
    <filter-name>requestContextFilter</filter-name>  
    <filter-class>org.springframework.web.filter.RequestContextFilter</filter-class>  
  </filter>  
  <filter-mapping>  
    <filter-name>requestContextFilter</filter-name>  
    <servlet-name>/*&lt;/srevlet-name>  
  </filter-mapping>  
```

- 高版本Web容器配置 运用Http 请求监听器进行相关配置

```xml
  <listener><listener-class>
  org.springframework.web.context.request.RequestContext.listener
  </listener-class></listener>
```

- Web应用环境的作用域
  - request作用域
    - 一个http请求和生命周期
    - 请求处理完毕后消除生成的Bean
  - session作用域
    - 横跨整个httpsession
    - session结束后清除所有实例化的Bean
  - globalSession作用域
`自定义作用域`

在Spring2.0中，Spring的Bean作用域机制是可以扩展的，这意味着你不仅可以使用Spring提供的预定义Bean作用域，还可以自定义作用域，甚至重定义现有的作用域（不提倡这么做，而且不能覆盖内置的singleton和prototype）

- 实现自定义Scope类
  - org.speingframework.beans.factory.config.Scope
- 注册自定义的Scope类
  - ConfigurableBenFactory.registerScope(String scopeName, Scope scope)

##  配置文件的整合

这里有多个配置文件：

1. Spring-Common.xml 位于 common文件夹下
2. Spring-Connection.xml 位于 connection 文件夹下
3. Spring-Module.xml 位于 module 文件夹下



### 传统加载方式



ApplicationContext context = new ClassPathXmlApplicationContext(new String[]{"Spring.-Common.xml","Spring-Connection.xml","Spring-ModuleA.xml"});



### 整合配置文件:Spring-All_Module.xml

- &lt;beans ... ...>
  - &lt;import resource="connection/Spring-Connection.xml" />
  - &lt;import resource="common/Spring-Common.xml" />
  - &lt;import resource="module/Spring-Resouce.xml" />
- &lt;/beans>

### 整合后的加载方式

	- ApplicationContext context = new ClassPathXmlApplicationContext("Spring-All-Module.xml");


# Java注解技术
- `注解`
	- 顾名思义就是对某个事物添加 注释 说明
	- 存放一些信息，对未来某个时刻可能有用
	- Java注解又叫做Java标注
 `Java提供了一套机制，使得我们可以对类，包，方法，参数，域以及变量等添加标注，添加某些信息并且在以后的某个时段通过反射将标注的信息提取出来，以供使用`
 
## Java注解技术基本概念

## 概念
 `Annotation`是Java5开始引入的新特征
 中文名称一般叫注解
 它提供了一种安全的类似注释的机制，用来将任何的信息或元数据（metadata）与程序元素（类，方法，成员变量等）进行关联
 
- 注解
	- 对某一事物添加注释说明，存放以后可能会用到的信息
	- 对类，包，方法，参数，域以及变量等添加标注，即附加上某些信息
	- Annotation就是Java提供一种源程序中，元素关联关联任何信息和任何元数据的途径和方法
- 可以用于创建文档，跟踪代码中的依赖性，执行基本编译检查
### 原理
注解是`一种接口`，通过Java 反射机制相关的API来访问注解信息
相关类，即：
1. 框架
2. 工具当中的类
Java语言解释器在工作的时候会忽略这些注解，因此在Java虚拟机当中这些注解是不起作用的

#### 注解不同于接口
1. 注解是使用关键字， @interface，而不是interface
2. 注解类型方法定义是独特的，受限制的。注解类型的方法必须声明为无参数，无异常抛出的，这些方法定义了注解的成员，方法名成为了成员名，而方法返回值成为了成员你的类型
3. 注解类型又与接口又相似之处，可以定义常亮，静态成员类型
### 应用场合
注解一般被作为一种辅助途径，应用在软件框架或者工具当中
在这些工具类中，根据不同的注解信息采取不同的处理过程，或者改变相应的程序元素
## Java标准注解
`Java内置了三种标准注解`
### Override注解
用作标注方法，说明了被标注的方法，重载的父类的方法，起到了断言的作用
如果我们使用这种注解，在一个没有覆盖父类方法的方法时，Java编译器讲以一个编译错误来进行解释
这个注解常用在我们试图覆盖父类方法，而又`写错了方法名称` 时，加上一个Override这样一个保证性校验过程

### Deprecated
当一个类型或者类型成员使用@Deprecated修饰的时候，编译器将不鼓励使用这种被标注的程序元素。
所以使用这种注解修饰具有一定的延续性，即如果我们在代码中通过继承或者覆盖的方法使用了这个`过时的类型或者成员`，虽然继承或者覆盖后的类型成员并不是被声明为@Deprecated，但编译器仍然要报警
### SuppressWarinings
这个注解能够告诉Java编译器`关闭对类，方法以及成员变量的警告`
有时候编译会出现一些警告，对于这些警告有的隐藏着bug，有的则是无法避免的。
对于某些不想看到的警告信息，可以通过@SuppressWarinings来屏蔽那些警告信息
## Java元注解
元注解就是注解其他注解的注解
Java5.0定义了4个标准的metea-annotaion类型，他们被涌来提供对其他annotaion类型做说明，Java5.0定义的元注解有四种
1. @Target
2. @Retention
3. @Documented
4. @Inherited

### @Target元注解
@Target 主要作用是用于描述注解的使用范围，即被描述的注解可以用在什么地方
1. CONSTRUCTOR		主要用于描述构造器
2. FIELD				用来描述域
3. LOCAL_VARIABLE	用来描述局部变量
4. METHOD			用来描述方法
5. PACKAGE			用来描述包
6. PARAMETER			用来描述参数
7. TYPE				用于描述类，接口，枚举，声明等

### @Retention元注解
@REtention主要表示需要在什么级别保存该注释信息，用于描述注解的生命周期
`注解的生命周期由Retention的取值决定的`
@Retention取值：
1. SOURCE		在源文件有效
2. CLASS		在CLASS中有效
3. RUNTIME	在运行时有效

### @Documented元注解
@Documented用于描述其他类型的 注解 应该被作为被标注的程序成员的公共API，因此可以被例如Javadoc此类工具文档化
这是个标记注解，没有任何成员

### @Inherited元注解
@Inherited 元注解是一个标记注解，@Inherited阐述了某个被标注的类型是被继承的。
如果使用了@Inherited修饰的 注解 类型被用于一个class，则这个 注解 将被用于这个 class 的子类
## Java自定义注解
 我们可以使用@Interface来定义自定义注解
 在使用@Interface来定义自定义注解的时候，自动继承了Java.lang.annotation.****（我不知道是哪个），由编译程序自动完成其他的细节
 那么，在`定义注解的时候，不能继承其他的注解或者接口`
 @interface来声明一个注解，其中每个方法实际上是声明了一个配置参数，方法的名称就是参数的名称，返回值类型就是参数的类型，即返回值类型只能是基本类型

自定义注解主要一下两步：

- 通过 @interface关键字声明注解名称，注解成员属性等
- 使用Java内置的四个元注解对自定义标注的功能和范围进行约束

`自定义注解的格式`
```
	public @interface 注解名 {
		定义体
	}
```

### 注解参数支持的数据类型

- 所有的基本数据类型
- String类型
- Class类型
- enum类型
- Annotation类型
	- 只能用public，default这两个访问权来进行修饰
- 以上所有类型的数组

### 自定义注解及使用

```
	定义：
	@Target(ElementType.FIELD)
	@Retention(RetentionPolicy.RUNTIME)
	@Documented
	public @interface FruitName{
		String value() default "";
	}
	
	使用
	public class Apple{
		@FruitName("Apple")
		private String appleName;
	}
	
```

## Java注解元素默认值
注解元素的默认值：注解元素必须有确定的值，要么在定义注解的默认值中指定，要么在使用注解时指定，非基本类型的注解元素的值不可以为null，因此使用空字符串或0是一种比较常用的做法

###　例子

```
	@Target(ElementType.FIELD)
	@Retention(RetentionPolicy.RUNTIME)
	@Documented
	public @interface FruitProvider{
		//供应商编号
		public int id() default -1;
		//供应商名称
		public String name() default "";
		//供应商地址
		public String address() default "";
	}
```

