---
title: Spring 注解学习-持续更新  
date: 2020/08/11 16:00:00  
tags: 
- spring
categories:	
- spring  
---
## Spring 注解  
### @Bean
### @WebMethod
### @FeignClient  
注解被@Target(ElementType.TYPE)修饰，表示FeignClient注解的作用目标在接口上。  
	name：指定FeignClient的名称，如果项目使用了Ribbon，name属性会作为微服务的名称，用于服务发现  
	url: url一般用于调试，可以手动指定@FeignClient调用的地址   
### @EnableMongoRepositories  
启动类中：让框架创建的Repository接口创建实现类，并添加到Spring容器中进行管理。  
resources目录下：application.properties文件中配置MongoDB的连接字符串。
spring.data.mongodb.uri=mongodb://springbucks:springbucks@xxx.xxx.xxx.xxx:xxxxx/springbucks  
### @RequestMapping  
用来映射请求，也就是通过它来指定控制器可以处理哪些URL请求，相当于Servlet中在web.xml中配置  
1. @Target中有两个属性，分别为 ElementType.METHOD 和 ElementType.TYPE ，也就是说 @RequestMapping 可以在方法和类的声明中使用  
### @RestController  

### @controller  
控制器（注入服务），用于标注控制层，相当于struts中的action层。  
### @service  
服务（注入dao），用于标注服务层，主要用来进行业务的逻辑处理。  
### @repository  
实现dao访问，用于标注数据访问层，也可以说用于标注数据访问组件，即DAO组件。  
### @component  
把普通pojo实例化到spring容器中，泛指各种组件，就是说当我们的类不属于各种归类的时候（不属于@Controller、@Services等的时候），我们就可以使用@Component来标注这个类。
### @Document  
主要体现在pojo实体中，通常要在实体类上注明@Document。
其属性可以标明属于的索引和类型----对应数据库中的数据库名和表名,其中type不预先创建也可以,没预先创建的它会自动创建一个与实体相匹配的type。  
标识要持久保存到MongoDB的域对象。  
### @NoRepositoryBean  
以排除获取存储库接口，从而导致创建实例。  
当为所有存储库提供扩展的基本接口并结合自定义存储库基类以实现在该中间接口中声明的方法时，通常会使用此方法。在这种情况下，您通常是从中间接口派生出具体的存储库接口，但又不想为中间接口创建Spring bean。  
### @SuppressWarnings  
抑制警告，取消警告信息。  
### @Configuration  
指示一个类声明了一个或多个@Bean方法，并且可以由Spring容器处理以在运行时为这些bean生成bean定义和服务请求。  
### @Entity  
指定该类是一个实体。该注释应用于实体类。  
### @Table(name = "DE_WS_OID_DT")  
指定带注释的实体的主表。  
如果没有为实体类指定Table注释，则使用默认值。  
### @NamedQuery  
(用Java Persistence查询语言)指定一个静态的命名查询。查询名称的作用域是持久性单元。(NamedQuery批注可以应用于实体或映射的超类。)  
### @Column  
用于为持久属性或字段指定映射的列。如果未指定Column注解，则应用默认值。  
### @