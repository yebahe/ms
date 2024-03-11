  spring面试

# 1、*Spring是什么?（谈一下对spring的理解

我们通常所说的Spring就是指**Spring框架**，**Spring框架**是很多模块的集合，使用这些模块可以很方便地进行开发。例如 ：

- 整个Spring框架构建在Core核心模块之上，它是整个框架的基础。在该模块中，Spring为我们提供了一个IoC容器（IoC Container）实现，**用于帮助我们以依赖注入的方式管理对象之间的依赖关系**。
- AOP模块。该模块提供了一个轻便但功能强大的AOP框架，让我们可以以AOP的形式增强各POJO的能力。
- Spring框架在Core核心模块和AOP模块的基础上，为我们提供了完备的数据访问和事务管理功能。可以很方便地对数据库进行访问和进行事务管理。
- spring是一个java企业级开发的开源框架，能够整合众多的第三方框架和类库，使得开发者可以在一个统一的环境中使用它们，而不需要手动集成多个不同的库和工具。因此简化了Java应用程序的开发过程，并且现在的SpringBoot 和SpringCloud框架都是以Spring为基石的。
- **Spring框架的核心特性包括IOC 和AOP**

Spring是一个管理Bean的容器



# 2、*IOC和AOP的理解

- **Spring框架的核心特性包括IOC 和AOP**

## 2.1 对IOC的理解

IOC：控制反转 ,即由用户管理Bean转变为IOC容器帮助用户管理Bean，意思就是将对象的控制权交给IOC容器，由Ioc容器来管理Bean的创建，并由 IoC 容器完成对象的注入。降低了对象之间的耦合度或者说依赖程度。

比如说 现有类 A 依赖于类 B，

- **在传统的开发模式中**，往往是在类 A 中手动通过 new 关键字来 new 一个 B 的对象出来，是程序主动去创建依赖对象b。

- **使用 IoC 思想的开发方式** ：不通过 new 关键字来创建对象，IoC是有专门一个容器来创建这些对象，即由Ioc容器来控制对象的创建，程序需要使用哪个对象就直接从 IoC 容器里面过去即可。所以，当对象A运行到需要对象B的时候，IOC容器会主动创建一个对象B注入到对象A需要的地方。

**===>IOC 是一种设计思想，给出的实现IOC的方法：DI_依赖注入。**

- **所谓依赖注入**，就是由IOC容器在运行期间，动态地将某种依赖关系注入到对象之中。

> **●IoC 容器控制了对象**，**因为由容器帮我们查找及注入依赖对象，对象只是被动的接受依赖对象，所以是反转；哪些方面反转了？依赖对象的获取被反转了。**
>
> ●**谁依赖于谁：**当然是**应用程序依赖于IoC容器**；
>
> ●**为什么需要依赖：****应用程序需要IoC容器来提供对象需要的外部资源**；
>
> ●**谁注入谁：**很明显是**IoC容器注入应用程序某个对象，应用程序依赖的对象**；
>
> **●注入了什么：**就是**注入某个对象所需要的外部资源（包括对象、资源、常量数据）**。





- 传统应用程序都是由我们在类内部主动创建依赖对象，从而导致类与类之间高耦合，难于测试；有了IoC容器后，**把创建和查找依赖对象的控制权交给了容器，由容器进行注入组合对象，所以对象与对象之间是 松散耦合，这样也方便测试，利于功能复用，更重要的是使得程序的整个体系结构变得非常灵活**。

  ------

### 2.2.1 [Ioc 配置的三种方式](https://pdai.tech/md/spring/spring-x-framework-ioc.html#ioc-配置的三种方式)

- #### xml文件配置

  将bean的信息配置.xml文件里，通过Spring加载文件为我们创建bean。

- #### java配置

  1. 创建一个配置类， 添加@Configuration注解声明为配置类
  2. 创建方法，方法上加上@bean，该方法用于创建实例并返回，该实例创建后会交给spring管理，方法名建议与实例名相同（首字母小写）

- #### 注解配置

  通过在类上加注解的方式，来声明一个类交给Spring管理，Spring会自动扫描带有@Component，@Controller，@Service，@Repository这四个注解的类，然后帮我们创建并管理，**前提是需要先配置Spring的注解扫描器。**

  对类添加@Component相关的注解，比如@Controller，@Service，@Repository

  设置ComponentScan的basePackage, 比如``, 或者`@ComponentScan("tech.pdai.springframework")`注解，或者 `new AnnotationConfigApplicationContext("tech.pdai.springframework")`指定扫描的basePackage.

