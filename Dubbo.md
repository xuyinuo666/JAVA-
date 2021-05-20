# 分布式架构

1. 将服务提供者注册到服务中心

   

2. 将服务消费者订阅服务中心的提供者


服务提供者只需将服务接口暴露给消费者,再将接口加以实现其他功能,消费者调用接口就可以直接调用服务者实现的功能

```
<!-- https://mvnrepository.com/artifact/com.alibaba/dubbo -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>dubbo</artifactId>
    <version>2.6.5</version>
</dependency>


<!-- https://mvnrepository.com/artifact/org.apache.curator/curator-framework -->
<dependency>
    <groupId>org.apache.curator</groupId>
    <artifactId>curator-framework</artifactId>
    <version>5.1.0</version>
</dependency>

```

> 提供者

![image-20210112210034720](F:\文档\JAVA笔记\Typora\image-20210112210034720.png)

1. 导入公共接口以及bean的依赖

   ```xml
   <dependency>
           <groupId>org.example</groupId>
           <artifactId>Dubbo-interface</artifactId>
           <version>1.0-SNAPSHOT</version>
       </dependency>
   ```

2. 编写xml文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
   
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd">
       <!--1. 指定提供者名字-->
       <dubbo:application name="provider"></dubbo:application>
       <!--2. 指定注册地址 两种方式都行-->
       <!--    <dubbo:registry address="zookeeper://127.0.0.1:2181"></dubbo:registry>-->
       <dubbo:registry protocol="zookeeper" address="127.0.0.1:2181"></dubbo:registry>
       <!--3. 指定与消费者之间的通讯协议以及端口    -->
       <dubbo:protocol name="dubbo" port="20880"></dubbo:protocol>
       <!--4. 暴露哪些接口服务    -->
       <dubbo:service interface="com.dao.userservice" ref="userimpl"></dubbo:service>
       <bean name="userimpl" class="com.dao.impl.userserviceImpl"></bean>
   </beans>
   ```

   

> 消费者

<img src="F:\文档\JAVA笔记\Typora\image-20210112205848824.png" alt="image-20210112205848824"  />

1. 导入公共interface的依赖

2. ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
   		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd
   		http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd
   		http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">
       <context:component-scan base-package="service"></context:component-scan>
       <!--1. 指定服务者名字-->
       <dubbo:application name="consumer"></dubbo:application>
       <!--2. 指定注册地址 两种方式都行-->
       <!--    <dubbo:registry address="zookeeper://127.0.0.1:2181"></dubbo:registry>-->
       <dubbo:registry protocol="zookeeper" address="127.0.0.1:2181"></dubbo:registry>
       <!--3. 调用哪些接口服务    -->
       <dubbo:reference interface="com.dao.userservice" id="userimpl"></dubbo:reference>
   </beans>
   ```






# SpringBoot-Dubbo方式连接

1. 新建服务提供者和消费者两个springboot项目
2. 将两者共有的接口暴露在一个模块中

![image-20210113131512005](F:\文档\JAVA笔记\Typora\image-20210113131512005.png)

> 提供者

![image-20210113131546433](F:\文档\JAVA笔记\Typora\image-20210113131546433.png)

@Service表示将接口暴露出去

```java
@Service
@com.alibaba.dubbo.config.annotation.Service
public class userserviceimpl implements userservice {

    @Override
    public String userSelect() {
        System.out.println("--------------");
        return "hahaha";
    }
}

```

在将xml文件转换为properties

```properties
server.port=8081
dubbo.application.name=provider
dubbo.registry.address=127.0.0.1:2181
dubbo.registry.protocol=zookeeper
dubbo.protocol.name=dubbo
dubbo.protocol.port=20880
dubbo.registry.timeout=1000000
```



> 消费者

![image-20210113131722977](F:\文档\JAVA笔记\Typora\image-20210113131722977.png)

```java
@Controller
public class testctr {
    @Reference
    userservice userservice;
    @RequestMapping("user")
    @ResponseBody
    public String t1() {
        String s = userservice.userSelect();
        return s;
    }
}

```

@Reference :表示调用暴露的接口

```properties
server.port=8082
dubbo.application.name=consumer
dubbo.registry.address=127.0.0.1:2181
dubbo.registry.protocol=zookeeper


```



# 分包直连(不用注册中心zoopropertieskepper)

## 依赖:

```xml
 <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.2.9.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.2.9.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>dubbo</artifactId>
      <version>2.6.5</version>
    </dependency>
    <dependency>
      <groupId>com.interface</groupId>
      <artifactId>Dubbo-interface</artifactId>
      <version>1.0</version>
    </dependency>
  </dependencies>
```



# Dubbo-interface:

作用:

提供接口和实体类

![image-20200927154110964](C:\Users\徐一诺\AppData\Roaming\Typora\typora-user-images\image-20200927154110964.png)

User

```java
package com.pojo;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.io.Serializable;

@Data
@AllArgsConstructor
@NoArgsConstructor
//需要序列化
public class User implements Serializable {
    private Integer id;
    private String name;
}

```

UserDao

```java
package com.dao;

import com.pojo.User;

public interface UserDao {
    User q();
}

```

# Dubbo-provide

作用:

暴露接口的实现类.提供服务

![image-20200927154427592](C:\Users\徐一诺\AppData\Roaming\Typora\typora-user-images\image-20200927154427592.png)

userimpl

```java
package com.service;

import com.dao.UserDao;
import com.pojo.User;

public class userimpl implements UserDao {
    @Override
    public User q() {
        User xgw = new User(23, "xgw");
        return xgw;
    }
}

```

dubbo.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd">
<!--    服务名字:唯一性-->
    <dubbo:application name="provide"></dubbo:application>
<!--    访问服务协议的名称和端口号-->
    <dubbo:protocol name="dubbo" port="20880"></dubbo:protocol>
<!--
        暴露服务接口
        interfaca:暴露接口的全限定名
        ref:接口实现类
-->
    <dubbo:service interface="com.dao.UserDao" ref="ser" registry="N/A"></dubbo:service>
    <bean id="ser" class="com.service.userimpl"></bean>
</beans>
```

web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
    <!--    注册监听器-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:dubbo.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
</web-app>

```

# Dubbo-custom

相当于controller层

![image-20200927155319813](C:\Users\徐一诺\AppData\Roaming\Typora\typora-user-images\image-20200927155319813.png)

he

```java
package com.cont;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class he {
    @RequestMapping("/hehe")
    public String h() {
        return "hahaha";
    }
}

```

applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">
<!--    扫描包-->
<context:component-scan base-package="com.cont"></context:component-scan>
<!--    注解驱动-->
    <mvc:annotation-driven></mvc:annotation-driven>
<!--    视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/"></property>
        <property name="suffix" value=".html"></property>
    </bean>
</beans>
```

Dubbo.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd">
<!--    服务名称：唯一性-->
<dubbo:application name="custom"></dubbo:application>
<!--    接收暴露的接口-->
    <dubbo:reference id="ser"
                     interface="com.dao.UserDao"
                     url="dubbo://localhost:20880"
                     registry="N/A"></dubbo:reference>
</beans>
```

web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
<!--  配置中央调度器，将Dubbo.xml加入到其中-->
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:Dubbo.xml,classpath:applicationContext.xml</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>

```

# 使用注册中心(zookeeper)

将以上的registty属性单独提取出来

```java
<dubbo:registry address="zookeeper://localhost:2181"></dubbo:registry>
```

