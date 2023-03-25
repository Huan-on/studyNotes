# 一、搭建项目环境

## 1、开发环境

- IDE：idea 2020.2.4
- 构建工具：maven 3.6.3
- spring版本：spring 5.3.1
- MyBatis版本：MyBatis 3.5.7
- MySQL版本：MySQL 5.7

## 2、创建maven工程

### a>添加web模块

### b>打包方式：war

```xml
<packaging>war</packaging>
```

### c>配置pom，引入依赖

> spring
>
> springMVC
>
> MyBatis
>
> 数据库连接池和驱动包
>
> 其他：jstl(jsp常用标签库，使用Thymeleaf可以不用管)，servlet-api，junit

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.ssm</groupId>
    <artifactId>SSM_CRUD</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <dependencies>

        <!-- ============== SpringMVC =================-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.3.1</version>
        </dependency>

        <!-- ============== spring-jdbc =================-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.3.1</version>
        </dependency>

        <!-- ============ spring面向切面编程 ============== -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>5.3.1</version>
        </dependency>

        <!-- ================= MyBatis ================== -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.7</version>
        </dependency>

        <!-- ========= MyBatis整合Spring的适配包 ========== -->
        <dependency>
            <!--mybatis版本在3.4左右整合包的版本在1.3，3.5在2.0左右-->
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.7</version>
        </dependency>

        <!-- ==================== 数据库 ================= -->

        <!-- =============== druid数据库连接池 =============== -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.1</version>
        </dependency>

        <!-- ================== mysql驱动 =================== -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.41</version>
        </dependency>

        <!-- ==================== 其他jar ================= -->

        <!-- ================ Servlet-API ================= -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- ========== Spring5和Thymeleaf整合包 ============ -->
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring5</artifactId>
            <version>3.1.0.M2</version>
        </dependency>


        <!-- =============== junit单元测试 ================== -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>


        <!-- MBG，MyBatis逆向工程使用 -->
        <dependency>
            <groupId>org.mybatis.generator</groupId>
            <artifactId>mybatis-generator-core</artifactId>
            <version>1.3.5</version>
        </dependency>


    </dependencies>
</project>
```

## 3、引入Bootstrap

> 前端框架，视图界面，简化开发，美化界面

### a> 基本流程：

1. 在`webapp`下创建`static`目录，存放静态资源
2. 在`webapp`下创建`index`首页页面，引入相关的静态资源

### b> 下载地址：

### [起步 · Bootstrap v3 中文文档 | Bootstrap 中文网 (bootcss.com)](https://v3.bootcss.com/getting-started/#download)

### c> 使用：

#### 1、引入样式文件、jQuery文件和js文件

```html
 <!--引入样式-->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css"
          integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu"
          crossorigin="anonymous">

    <!--引入jQuery-->
    <script type="text/javascript" src="static/js/jquery-3.4.1.min.js"></script>
    <!--引入js文件-->
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"
            integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd"
            crossorigin="anonymous"></script>
```

#### 2、基本模板

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css" integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">

    <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!--[if lt IE 9]>
      <script src="https://cdn.jsdelivr.cn/npm/html5shiv@3.7.3/dist/html5shiv.min.js"></script>
      <script src="https://cdn.jsdelivr.cn/npm/respond.js@1.4.2/dest/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>你好，世界！</h1>

    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="https://cdn.jsdelivr.cn/npm/jquery@1.12.4/dist/jquery.min.js" integrity="sha384-nvAa0+6Qg9clwYCGGPpDQLVpLNn0fRaROjHqs13t4Ggj3Ez50XnGQqc/r8MhnRDZ" crossorigin="anonymous"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js" integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous"></script>
  </body>
</html>
```

## 4、编写整合的关键配置文件

