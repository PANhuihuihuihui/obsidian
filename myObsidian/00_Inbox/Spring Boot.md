After learning the Udacity Java Developer course, I still don't not how spring boot work. Hence I translate this [blog](https://zhuanlan.zhihu.com/p/109273436) to have a better understanding.
## Spring boot I: Intro
### 1. The birth of Spring Boot
Spring 这个企业

### The Feature of Spring Boot
```

```

#### Spring Boot 核心配置
**1. 入口类和@SpringBootApplication** 
上面我们通过创建项目知道了，每次创建项目系统会给我们生成一个入口类，例如上面的  DemoApplication   入口类中有一个main方法，这个main放在其实就是一个标准的Java 应用的入口方法， 在mian方法中使用 SpringApplication.run(DemoApplication.class, args); 启动Spring Boot 项目。  
同时入口类中有一个默认的注解 @SpringBootApplication，该注解是Spring Boot 的核心注解，同时也是一个组合注解，@SpringBootApplication 注解组合了，如下三个注解：`@SpringBootConfiguration, @EnableAutoConfiguration, @ComponentScan`
1, SpringBootConfiguration实际上就是@Configuration注解，表明这个类是一个配置类，
2, EnableAutoConfiguration则表示让Spring Boot根据类路径中的jar包依赖为当前项目进行自动配置，
3, ComponentScan的作用不在详细描述，需要注意的是如果我们使用了@SpringBootApplication注解的话，**系统会去入口类的同级包以及下级包中去扫描实体类**，因此我们建议入口类的位置在groupId+arctifactID组合的包名下。
**2. 关闭特定的自动配置**
上一节我们讲到 组合注解中的 @ComponentScan 注解，该注解有过滤器的作用，如果我们需要关闭特定的自动配置应该使用@SpringBootApplication注解的 exclude参数，例如：
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})

