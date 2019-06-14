---
layout: post
title:  Spring Boot configurations
date:   2019-06-14 00:00:00 +0300
categories: ssh
tag: [ssh] # add tag
---

* content
{:toc}


## 概述
最近搞的项目涉及到了Spring Boot，之前Spring用的比较多，这里简单记录一下Spring Boot的一些常用配置备用。一些基本概念传承自Spring的如IoC和AOP就不详细介绍了。

来个原版，要想看的明白还是得原版比较清楚：
[Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/current/reference/html/)

英文不好的小伙伴看这个中文版的也还凑合:
[Spring Boot手册](http://www.ybao.org/book/springboot/6143.html)

---

### 1. Spring Boot 常用注解

-  @SpringBootApplication

    主类（入口类）的注解。（@Configuration，@EnableAutoConfiguration ， @ComponentScan）

- @Repository

    DAO层注解，DAO层中接口继承JpaRepository<T,ID extends Serializable>,需要在build.gradle中引入相关jpa的一个jar自动加载。

- @Service

    ServiceImpl上面注解，注意不是Service接口，而是接口的实现类上。

- @Entity

    SpringMVC中model层相当于SpringBoot中的entity层，@Entity注解在实体类(domain层)上面。@Table(name ="数据库表名")，这个注解也注释在实体类上，对应数据库中相应的表。@Id、@Column注解用于标注实体类中的字段，pk字段标注为@Id，其余@Column。

- @RestController

    Controller层注解，@RestController相当于@Controller + @ResponseBody

    特殊的，若该控制器用于跳转JSP页面，必须用@Controller标注，否则不予跳转。

- @RequestMapping

    @RequestMapping是一个用来处理请求地址映射的注解，用于类或方法上，用于类上，表示类中所有响应请求的方法都是以该路径为父路径；

- @Autowired

    自动装配，自动导入依赖的beans，一般自动注入*Mapper或者*Service到另一层。

- @PathVariable

    用来处理占位符，类似user/{id}的路径，参数中需要@PathVariable(value="id") String id，为了避免犯错，尽量命名相同。

- @ResponseBody

    Controller方法返回结果直接写入HTTP response body中，一般在异步ajax获取数据时使用。

    也就是后台向前台返回结果的时候写此标签。

- @RequestBody

    对json格式的参数转换为Java类型。

- @RequestParam

    用在方法参数之前@RequestParam String id =request.getParameter("id");

---

### 2. 跨域访问

```
/**
 * CORS configuration
 */
@Configuration
public class CORSConfig {

    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurerAdapter() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**")
                        .allowedOrigins(ALL)
                        .allowedMethods(ALL)
                        .allowedHeaders(ALL)
                        .allowCredentials(true);
            }
        };
    }

}
```

---

### 3. Spring Data JPA

    访问数据库的方式有两个流派，一派以SQL为中心，在JDBC上做了一定程度的封装，比 直接操作JDBC更加方便和便捷流行DAO工具MyBatis也属于这个流派。
    另外一个流派则是以Java Entity为中心，将实体和实体关系对应到数据库的表和表关系， 这类工具通常就是ORM (Object Relational Mapping)工具。对实体和实体关系的操作会映射到 数据库操作。

  -  创建 Entity
  
    自增主键
    @GeneratedValue(strategy=GenerationType.IDENTITY)

  - Repository

    JpaRepository:真的很省事，一些基本的简单查询不用自己写了，直接用就好了，啥也不说了，见示例

    ```
    public interface PersonsRepository extends JpaRepository<Persons, Long> {

        public static final String FIND_SEX = "select DISTINCT sex from Persons p";

        @Query(FIND_SEX)
        List<Persons> findSex();

        Page<Persons> findAll(Pageable pageable);

        Page<Persons> findBySexAndEmailContains(String sexName, String emailName, Pageable pageable);

        Page<Persons> findBySex(String sexName, Pageable pageable);

        Page<Persons> findByEmailContains(String emailName, Pageable pageable);

        Persons findById(Long id);
    }
    ```

  -  Pageable

    啥也不说了，分页神器

---