### a> 编写web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!-- 1、启动Spring的容器 -->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <!--配置Spring配置文件的路径-->
        <param-value>classpath:applicationContext.xml</param-value>
    </context-param>

    <!--配置监听器-->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <!-- ================================================================================== -->

    <!-- 2、SpringMVC的前端控制器，拦截所有请求 -->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>

        <!--
        指定SpringMVC配置文件的位置
        不指定需要在与web.xml同级的目录下有一个配置文件
        名字为 当前servlet-name + (-servlet)
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value></param-value>
        </init-param>
        -->

        <!--初始化等级-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!-- =============================================================================== -->

    <!-- 3、配置字符编码过滤器，一定要在所有过滤器之前 -->
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>

        <!--初始化配置-->
        <init-param>
            <!--指定encoding的字符集编码为utf-8-->
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>

        <init-param>
            <!--设置请求编码为encoding-->
            <param-name>forceRequestEncoding</param-name>
            <param-value>true</param-value>
        </init-param>

        <init-param>
            <!--设置响应编码为encoding-->
            <param-name>forceResponseEncoding</param-name>
            <param-value>true</param-value>
        </init-param>

    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!-- =============================================================================== -->

    <!-- 4、使用Rest风格 -->
    <filter>
        <!-- 将页面普通的post请求转换为指定的 put 请求或 delete 请求 -->
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>


</web-app>
```

### b> 编写springMVC的配置文件

> springMVC的配置文件是dispatcherServlet-servlet.xml，放在WEB-INF下

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/mvc
                           http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- SpringMVC的配置文件，配置网站跳转逻辑的控制 -->

    <!-- 1、扫描所有的业务逻辑的组件 -->
    <context:component-scan base-package="com.hu" use-default-filters="false">
        <!-- use-default-filters="false"表示禁用默认的过滤规则 -->

        <!-- 使其只扫描控制器 -->
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>

    </context:component-scan>

    <!-- =============================================================================================== -->

    <!-- 2、配置视图解析器，方便页面返回 -->
    <bean id="viewResolver" class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
        <property name="order" value="1"/>
        <property name="characterEncoding" value="UTF-8"/>
        <property name="templateEngine">
            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
                <property name="templateResolver">
                    <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">

                        <!-- 视图前缀 -->
                        <property name="prefix" value="/WEB-INF/templates/"/>

                        <!-- 视图后缀 -->
                        <property name="suffix" value=".html"/>
                        <property name="templateMode" value="HTML5"/>
                        <property name="characterEncoding" value="UTF-8" />
                    </bean>
                </property>
            </bean>
        </property>
    </bean>

    <!-- =============================================================================================== -->

    <!-- 3、两个标准配置 -->

    <!-- a> 将SpringMVC不能处理的请求交给TomCat -->
    <mvc:default-servlet-handler/>

    <!-- b> 开启mvc注解驱动 -->
    <mvc:annotation-driven/>

</beans>
```

### c>编写spring的配置文件

> jdbc配置文件是dbconfig.properties，放在resources下

- 编写jdbc配置文件

```properties
jdbc.url=jdbc:mysql://localhost:3306/ssm_crud
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.username=root
jdbc.password=hu
```

> 前面加 jdbc. 是为了防止数据混乱而加上的定位符

> Spring的配置文件 applicationContext.xml，放在resources下

