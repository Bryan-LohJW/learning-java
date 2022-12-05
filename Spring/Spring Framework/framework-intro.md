# Spring FrameWork

## Java application have different layers

Layers can be DAO (database), Service (business logic), Controllers (mapping), etc

Tight coupling of the different layers within the application can cause dependency issues.

## How spring resolves tight coupling

One key feature of spring is dependency injection, this uses interfaces and implementations of the interface for coupling. 

```java
// tight coupling of component
private ApplicationDao applicationDao = new ApplicationDao();

// loose coupling of component
@Autowired
private ApplicationDao applicationDao;

// tight coupling of fields
private String field = "field value";

// loose coupling of fields
@Value("${properties.prop}")
private String field;
```

## Modules of spring framework

[![Spring Modules](https://static.javatpoint.com/images/sp/spmodules.jpg)](https://https://static.javatpoint.com/images/sp/spmodules.jpg)


## Spring Core

One way perform DI for beans, can use through config.xml

To use the beans, need to use `ApplicationContext` pointing to the configuration file 'context.xml'

From there we can pull the bean out

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext("config.xml");
Employee employee = (Employee) ctx.getBean("emp");
```

This is an example of how to declare beans for dependency injection from the configuration file

There are different ways to inject dependencies

 - Setter (can use the p schema)

 - Constructor (can use the c schema)

```xml
<bean name="city" class="com.bryan.bean.City" address="addr">

    <property name="city">
        <value>Singapore</value>
    </property>

    <property name="state" value="Singapore"/>

</bean>

<!-- Using a schema to help sumplify code -->
<bean name="address" class="com.bryan.bean.Address" p:city="Singapore" p:state="Singapore"/>

<bean name="emp" class="com.bryan.bean.Employee">

    <property name="firstName">
        <value>Bryan</value>
    </property>

    <!-- Injection of bean into another bean -->
    <property name="address">
        <ref bean="addr">
    </property>

    <property name="list">
        <!-- Other than list, can also have map, set, etc -->
        <list>
            <value>First Element</list>
            <value>Second Element</list>
            <value>Third Element</list>
            <value>Fourth Element</list>
            <value>Fifth Element</list>
        </list>
    </property>

</bean>

<bean name="emp" class="com.bryan.bean.Employee">
    <constructor-arg name="firstName" value="Bryan">
</bean>
```

The init and destroy methods can also be defined withing the config file

```xml
<bean name="address" class="com.bryan.bean.Address" p:city="Singapore" p:state="Singapore" init-method="methodName" destroy-method="methodName2"/>
```

The init method is called after the setter methods are called

Can also implement InitializingBean interface to access methods that can be used within the lifecycle

Can also use the bean factory to inject the beans

Another way to inject dependencies is by using `@Autowired` annotation

## Bean scopes

Singleton (default)

Prototype

Request and session scope

## view resolver

## servlet config or controller

## component scanning

## controller
Request mapping
Using model and view to set attribute and everything
Parameters and all
Required, and default value
Using model map to add attributes