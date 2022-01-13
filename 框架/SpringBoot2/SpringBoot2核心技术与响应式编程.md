# SpringBoot2核心技术与响应式编程



> - 在idea左侧有个锚点可以定位当前资源所在的包位置；
> - 右击选择Evaluate express可以计算表达式（debug的时候也可以用）
>
> 
>
> - ctrl+enter 下一行
>
> - ctrl+/ 切换源代码模式和浏览模式
>
> - idea中快捷键.var或者"hello".sout这种方法比较快
>
> - 资料页
>
>     [语雀官网上的资料](https://www.yuque.com/atguigu/springboot)
>
>     [Spring官网](https://spring.io/)
>
>     [Spring生态](https://spring.io/projects/spring-boot)
>
>     [视频地址](https://www.gulixueyuan.com/)
>
>     [源码地址](https://gitee.com/leifengyang/springboot2)
>
> - SpringBoot
>
> 1. [官网区](https://spring.io/projects/spring-boot#learn)
> 2. [Reference Doc.](https://docs.spring.io/spring-boot/docs/current/reference/html/)
> 3. [API Doc.](https://docs.spring.io/spring-boot/docs/current/api/)
> 4.  [the project release notes section](https://github.com/spring-projects/spring-boot/wiki#release-notes)
> 5. [Common Application properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties)
> 6. [Dependency Versions](https://docs.spring.io/spring-boot/docs/current/reference/html/dependency-versions.html#dependency-versions)

<hr />



[TOC]



<hr />

## SpringBoot2核心技术

### SpringBoot2基础入门

<hr />

#### Spring能做什么？

- Microservices 
    - 微服务
- Reactive 
    - 响应式编程
- Cloud 
    - 分布式应用
- Web apps
    - Web开发
- Serverless
    - 无服务开发，即函数级服务
- Event Driven
    - 事件驱动，构建事实数据流通过响应式的方式去让系统占用少量资源去完成高吞吐量作业
- Batch
    - 批处理
- [Spring生态](https://spring.io/projects/spring-boot)
- Spring5升级新特性
    - 响应式编程
        - Servlet Stack
        - Reactvie Stack
    - 内部源码设计
        - 基于Java8的一些新特性，如：接口默认实现。
        - 重新设计源码架构。

<hr />

#### 为什么用SpringBoot？

- Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".
     - [引自官网](https://spring.io/projects/spring-boot)
     - 即能快速创建出生产级别的Spring应用。

 - SpringBoot优点

     - [引自官网](https://spring.io/projects/spring-boot)
     - 创建独立Spring应用
     - 内嵌web服务器
         - 直接嵌入Tomcat、Jetty或Undertow（无需部署WAR文件）
     - 自动starter依赖，简化构建配置
     - 自动配置Spring以及第三方
     - 提供生产级别的监控、健康检查以及外部化配置
     - 无代码生成、无需编写XML

 - SpringBoot是什么？

     - SpringBoot是整合Spring技术栈的一站式框架
     - SpringBoot是简化Spring技术栈的快速开发脚手架

> - 相关知识
>
>     - 微服务
>
>       - > In short, the **microservice architectural style** is an approach to developing a single application as a **suite of small services**, each **running in its own process** and communicating with **lightweight** mechanisms, often an **HTTP** resource API. These services are **built around business capabilities** and **independently deployable** by fully **automated deployment** machinery. There is a **bare minimum of centralized management** of these services, which may be **written in different programming languages** and use different data storage technologies.-- [James Lewis and Martin Fowler (2014)](https://martinfowler.com/articles/microservices.html)
>
>       - > - 微服务是一种架构风格
>         > - 一个应用拆分为一组小型服务
>         >
>         > - 每个服务运行在自己的进程内，也就是可独立部署和升级
>         > - 服务之间使用轻量级HTTP交互
>         >
>         > - 服务围绕业务功能拆分
>         > - 可以由全自动部署机制独立部署
>         >
>         > - 去中心化，服务自治。服务可以使用不同的语言、不同的存储技术
>
>     - 分布式
>
>         - 分布式的困难
>             - 远程调用
>             - 服务发现
>             - 负载均衡
>             - 服务容错
>             - 配置管理
>             - 服务监控
>             - 链路追踪
>             - 日志管理
>             - 任务调度
>         - 分布式的解决
>             - SpringBoot + SpringCloud + Spring Cloud Data Flow
>
>     - 云原生
>
>         > 原生应用如何上云。 Cloud Native
>
>         - 上云的困难
>             - 服务自愈
>             - 弹性伸缩
>             - 服务隔离
>             - 自动化部署
>             - 灰度发布
>             - 流量治理
>         - 上云的解决
>             - [如课程](https://www.gulixueyuan.com/my/course/474)

- SpringBoot Reference Documentation
    1. [官网区](https://spring.io/projects/spring-boot#learn)
    2. [Reference Doc.](https://docs.spring.io/spring-boot/docs/current/reference/html/)
    3. [API Doc.](https://docs.spring.io/spring-boot/docs/current/api/)
    4.  [the project release notes section](https://github.com/spring-projects/spring-boot/wiki#release-notes)
    5. [Common Application properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties)

<hr />

#### 快速体验SpringBoot

- [系统要求](https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started.system-requirements)

    - Spring Boot 2.6.2 requires [Java 8](https://www.java.com/) and is compatible up to and including Java 17. [Spring Framework 5.3.14](https://docs.spring.io/spring-framework/docs/5.3.14/reference/html/) or above is also required.

        Explicit build support is provided for the following build tools:

        | Build Tool | Version               |
        | :--------- | :-------------------- |
        | Maven      | 3.5+                  |
        | Gradle     | 6.8.x, 6.9.x, and 7.x |

    - 检查一下自己环境

        ```shell
        C:\Users\13674>java -version
        java version "1.8.0_301"
        Java(TM) SE Runtime Environment (build 1.8.0_301-b09)
        Java HotSpot(TM) 64-Bit Server VM (build 25.301-b09, mixed mode)
        
        C:\Users\13674>mvn -v
        Apache Maven 3.8.1 (05c21c65bdfed0f71a2f2ada8b84da59348c4c5d)
        Maven home: C:\Program Files (x86)\maven\apache-maven-3.8.1\bin\..
        Java version: 1.8.0_301, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jdk1.8.0_301\jre
        Default locale: zh_CN, platform encoding: GBK
        OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
        ```

    - maven->conf->settings.xml修改

        ```xml
            <!-- 阿里云镜像-->
            <mirrors>
                  <mirror>
                    <id>nexus-aliyun</id>
                    <mirrorOf>central</mirrorOf>
                    <name>Nexus aliyun</name>
                    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
                  </mirror>
              </mirrors>
             <!--maven使用java1.8进行编译-->
              <profiles>
                     <profile>
                          <id>jdk-1.8</id>
                          <activation>
                            <activeByDefault>true</activeByDefault>
                            <jdk>1.8</jdk>
                          </activation>
                          <properties>
                            <maven.compiler.source>1.8</maven.compiler.source>
                            <maven.compiler.target>1.8</maven.compiler.target>
                            <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
                          </properties>
                     </profile>
              </profiles>
        ```

    - Hello,world

        > 需求：浏览发送/hello请求，响应：Hello World!

        1. 创建maven工程

        2. 引入依赖

          ```xml
          <parent>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-parent</artifactId>
              <version>2.6.2</version>
          </parent>
          
          <dependencies>
              <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-web</artifactId>
              </dependency>
          </dependencies>
          ```

        3. 创建主程序

            ```java
            @SpringBootApplication
            public class MyApplication {
                public static void main(String[] args) {
                    SpringApplication.run(MyApplication.class, args);
                }
            }
            ```

        4. 编写业务

            ```java
            @RestController
            public class HelloController {
            
                @RequestMapping("/hello")
                public String handle01(){
                    return "Hello World!";
                }
            }
            ```

        5. 测试

            - http://localhost:8080/hello

        6. 简化配置

            - 在resources目录下创建的application.properties配置文件中

                ```properties
                server.port=8888
                ```

            - 测试

                - http://localhost:8888/hello

            - 配置依据

                - [Common Application properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties)

        7. 简化部署

            1. 引入插件至Pom

                ```xml
                <build>
                    <plugins>
                        <plugin>
                            <groupId>org.springframework.boot</groupId>
                            <artifactId>spring-boot-maven-plugin</artifactId>
                        </plugin>
                    </plugins>
                </build>
                ```

            2. Save your `pom.xml` and run `mvn package` from the command line

                ```shell
                $ mvn package
                ```

            3. To run that application, use the `java -jar` command
            
                ```shell
                $ java -jar target/myproject-0.0.1-SNAPSHOT.jar
                ```
            
            4. 测试
            
                - http://localhost:8888/hello

<hr />

#### 自动配置原理入门

- SpringBoot特点

    - 依赖管理

        - 父项目做依赖管理

            ```xml
                <!-- 依赖管理 -->
                    <parent>
                        <groupId>org.springframework.boot</groupId>
                        <artifactId>spring-boot-starter-parent</artifactId>
                        <version>2.6.2</version>
                    </parent>
            
                <!-- 它的父项目中规定的依赖管理，几乎声明了所有开发中常用的依赖的版本号，即Maven的自动版本仲裁机制 -->
                  <parent>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-dependencies</artifactId>
                    <version>2.6.2</version>
                  </parent>
            
                <!-- 如果需要自定义依赖，则带版本号重写即可 -->
            ```

        - starter场景启动器：[Starters](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters)

            1. starter是一系列依赖的集合描述，一般引入一个starter，它的完整的开发场景就被完全引入，这个场景的所有常规需要的依赖我们都自动引入，无需额外引用依赖。
            2. 命名习惯
                1. 所有**官方**首发都遵循类似的命名模式；`spring-boot-starter-*`，其中`*`是特定类型的应用程序。
                    - 此命名结构旨在在您需要查找入门时提供帮助。许多 IDE 中的 Maven 集成允许您按名称搜索依赖项。例如，安装适当的 Eclipse 或 Spring Tools 插件后，您可以`ctrl-space`在 POM 编辑器中按并键入“spring-boot-starter”以获得完整列表。
                2. 第三方启动器不应以 开头`spring-boot`，因为它是为官方 Spring Boot 工件保留的。相反，第三方启动器通常以项目名称开头。
                    - 例如，名为的第三方启动项目`thirdpartyproject`通常命名为`thirdpartyproject-spring-boot-starter`。
                3. [表 1. Spring Boot 应用程序启动器](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters)
                4. 所有场景启动器最底层的依赖

                    ```xml
                        <dependency>
                            <groupId>org.springframework.boot</groupId>
                            <artifactId>spring-boot-starter</artifactId>
                            <version>2.3.4.RELEASE</version>
                            <scope>compile</scope>
                        </dependency>
                    ```

        - 一般无需关注版本号，自动版本仲裁

            - 如果引入的非版本仲裁的jar要写版本号

        - 修改版本号

            ```xml
                <!-- 1、查看spring-boot-dependencies里面规定当前依赖的版本用的 key -->
                <!-- 2、在当前项目pom中重写配置 -->
                    <properties>
                        <mysql.version>5.1.43</mysql.version>
                    </properties>
            	<!-- 或者重写，我觉得重写更好用 -->
                    <dependency>
                        <groupId>mysql</groupId>
                        <artifactId>mysql-connector-java</artifactId>
                        <version>8.0.26</version>
                    </dependency>
            ```

    - 自动配置

        - 自动配好tomcat

            - 引入的场景中拥有tomcat依赖或引入依赖

            - 配置tomcat

                ```xml
                    <dependency>
                        <groupId>org.springframework.boot</groupId>
                        <artifactId>spring-boot-starter-tomcat</artifactId>
                        <version>2.6.2</version>
                        <scope>compile</scope>
                    </dependency>
                ```

        - 自动配好SpringMVC

            - 引入的场景中拥有SpringMVC依赖或引入依赖

            - 自动配好SpringMVC常用组件（功能）

                ```xml
                    <dependency>
                        <groupId>org.springframework</groupId>
                        <artifactId>spring-web</artifactId>
                        <version>5.3.14</version>
                        <scope>compile</scope>
                    </dependency>
                    <dependency>
                        <groupId>org.springframework</groupId>
                        <artifactId>spring-webmvc</artifactId>
                        <version>5.3.14</version>
                        <scope>compile</scope>
                    </dependency>
                ```

        - 自动配好Web常见功能

            - 配置好了所有web开发的常见场景

                - 如：字符编码问题、视图解析器、文件上传等等...

                ```java
                @SpringBootApplication
                public class MyApplication {
                    public static void main(String[] args) {
                        //1. 返回IOC容器
                        ConfigurableApplicationContext run = SpringApplication.run(MyApplication.class, args);
                        //2. 查看容器里面的组件
                        String[] names = run.getBeanDefinitionNames();
                        for(String name: names) {
                            System.out.println("容器名:"+name);
                        }
                    }
                }
                ```

        - 默认的包结构

            > 1. We generally recommend that you locate your main application class in a root package above other classes. The [`@SpringBootApplication` annotation](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.using-the-springbootapplication-annotation) is often placed on your main class, and it implicitly defines a base “search package” for certain items. For example, if you are writing a JPA application, the package of the `@SpringBootApplication` annotated class is used to search for `@Entity` items. Using a root package also allows component scan to apply only on your project.
            >
            >     | tips | 1. SpringApplication是一个合成注解：If you do not want to use `@SpringBootApplication`, the `@EnableAutoConfiguration` and `@ComponentScan` annotations that it imports defines that behavior so you can also use those instead.2.或者也可以@SpringBootApplication(scanBasePackages = "扫描范围") |
            >     | ---- | ------------------------------------------------------------ |
            >
            >     
            >
            > 2. 主程序所在的包及其下面的所有子包里面的组件都会被默认扫描进来The following listing shows a typical layout:
            >
            > ```txt
            > com
            >  +- example
            >      +- myapplication
            >          +- MyApplication.java
            >          |
            >          +- customer
            >          |   +- Customer.java
            >          |   +- CustomerController.java
            >          |   +- CustomerService.java
            >          |   +- CustomerRepository.java
            >          |
            >          +- order
            >              +- Order.java
            >              +- OrderController.java
            >              +- OrderService.java
            >              +- OrderRepository.java
            > ```

            ```java
            @SpringBootApplication
            等同于
            @SpringBootConfiguration
            @EnableAutoConfiguration
            @ComponentScan("com.example")
            ```

        - 各种配置拥有默认值

            - 如上传文件大小

                ```properties
                # 默认为1MB
                spring.servlet.multipart.max-file-size=10MB
                ```

            - 配置文件的值最终会绑定到每个类上，这个类会在容器中创建对象

                - 如上述默认配置最终都是映射到MultipartProperties

        - 按需加载所有配置项

            - 引入哪些场景，哪个场景的自动配置才会自动开启

                - 如当前示例中只会将spring-boot-starter-web中配置项加载进来

            - SpringBoot的所有自动配置功能都在该包下

                - 可以去相应的依赖包下查看
                    - 虽然引入了众多类，但不是都生效
                    - 有泛红的部分，需要引入场景后生效

                ```xml
                    <dependency>
                        <groupId>org.springframework.boot</groupId>
                        <artifactId>spring-boot-autoconfigure</artifactId>
                        <version>2.6.2</version>
                        <scope>compile</scope>
                    </dependency>
                ```

        - etc...


- 容器功能

    - 组件添加

        - 底层注解-@Configuration详解

            - 设有两个Bean

                - ```java
                    public class User {
                        private String name;
                        private Integer age;
                
                        public User(){}
                
                        public User(String name, Integer age) {
                            this.name = name;
                            this.age = age;
                        }
                
                        public String getName() {
                            return name;
                        }
                
                        public void setName(String name) {
                            this.name = name;
                        }
                
                        public Integer getAge() {
                            return age;
                        }
                
                        public void setAge(Integer age) {
                            this.age = age;
                        }
                
                        @Override
                        public String toString() {
                            return "User{" +
                                    "name='" + name + '\'' +
                                    ", age=" + age +
                                    '}';
                        }
                    }
                    ```

                - ```java
                    public class Pet {
                        private String name;
                
                        public Pet(){}
                
                        public Pet(String name) {
                            this.name = name;
                        }
                
                        public String getName(){
                            return this.name;
                        }
                
                        public void setName(String name){
                            this.name = name;
                        }
                
                        @Override
                        public String toString() {
                            return "Pet{" +
                                    "name='" + name + '\'' +
                                    '}';
                        }
                    }
                    ```

            - 然后有相应的一个配置类
            
                - ```java
                    /**
                    *	
                    *	1. 配置类里面使用@Bean标注在方法上给容器注册组件，默认也是单实例的
                    * 	2. MyConfig本身也是一个容器中的组件，组件名称为myConfig
                    *	3. @Configuration的boolean proxyBeanMethods() default true;--代理bean的方法
                    		Full(proxyBeanMethods = true)	保证每个@Bean方法被调用多少次返回的组件都是单实例的
                    		Lite(proxyBeanMethods = false)	每个@Bean方法被调用多少次返回的组件都是新创建的
                    		最佳实战:组件依赖
                    			组件依赖必须使用Full模式默认。其他默认使用Lite模式
                                配置类组件之间有依赖关系，方法会被调用得到之前单实例组件，用Full模式
                                配置类组件之间无依赖关系，用Lite模式加速容器启动过程，减少判断
                    	4.//给容器中自动创建出这两个类型的组件，默认组件的名字就是全限定类名
                    		@Import({User.class, LogManagerStatus.class})
                    		打印容器有:
                    			org.yewenxue.boot.bean.User
                    			org.apache.logging.log4j.internal.LogManagerStatus
                    	5.@Conditional
                    		条件装配：满足Conditional指定的条件，则进行组件注入
                    		如： @ConditionalOnMissingBean(name = "user01")
                    		测试:
                    			1)首先注释掉宠物组件的@Bean
                    			2)此时只有user01被注册进容器，tomcatPet没有被注册进去
                    			3)因为user01依赖tomcatPet，组件依赖，我们想要的是，如果容器中没有tomcatPet组件，也就不要去注册user01组件，所以可以在user01的@Bean的附近加上注解@ConditionalOnBean(name = "tomcatPet")
                    			4)此时容器这两个组件一个都没有加载
                    			*)也可以注解至类上
                    			
                    
                    
                    (外部无论对配置类中的这个组件注册方法调用多少次获取的都是之前注册容器中的单实例对象,如果@Configuration(proxyBeanMethods = true)代理对象调用方法,SpringBoot总会检查这个组件是否在容器中，保持组件单实例。)
                    
                    */
                    //该注解告知为这是一个配置类 == 配置类
                    @Configuration
                    //给容器中自动创建出这两个类型的组件
                    @Import({User.class, LogManagerStatus.class})
                    public class MyConfig {
                    
                        //给容器中添加容器，以方法名作为组件的id。返回类型为组件类型。返回的值就是组件在容器中保存的对象，即实例。
                        /**
                        *	外部无论对配置类中的这个组件注册方法调用多少次获取的都是之前注册容器中的单实例对象
                        */
                        @Bean
                        public User user01() {
                            return new User("zhangsan",18);
                        }
                    //如果不想用方法名作为组件的名称，可以给Bean注解添加相应的内容,如@Bean("tom")
                        @Bean
                        public Pet tomcatPet() {
                            return new Pet("tomcat01");
                        }
                    }
                    
                    ```
            
            - 执行MyApplication后，查看容器中的组件，发现存在user01和tomcatPet两个组件
            
                - ```java
                    @SpringBootApplication
                    public class MyApplication {
                        public static void main(String[] args) {
                            //1. 返回IOC容器
                            ConfigurableApplicationContext run = SpringApplication.run(MyApplication.class, args);
                            //2. 查看容器里面的组件
                            String[] names = run.getBeanDefinitionNames();
                            for(String name: names) {
                                System.out.println(name);
                            }
                            //3. 从容器中获取组件
                            Pet tom01 = run.getBean("tomcatPet", Pet.class);
                            Pet tom02 = run.getBean("tomcatPet", Pet.class);
                            System.out.println("组件："+(tom01 == tom02));//结果为true，证明是单实例
                            
                            MyConfig myConfig = run.getBean(MyConfig.class);
                            System.out.println(myConfig);
                            //如果@Configuration(proxyBeanMethods = true)代理对象调用方法。SpringBoot总会检查这个组件是否在容器中，保持组件单实例
                            User user01 = myConfig.user01();
                            User user02 = myConfig.user01();
                            System.out.println("组件："+(user01 = user02));//true
                        }
                    }
                    ```
            
        - @Bean/@Component/Controller/Service/Repository
        
        - @ComponenScan/@Import

    - 原生配置文件引入 

        - @ImportResource导入Spring配置文件

    - 配置绑定

        - 如何使用Java读取到properties文件中的内容，并且把它封装到JavaBean中，以供随时使用

            - 原生过程

                - ```java
                    public class getProperties {
                         public static void main(String[] args) throws FileNotFoundException, IOException {
                             Properties pps = new Properties();
                             pps.load(new FileInputStream("a.properties"));
                             Enumeration enum1 = pps.propertyNames();//得到配置文件的名字
                             while(enum1.hasMoreElements()) {
                                 String strKey = (String) enum1.nextElement();
                                 String strValue = pps.getProperty(strKey);
                                 System.out.println(strKey + "=" + strValue);
                                 //封装到JavaBean。
                             }
                         }
                     }
                    ```

            - 方式一@ConfigurationProperties

                - SpringBoot的强大功能都需要组件添加到容器中才能够使用
                - 修改application.properties
                - Car的Bean类
                - Controller中依赖注入返回

            - 方式二@Component + @ConfigurationProperties

                - 在配置类中进行
                - 配置类中@EnableConfigurationProperties(Car.class)
                    - 1、开启Car配置绑定功能
                    - 2、把这个Car这个组件自动注册到容器中
                - 









- 自动配置原理入门

    - 引导加载自动配置类
    - 按需开启自动配置项
    - 修改默认配置
    - 最佳实践

- 开发小技巧

    - Lombok
    - dev-tools
    - Spring Initializer



























<hr />

### SpringBoot2核心功能

#### 配置文件

#### Web开发

#### 数据访问

#### JUnit5单元检测

#### 生产指标监控

#### SpringBoot核心原理解析

### SpringBoot场景整合

#### 虚拟化技术

#### 安全控制

#### 缓存技术

#### 消息中间件

#### 分布式入门

## SpringBoot2响应式编程

### 响应式编程基础

#### 响应式编程模型

#### 使用Reactor开发

### Webflux开发web应用

#### Webflux构建RESTful应用

#### 函数式构建RESTful应用

#### RestTemplate与WebClient

### 响应式访问持久化层

#### 响应式访问MySQL

#### 响应式访问Redis

### 响应式安全开发

#### Spring Security Reactive构建安全服务

### 响应式原理

#### 几种IO模型

#### Netty-Reactor

#### 数据流处理原理