- 编写spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop
                           http://www.springframework.org/schema/aop/spring-aop.xsd
                           http://www.springframework.org/schema/tx
                           http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!--Spring的配置文件,配置业务逻辑类-->

    <!-- 1、扫描业务逻辑的组件 -->
    <context:component-scan base-package="com.hu">

        <!-- 在Spring的配置文件中使Spring的容器不扫描控制器组件，也就是SpringMVC扫描的组件 -->
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>

    </context:component-scan>

    <!-- =============================================================================================== -->

    <!-- 2、配置druid数据源 -->

    <!-- 引入外部properties文件 -->
    <context:property-placeholder location="classpath:dbconfig.properties"></context:property-placeholder>

    <bean id="DruidDataSource" class="com.alibaba.druid.pool.DruidDataSource">

        <!-- 配置JDBC连接数据库的基本属性 -->

        <!-- 驱动名字 -->
        <property name="driverClassName" value="${jdbc.driverClassName}"></property>

        <!-- 路径 -->
        <property name="url" value="${jdbc.url}"></property>

        <!-- 用户名 -->
        <property name="username" value="${jdbc.username}"></property>

        <!-- 密码 -->
        <property name="password" value="${jdbc.password}"></property>

    </bean>

    <!-- =============================================================================================== -->

    <!-- 3、配置和MyBatis的整合 -->
    <bean id="sqlSessionFactoryBean" class="org.mybatis.spring.SqlSessionFactoryBean">

        <!-- 指定MyBatis全局配置文件的位置 -->
        <property name="configLocation" value="classpath:mybatis-config.xml"></property>

        <!-- 指定数据源 -->
        <property name="dataSource" ref="DruidDataSource"></property>

        <!-- 指定MyBatis的mapper文件的位置 -->
        <property name="mapperLocations" value="classpath:mapper/*.xml"></property>

    </bean>

    <!-- 配置扫描器，将MyBatis接口的实现加入到ioc容器中 -->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">

        <!--扫描所有dao接口的实现，加入到ioc容器中-->
        <!-- 扫描dao包下的所有mapper接口的实现，加入到ioc容器中 -->
        <property name="basePackage" value="com.hu.crud.dao"></property>
    </bean>

    <!-- =============================================================================================== -->

    <!-- 4、配置事务控制 -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">

        <!-- 控制住数据源 -->
        <property name="dataSource" ref="DruidDataSource"></property>

    </bean>

    <!-- 开启基于注解的事务，使用xml配置形式的事务（必要主要的都是使用配置式） -->
    <aop:config>

        <!-- 切入点表达式 -->
        <aop:pointcut id="txPoint" expression="execution(* com.hu.crud.service..*(..))"/>

        <!-- 配置事务增强 -->
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPoint"/>

    </aop:config>

    <!-- 配置事务增强，事务如何切入 -->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <!-- transaction-manager表示使用什么事务管理器控制事务，值为事务管理器的bean的id-->

        <tx:attributes>
            <!-- *表示切入的所有方法都是事务方法 -->
            <tx:method name="*"/>

            <!-- 表示以get开始的所有方法 -->
            <tx:method name="get*" read-only="true"/>
        </tx:attributes>
        
    </tx:advice>

</beans>
```

> 切入点表达式
>         (这里还有一个访问权限修饰符，可以不写) (返回类型所有)
>         com.crud.service..*(..表示所有类，即使这个包下有子包也行，*表示所有方法)
>         (..)(括号里两个点表示方法中参数任意多)

> transaction-manager="transactionManager"意思为用id为transactionManager的事务管理器来控制事务
>         控制事务的细节写在aop，表示切什么方法，方法切入之后又该怎么办，就在tx中写

> tx:attributes表示事务增强的配置，切入点表达式切入之后怎么办就看这里的配置

### d>编写mybatis的配置文件

#### 1、使用mybatis的逆向工程生成dao的各种文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>

    <context id="DB2Tables" targetRuntime="MyBatis3">

        <!-- 取消生成文件时的自动生成注释 -->
        <commentGenerator>
            <property name="suppressDate" value="true" />
        </commentGenerator>

        <!-- 配置数据库连接信息 -->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/ssm_crud"
                        userId="root"
                        password="hu">
        </jdbcConnection>

        <javaTypeResolver >
            <property name="forceBigDecimals" value="false" />
        </javaTypeResolver>

        <!-- 指定javaBean生成的位置 -->
        <javaModelGenerator targetPackage="com.hu.crud.bean"
                            targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true" />
            <property name="trimStrings" value="true" />
        </javaModelGenerator>

        <!-- 指定sql映射文件生成的位置 -->
        <sqlMapGenerator targetPackage="mapper"
                         targetProject=".\src\main\resources">
            <property name="enableSubPackages" value="true" />
        </sqlMapGenerator>

        <!-- 指定dao接口生成的位置，mapper接口 -->
        <javaClientGenerator type="XMLMAPPER"
                             targetPackage="com.hu.crud.dao"
                             targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true" />
        </javaClientGenerator>

        <!-- 指定每个表的生成策略 -->
        <table tableName="tbl_emp" domainObjectName="Employee"></table>
        <table tableName="tbl_dept" domainObjectName="Department"></table>

    </context>
</generatorConfiguration>
```

#### 2、使用java代码基于xml配置文件的方式，使用逆向工程

> 使用前，需要先在pom文件中引入MBG的依赖