#### @Component 和 @Bean 的区别是什么？

- `@Component` 注解作用于类，而`@Bean`注解作用于方法。
- `@Component`通常是通过类路径扫描来自动侦测以及自动装配到 Spring 容器中（我们可以使用 `@ComponentScan` 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。`@Bean` 注解通常是我们在标有该注解的方法中定义产生这个 bean,`@Bean`告诉了 Spring 这是某个类的实例，当我需要用它的时候还给我。
- `@Bean` 注解比 `@Component` 注解的自定义性更强，而且很多地方我们只能通过 `@Bean` 注解来注册 bean。比如当我们引用第三方库中的类需要装配到 `Spring`容器时，则只能通过 `@Bean`来实现。



### 2.2.2 [依赖注入的三种方式](https://pdai.tech/md/spring/spring-x-framework-ioc.html#依赖注入的三种方式)

- #### setter方式

  - **在XML配置方式中**，**property**都是setter方式注入【**<u>类中必须存在set()方法</u>**】，比如下面的xml:

    ```xml
    // 配置
    <bean id="userService" class="tech.pdai.springframework.service.UserServiceImpl">
            <property name="userDao" ref="userDao"/>
            <!-- additional collaborators and configuration for this bean go here -->
        </bean>
    ------------------------------------------------------------------------------
    ```
    
1. 第一步，需要new UserServiceImpl()创建对象, 所以需要默认构造函数【**默认的构造器函数一定要存在】**
2. 第二步，调用setUserDao()函数注入userDao的值, 所以需要setUserDao()函数
```java
    // 使用 
ApplicationContext context = new       ClassPathXmlApplicationContext("applicationContext.xml");
    
   // 从容器中获取bean
 UserService userService = (userService) context.getBean("userService");
```

- #### 构造方法注入

  - **在XML配置方式中**，`constructor-arg`是通过**构造函数参数注入**

    本质上是new UserServiceImpl(userDao)创建对象 【所以对应的构造器方法都必须存在】

    ```xml
     <bean id="userService" class="tech.pdai.springframework.service.UserServiceImpl">
            <constructor-arg name="userDao" ref="userDao"/>
            <!-- additional collaborators and configuration for this bean go here -->
        </bean>
    ------
    著作权归@pdai所有
    原文链接：https://pdai.tech/md/spring/spring-x-framework-ioc.html
    ```

- ### 注解注入


#### `autowire`如何使用

当使用基于 XML 的配置元数据时，可以使用 元素的 `autowire` 属性为 bean 定义指定自动装配模式。共4种模式可以指定。

| 模式        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| no          | （默认）不自动装配。 Bean 引用必须由 ref 元素定义。          |
| byName      | 按属性名称自动装配。 Spring 寻找与需要自动装配的属性同名的 bean。 |
| byType      | 根据类型自动装配。如果容器中恰好存在一个属性类型的 bean，则让属性自动装配；如果存在多个，则会抛出一个致命异常，表明不能为该 bean 使用 byType 自动装配；没有匹配的 bean，什么也没有发生（属性未设置） |
| constructor | 类似于 byType 但适用于构造函数参数。如果容器中没有一个构造函数参数类型的 bean，则会引发致命错误。 |

#### `@Autowired`和`@Resource`的区别

`@Autowired`和`@Resource`是用于依赖注入的注解，用于将依赖对象自动注入到目标类中。它们的区别如下：

1. 来源：`@Autowired`是Spring框架提供的注解，而`@Resource`是Java EE标准提供的注解。
2. 依赖查找方式：`@Autowired`通过类型（byType）进行依赖查找和自动装配，它会根据类型在Spring容器中查找匹配的bean并进行注入。`@Resource`通过名称（byName）进行依赖查找和自动装配，它会根据指定的名称在Spring容器中查找匹配的bean并进行注入。
3. 优先级：当存在多个匹配的bean时，`@Autowired`默认按照类型进行匹配，如果存在多个相同类型的bean，会抛出异常。可以通过`@Qualifier`注解来指定具体要注入的bean。而`@Resource`默认按照名称进行匹配，可以通过`name`属性指定具体要注入的bean名称。
4. 应用范围：`@Autowired`注解在Spring框架中更常用，适用于Spring的依赖注入。`@Resource`注解是Java EE标准的一部分，适用于各种Java EE容器，也可以在Spring中使用。

## 2.2 Aop

