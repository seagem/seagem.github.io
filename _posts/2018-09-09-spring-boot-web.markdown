---
layout:     post
title:      "基于spring boot搭建web项目一"
subtitle:   "主要是完成页面的访问"
date:       2017-03-15 21:20:00
author:     "gehaiyang"
header-img: "img/post-bg-design-patterns.jpg"
catalog: true
tags:
    - spring boot
---

> 先考虑最简单的实现，再斟酌使用设计模式。

#參考： https://www.cnblogs.com/sxdcgaq8080/p/7712874.html

其中需要注意的是：

* 1.添加pom.xml依赖：

        <!--web 支持-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
            
        <!--jsp页面使用jstl标签-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
        </dependency>
    
        <!--用于编译jsp-->
        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
            <scope>provided</scope>
        </dependency>
		
* 2.application.properties中添加：

```
spring.mvc.view.prefix = /WEB-INF/views/
spring.mvc.view.suffix = .jsp
```

* 3.还有一个很重要的地方,就是controller的设置，这里对应着@Controller
@RequestMapping(value = "/test")，而不是GetMapping，GetMapping是rest服务调用，而不是页面跳转：

```
package demoweb.demo;

import org.springframework.stereotype.Controller;
import org.springframework.stereotype.Repository;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@Controller
@RequestMapping(value = "/test")
public class MyController {

 /*   @GetMapping("/hello/{str}") //这里会影响到前台的欢迎界面
    public String Echo(@PathVariable String str) //如果想获取浏览器中输入的str，需要使用@PathVariable
    {
        //return "hi" + testtemplate.getForObject("http://localhost:18181/"+str, String.class);

        return "Hello " + str + " Welcome to my cloud.";
    }*/

    @RequestMapping(value = "/hello")
   public String Hello()
   {
       return "index";
   }

}
```

* 4.具体项目结构如下：

![1536464983477](img/book/pringbootweb.PNG)

* 5.访问路径：http://localhost:8080/test/hello

其中：第三点很重要。