```java
    public static void main(String[] args) throws Exception{
        List<String> warnings = new ArrayList<String>();
        boolean overwrite = true;
        File configFile = new File("mbg.xml");
        ConfigurationParser cp = new ConfigurationParser(warnings);
        Configuration config = cp.parseConfiguration(configFile);
        DefaultShellCallback callback = new DefaultShellCallback(overwrite);
        MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, callback, warnings);
        myBatisGenerator.generate(null);
    }
```

#### 3、mybatis配置文件

> 这里写的配置信息少的原因是，其他配置信息已经在spring配置文件中写了，这里不用多写，所以就写的比较少

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <!-- 配置驼峰命名规则 -->
    <settings>
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>

    <!-- 配置类型别名 -->
    <typeAliases>
        <package name="com.hu.crud.bean"/>
    </typeAliases>

</configuration>
```

#### 4、完善动态生成的文件中不足的部分

##### a>在持久层补充信息

```java
 //希望查询员工的同时部门信息也是查询好的
    private Department department;

    public Department getDepartment() {
        return department;
    }

    public void setDepartment(Department department) {
        this.department = department;
    }
```

##### b>接口中创建方法

```java
List<Employee> selectByExampleWithDept(EmployeeExample example);
Employee selectByPrimaryKeyWithDept(Integer empId);
```

##### c>映射文件中编写SQL

```xml
<resultMap id="WithDeptResultMap" type="com.crud.bean.Employee">
    <id column="emp_id" property="empId" jdbcType="INTEGER" />
    <result column="emp_name" property="empName" jdbcType="VARCHAR" />
    <result column="gender" property="gender" jdbcType="CHAR" />
    <result column="email" property="email" jdbcType="VARCHAR" />
    <result column="d_id" property="dId" jdbcType="INTEGER" />
<!--    指定联合查询出的部门字段的封装-->
    <association property="department" javaType="com.crud.bean.Department">
      <id column="dept_id" property="deptId"/>
      <result column="dept_name" property="deptName"/>
    </association>
  </resultMap>
===================================分割线====================================
<!--补充编写外部能引入的sql-->
<sql id="WithDept_Column_List">
    e.emp_id, e.emp_name, e.gender, e.email, e.d_id,d.dept_id,d.dept_name
</sql>
===================================分割线====================================
<!--
    List<Employee> selectByExampleWithDept(EmployeeExample example);
    Employee selectByPrimaryKeyWithDept(Integer empId);
-->
<!--查询员工同时带部门信息-->
<select id="selectByExampleWithDept" resultType="WithDeptResultMap">
      select
      <if test="distinct" >
        distinct
      </if>
      <include refid="WithDept_Column_List" />
      from tbl_emp e left join tbl_dept d on e.`d_id`=d.`dept_id`
      <if test="_parameter != null" >
        <include refid="Example_Where_Clause" />
      </if>
      <if test="orderByClause != null" >
        order by ${orderByClause}
      </if>
</select>
<select id="selectByExampleWithDept" resultMap="WithDeptResultMap">
    select
    <include refid="WithDept_Column_List" />
    from tbl_emp e left join tbl_dept d on e.`d_id`=d.`dept_id`
    where emp_id = #{empId,jdbcType=INTEGER}
</select>
===================================分割线====================================
<!--下面是原有的sql，上面的sql就是在这两个原有的sql上改造而成-->
<!--查询员工不带部门信息的-->
<select id="selectByExample" resultMap="BaseResultMap" parameterType="com.crud.bean.EmployeeExample" >
    select
    <if test="distinct" >
      distinct
    </if>
    <include refid="Base_Column_List" />
    from tbl_emp
    <if test="_parameter != null" >
      <include refid="Example_Where_Clause" />
    </if>
    <if test="orderByClause != null" >
      order by ${orderByClause}
    </if>
</select>
<select id="selectByPrimaryKey" resultMap="BaseResultMap" parameterType="java.lang.Integer" >
    select 
    <include refid="Base_Column_List" />
    from tbl_emp
    where emp_id = #{empId,jdbcType=INTEGER}
</select>
```

### 5、测试mapper

失败，查问题查了两天，放弃了