-  AOP : 面向切面编程，**AOP 是一种编程思想**，面向切面编程是将程序抽象成各个切面，即解剖对象的内部，**将那些影响了多个类的公共行为（例如事务处理、日志管理 交叉业务）但是和核心业务没有关系的代码 抽取到一个可重用模块里**，**形成一个横向的切面**，将这个切面通过特定的方式切入到核心业务中。【这个过程称为AOP】
-  **它是面向对象编程的一种补充和完善，可以通过预编译方法和运行期动态代理方法实现，在不修改代码的情况下给程序动态添加额外功能，使用AOP还可以减少系统的重复代码，降低模块间的耦合度**。
-  **Spring AOP **
   - 底层的实现是动态代理，有两种方式 ： jdk动态代理和cglib动态代理
     - Spring AOP 就是基于动态代理的，**Spring AOP 属于运行时增强技术，**如果要代理的对象，实现了某个接口，那么 Spring AOP 会使用 **JDK Proxy**，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候 Spring AOP 会使用 **Cglib** 生成一个被代理对象的子类来作为代理。
-  Spring框架中对AOP的使用场景有 ：
   - Spring Bean
   - spring 事务

 

# 3、Spring 的启动过程

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**0、创建容器**

启动Spring容器，首先需要创建一个ApplicationContext对象。这个对象是Spring框架的核心，**负责管理所有的Bean对象，以及解决它们之间的依赖关系**。ApplicationContext对象可以通过多种方式来创建。

如果是以XML方式配置Bean，那么就使用ClassPathXmlApplicationContext类的构造方法创建一个ApplicationContext对象，这个过程有一个叫做 refresh() 方法，**它会触发Spring容器开始加载启动和初始化所有的非懒加载的单例Bean对象**。

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**1、加载并且解析配置文件，得到bean定义信息**

```java
this.obtainFreshBeanFactory(); //【创建beanFactory的实例，得到一个 ConfigurableListableBeanFactory对象】
```

加载并且解析配置文件：【这一步发生在在获取BeanFactory对象的过程中 ，根据在开始的构造参数中传入的文件的路径，将配置文件转为一个document对象，然后遍历每一个元素进行解析操作（可以理解为一个标签就是一个元素，对这些标签进行解析操作）】解析标签之后生成BeanDefinition存放到BeanDefinitionMap当中。

- > BeanFactory是一个Bean工厂，**是Spring框架中提供的一种对象创建和管理机制**。BeanFactory会[读取配置文件](https://so.csdn.net/so/search?q=读取配置文件&spm=1001.2101.3001.7020)，通过反射机制实例化对应的Bean，然后将Bean注册到容器中。

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**2、启动各种后置处理器，这个过程主要做的是对beanDifinition的修改以及补充**

会启动各种后置处理器**BeanFactoryPostProcessor**，后置处理器是一种回调函数，它可以在Bean实例化、初始化之前或之后进行操作，比如修改Bean属性、替换Bean对象等【这个过程主要做的是对beanDifinition的修改以及补充】。Spring框架中有很多内置的后置处理器。

- this.invokeBeanFactoryPostProcessors(beanFactory);// beanFactory后处理器，充当beanFactory的扩展点，可以用来修改或者补充beanDefinition。（1）例如如果在xml文件中配置的bean标签中的属性的值是通过${}去配置文件中获取的话，那么在创建benaFactory的时候解析bean标签得到的beanDefinition中的值还是${}，是在这一步进行替换的。（2）再例如注解扫描是由ConfigurationClassPostProcessor（配置类后置处理器）执行的，这个后置处理器是在invokeBeanFactoryPostProcessors(beanFactory)方法中调用的。此时会解析@Configuration、@Bean @Import @PropertySource等注解

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**3、创建bean**

创建bean的过程具体可以分成3步： 实例化Bean、依赖注入、初始化Bean

**Spring容器开始加载启动和初始化所有的非懒加载的单例Bean对象【非单例bean：在getBean的时候才会创建bean对象】**，根据BeanDefinition通过反射来创建对象 在堆中开辟内存空间此时属性为默认值’

实例化bean后填充bean对象属性、Spring容器会根据bean定义中的依赖关系，自动将依赖的bean注入到需要的bean中。

初始化bean操作【执行Aware接口的方法 、执行beanPostProcesssor前置处理，检查是否实现了InitializingBean接口、检查是否配置了有自定义的init-method方法】初始化构造方法、bean的后置处理，

将创建好的bean对象放入单例池中。

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**4、设置代理对象：如果bean需要被AOP切面增强，则容器会为其创建代理对象。**

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**5、完成容器初始化：所有bean初始化完成后，Spring容器启动完成。**

- 创建容器：Spring容器启动后会创建一个容器实例，容器负责管理bean的生命周期和依赖关系。
- 扫描包并创建bean定义：Spring容器会扫描指定的包路径，自动创建包中标注了@Component、@Service、@Controller、@Repository等注解的类的bean定义。
- 解析依赖关系：Spring容器会根据bean定义中的依赖关系，自动将依赖的bean注入到需要的bean中。
- 初始化bean：容器会按照指定的顺序依次对bean进行初始化，包括实例化、属性注入、初始化方法执行等。
- 设置代理对象：如果bean需要被AOP切面增强，则容器会为其创建代理对象。
- 完成容器初始化：所有bean初始化完成后，Spring容器启动完成。





> **（1）启动容器的入口是一个构造方法，会把spring的配置信息作为参数传入**
>
> > 如果使用的是xml进行的开发，会在构造方法中将spring配置文件的地址当做参数传入
> >
> > 如果使用的是注解开发，会在构造方法中将spring配置类作为参数传入
>
> **（2）在构造方法中有一个叫做refresh()的方法，执行这个方法会启动Spring容器**
>
> **（3）在refresh()方法中**
>
> - prepareRefresh() ： 准备工作
>
> > 首先会先进行一些准备和初始化的操作
>
> - obtainFreshBeanFactory(); 获取beanFactory实例对象
>
> > 创建beanFactory实例对象，该对象中有一个叫做beanDefinitionMap的属性，里面存放的是bean定义信息
> >
> > （用来创建bean对象的蓝图）
> >
> > 有一个接口叫做beandefinitionReader,有各种实现类来解析这些配置信息得到beanDifinition对象，存放在beanDefinitionMap中【来源有多种 xml、组件扫描、配置类等等】
> >
> > - 例如根据xml中的bean标签进行解析，每一个bean标签就是一个beanDifinition对象，存放在beanDefinitionMap中，
>
> - 扩展点 BeanFactoryPostProcessors 
>   - this.postProcessBeanFactory(beanFactory);		  // 留给子类扩展
>   - this.invokeBeanFactoryPostProcessors(beanFactory);
>
> ```java
> 
> this.invokeBeanFactoryPostProcessors(beanFactory);// beanFactory后处理器，充当beanFactory的扩展点，可以用来修改或者补充beanDefinition。（1）例如如果在xml文件中配置的bean标签中的属性的值是通过${}去配置文件中获取的话，那么在创建benaFactory的时候解析bean标签得到的beanDefinition中的值还是${}，是在这一步进行替换的。（2）再例如注解扫描是由ConfigurationClassPostProcessor（配置类后置处理器）执行的，这个后置处理器是在invokeBeanFactoryPostProcessors(beanFactory)方法中调用的。此时会解析@Configuration、@Bean @Import @PropertySource等注解
> //1、ConfigurationClassPostProcessor implement BeanDefinitionPostProcessor 
> //2、BeanDefinitionPostProcessor 是 BeanFactoryPostProcessors的子接口
> 
> ```
>
> - - this.registerBeanPostProcessors(beanFactory);
>
>   - this.initMessageSource();
>
>   - this.initApplicationEventMulticaster();
>
>   - this.onRefresh();
>
>   - this.registerListeners();
>
>   - this.finishBeanFactoryInitialization(beanFactory);
>
>     - 在这个方法中创建bean对象
>     - 方式 ：反射【】
>     - 
>
>   - this.finishRefresh();
>
>     
>

# 4、Spring bean

# 4.1 什么是 Spring Bean？

- **简单来说，Bean 代指的就是那些被 IoC 容器所管理的对象。**

## 1、怎么配置Bean?

配置Bean 具有三种方法

- 使用xml配置文件进行配置，<bean>标签
- 使用java 配置 ，@bean
- 使用Spring提供的注解

## 2、将一个类声明为 Bean 的注解有哪些?

@component、@Service、@Controller、@Repository

## 3、注入 Bean 的注解有哪些？

@Autowire

@Resource

## 4、@Autowired 和 @Resource 的区别是什么？

`@Autowired`和`@Resource`是用于依赖注入的注解，用于将依赖对象自动注入到目标类中。它们的区别如下：

1. 来源：`@Autowired`是Spring框架提供的注解，而`@Resource`是Java EE标准提供的注解。
2. 依赖查找方式：`@Autowired`通过类型（byType）进行依赖查找和自动装配，它会根据类型在Spring容器中查找匹配的bean并进行注入。`@Resource`通过名称（byName）进行依赖查找和自动装配，它会根据指定的名称在Spring容器中查找匹配的bean并进行注入。
3. 优先级：当存在多个匹配的bean时，`@Autowired`默认按照类型进行匹配，如果存在多个相同类型的bean，会抛出异常。可以通过`@Qualifier`注解来指定具体要注入的bean。而`@Resource`默认按照名称进行匹配，可以通过`name`属性指定具体要注入的bean名称。
4. 应用范围：`@Autowired`注解在Spring框架中更常用，适用于Spring的依赖注入。`@Resource`注解是Java EE标准的一部分，适用于各种Java EE容器，也可以在Spring中使用。

# 4.2 Spring bean的生命周期

**生命周期** ： 从对象的创建到使用销毁的过程，创建===> 使用 ===>销毁 

**创建Bean （ 实例化Bean 、设置Bean的属性值、初始化Bean ）** 

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**实例化阶段之前** ：Spring容器启动的时候，Spring会解析配置文件，**将在配置文件中配置的bean标签都转化为beanDefination对象**，`beanDefinitionNames` 中存放的是 beanDefinition 的名称。

> `beanDefinitionNames` 提供了一种查找和遍历所有注册的 bean 的方式。通过这个数组，我们可以获取所有 bean 的名称，进而获取相应的 beandefinition

>  非懒加载的单例bean才会在Spring容器启动的时候进行实例化的步骤 、非单例Bean会在需要使用的时候才会创建

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**实例化阶段总结** ：需要创建Bean的时候先获取对应的beanDefinition对象，从beanDefinition中拿到BeanClass， 利用反射机制创建对象【getDeclaredConstructor()  拿到这个类的构造方法，调用newInsatnce()创建实例对象】完成bean的实例化，此时分配了内存空间，但是属性还是默认值。

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**填充Bean的属性值【依赖注入过程】总结：**bean实例化之后需要进行属性填充，如果当前对象中要注入其他的对象，那么Spring会先去单例池中进行查找，如果查找不到会把当前正在创建的对象存放在单例池中，先去创建依赖的对象之后才继续来完成当前对象的创建



- 会存在循环依赖问题 ： 解决方法是三级缓存 【解决的只是单例模式下的 Bean 属性循环依赖问题，对于多例 Bean 和 Prototype 作用域的 Bean的循环依赖问题，并不能使用三级缓存设计解决。】

  - 创建对象 A，完成生命周期的第一步，即实例化（Instantiation），在调用 `createBeanInstance` 方法后，会调用 `addSingletonFactory` 方法，将已实例化但未属性赋值未初始化的对象 A 放入三级缓存 `singletonFactories` 中。即将对象 A 提早曝光给 IoC 容器。
  - 

- Pojo类不使用AOP增强的话、二级缓存就够了

  - **如果 Spring 选择二级缓存来解决循环依赖的话，那么就意味着所有 Bean 都需要在实例化完成之后就立马为其创建代理，而 Spring 的设计原则是在 Bean 初始化完成之后才为其创建代理。**

    > 使用三级缓存而非二级缓存并不是因为只有三级缓存才能解决循环引用问题，其实二级缓存同样也能很好解决循环引用问题。使用三级而非二级缓存并非出于 IOC 的考虑，而是出于 AOP 的考虑，即若使用二级缓存，在 AOP 情形注入到其他 Bean的，不是最终的代理对象，而是原始对象。

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**初始化Bean阶段总结：**

- **执行Aware接口的方法 并且设置相关的属性：**Aware 接口的作用 ：当spring容器创建bean对象的时候，如果当前对象要用到Spring容器中的其他对象，此时可以将此对象实现Aware接口来满足当前的需要
- **执行beanPostProcesssor前置处理**  前置处理阶段的主要目的是在bean的初始化之前，对其进行一些自定义操作或准备工作，以确保在bean完全初始化之前满足特定需求或条件，例如检查bean的属性，并在初始化之前根据特定条件进行动态设置或修改属性的值。
- **检查是否实现了InitializingBean接口？检查是否配置了有自定义的init-method方法？**
- **执行beanPostProcesssor后置处理**

对象创建完成，放入单例池中，

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**使用Bean阶段**： 通过容器对象调用getBean()方法，获取bean

![img](file:///C:\Users\16055\AppData\Local\Temp\SGPicFaceTpBq\3544\059E8E62.png)**销毁bean：**

- 当要销毁 Bean 的时候，如果 Bean 实现了 `DisposableBean` 接口，执行 `destroy()` 方法。
- 当要销毁 Bean 的时候，如果 Bean 在配置文件中的定义包含 destroy-method 属性，执行指定的方法



![img](https://img2020.cnblogs.com/blog/1771072/202009/1771072-20200909164026351-1683760583.png)

**实例化Bean ：**

- Bean 容器找到配置文件中 Spring Bean 的定义。
- Bean 容器利用 反射 创建一个 Bean 的实例。
- 检查Bean是否实现了`Aware` 接口 ，就调用相应的方法。
- 如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessBeforeInitialization()` 方法
- 如果 Bean 实现了`InitializingBean`接口，执行`afterPropertiesSet()`方法。
- 如果 Bean 在配置文件中的定义包含 init-method 属性，执行指定的方法。

- 如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessAfterInitialization()` 方法

  当要销毁 Bean 的时候，如果 Bean 实现了 `DisposableBean` 接口，执行 `destroy()` 方法。

  当要销毁 Bean 的时候，如果 Bean 在配置文件中的定义包含 destroy-method 属性，执行指定的方法


# 4.3循环依赖问题

https://juejin.cn/post/7099745254743474212

1. 什么是循环依赖，spring是如何解决的

   循环依赖顾名思义就是类与类之间的关系形成了闭环。比如类A中依赖了类B，类B中有依赖了类A。

   产生循环依赖的情况有三种：

   1. 通过构造方法进行依赖注入时产生的循环依赖问题。
   2. 通过setter方法进行依赖注入且是在多例（原型）模式下产生的循环依赖问题。
   3. 通过setter方法进行依赖注入且是在单例模式下产生的循环依赖问题。

2. spring能够解决哪些循环依赖的问题

   spring只解决了第三种情况的循环依赖，因为，第一种情况在new对象时就会阻塞住

   第二钟情况，每一次getbean都会产生一个新的bean，那么反复下去就会OOM。

   所以spring能够解决的缓存依赖只有

   **（setter方法注入，且单例模式下）**

3. spring如何解决循环依赖的问题

   spring中有三个缓存，用于存储单例的bean实例对象，这三个缓存时彼此相互排斥的，不会针对同一个bean实例同时存储。

   如果带哦用getBean方法，则需要从三个缓存中依次获取指定的bean实例。

   读取顺序依次是一级缓存 ==> 二级缓存 ==> 三级缓存。

   主要是使用二级缓存和三级缓存来解决循环依赖的问题的。

   具体spring如何解决循环依赖的问题：（setter注入引起的循环依赖）

   认识三级缓存：

   一级缓存：singletonObjects

   二级缓存：earlySingletonObjects

   三级缓存：singletonFactories

   singletonsCurrentlyInCreation：这是一个set集合，存储的是正在创建但还未完全创建成过的bean

   例子：类A依赖类B，类B依赖类A。

   在通过A的构造方法创建类A后，会将类A存储在三级缓存singletonFactories中和singletonsCurrentlyInCreation中，发现A依赖B，于是通过类B的构造方法创建B，也存储在三级缓存中与singletonsCurrentlyInCreation，此时的A、B都没有完成DI，类B又依赖类A，有开始创建A，此时，从一级缓存中没有获取到A，但是singletonsCurrentlyInCreation却含有A，（基本可以确定发生了循环依赖），从二级缓存中也没有获取到A，从三级缓存获取到A后，将A添加到二级缓存中，并从三级缓存中删除A。将A注入B中，就解决了循环依赖。

4. 如何解决构造函数相互注入造成的循环依赖

   可以使用@Lazy注解来解决。

   @Lazy实现原理是，当实例化对象时，如果发现参数或者属性有@Lazy注解修饰，那么就不直接创建所依赖的对象了，而是使用动态代理创建一个代理类。

   比如，类A的创建：A a=new A(B)，需要依赖对象B，发现构造函数的形参上有@Lazy注解，那么就不直接创建B了，而是使用动态代理创建了一个代理类B1，此时A跟B就不是相互依赖了，变成了A依赖一个代理类B1，B依赖A。但因为在注入依赖时，类A并没有完全的初始化完，实际上注入的是一个代理对象，只有当他首次被使用的时候才会被完全的初始化。 