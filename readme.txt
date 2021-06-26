Day1    30-May-2021
====================
JDK 8
=====
https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html#license-lightbox


STS Download
============
https://download.springsource.com/release/STS4/4.8.1.RELEASE/dist/e4.17/spring-tool-suite-4-4.8.1.RELEASE-e4.17.0-win32.win32.x86_64.self-extracting.jar

Spring Distrubution 5.0
=======================
https://repo.spring.io/release/org/springframework/spring/5.0.2.RELEASE/


Enterprise Application
=======================


Enterprise :(Business Organization) : make the money by providing services
===================================
Banks  :withdraw,deposit,fundTransfer,loan
LICS   :Insurance policy
Transports:book,cancel ticket
Hotels  :order food,book table
Hospitals:appointment
School   :admission,teaching,result
College  :admission,teaching,result


Layer :Logical separation of code
Tier  :Physical separation of code

Applications development platforms

Java
.Net
PHP
Node JS
Python



Database Operation
=====================
C=Create
R=Retrieve
U=Update
D=Delete


fundTransfer:(int source,int destination ,int amount)
             
             1.retireve source and validate amount < avialable
             2.retirve destination and validate 
             3.debit source -update
             4.credit destination -update
             5.commit


Presentation Layer :Code written to provide the input screen and resposne to the user
Service Layer      :Logical implementation of business rules
Data Access Layer  :Code written to access the data from Data source
Data Layer         :It is source for Data   


Three data sources
==================
Collection
MySQL
MongoDB


Data Access Layer : Hibernate
Service Layer     : EJB
Presentation Layer :Struts

Spring -One stop shop application
        It takes care of all layers of enterprise application
         


Banking
=======

Develop a Banking application

Write a Java application to perform standard CRUD operations on Customer and Account Domain Objects using Map as DataSource.

    
     
Customer
        customerId
        name
        pan
        mobile         
        address
        dob
        

Account:
        accno
	name 
        balance
        doc
        type

        
         
CustomerMainApp
              CustomerService
                           CustomerDao
                                        MapCustomerServiceImpl
                                                                CustomerMap
               


                                                    



Day2  :5-Jun-2021
======
IOC -Inversion of Control -Don't call me I  will call you
DI  -It is a mechanism of initializing the dependencies 

      1.setter injection      :
      2.constructor injection :     
      
      
We have to explain Spring Container about the spring beans(Java Classes) via XML file or annotations


Step 1: create a Java Project and add spring jar files to class path


Step 2: create a spring container (controls life-cyles of bean)

1.Core Container -BeanFactory based

2.Advanced Container -ApplicationContext

3.Web Container -WebApplicationContext



                             BeanFactory (I)
                                 |
                                 |XMLBeanFactory (C) :Lazy Initialization
                                 |
                            ApplicationContext(I)    :Eager Initialization
                                 |
ClasspatApplicationXMLContext (C)|    AnnotationConfigApplicationContext (C)
                                 |
                                 |
                           ServletWebApplicationContext(I)           


//core container


Lazy Initiialization

XmlBeanFactory c=new XmlBeanFactory(new ClassPathResource("beans.xml"));
         
         
//advanced container
Eager Initialization     
ClassPathXmlApplicationContext c=new ClassPathXmlApplicationContext("beans.xml");
	    

<beans default-lazy-init=false|true/>
	    
<bean lazy-init=false|true/>


        
1.get bean by type if only one bean of specific type
  
  CustomerMainApp cma=c.getBean(CustomerMainApp.class);
         
2.get bean by id when multiple beans of same type

CustomerMainApp cma=(CustomerMainApp)c.getBean("customerMainApp");
        




DI :Mechamsim of initialzing the depencencies

  setter   ->    <property name="cs" ref="customerService">

  constructor -> <constructor-arg   name="cs" ref="customerService">
                          
                                                    
Spring Bean Life Cycle
==========================
1.Instantiation
2.Dependency Injection(setter/constructor)
3.Initialization   (init-method)
4.Service
5.Destruction      (destroy-method)

Spring Bean Scope : singleton|prototype|request|session



Spring Bean Scope
==================
<bean  scope="singleton"/>

singleton -Stateless Application
prototype -Stateful Application

request  -web
session  -web


Auto-wiring
============
Wiring - It's a mechanisam of associating the beans with each other
Auto-wiring -It's a mechanisam of delegating the responsisbilty of associating the beans with each other to the spring container

auto-wire="no|byType|byName|constructor"


Annotation Based configuration
===============================
                                           @Component

              @Controller                  @Service                   @Reposiotry



@Configuration   => <beans.xml>
@PostConstruct   => init-method
@PreDestroy      =>destroy-method
@Autowire        =>autwire (byType)
@Qualifier       => byName 
   can be applied to constructor/setter/intreface



<bean    init-method=""   destroy-method=""/>    @PostConstruct    @PreDestroy

<bean    autowire=""/>    

@Autowire  =>default byType


Note :To enable annotation based bean registration put below tag

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd">

<context:component-scan   package="com"/>

</beans>


Day3
====
6-Jun-2021
==========

1.Tomcat Download :https://apachemirror.wuchna.com/tomcat/tomcat-9/v9.0.46/bin/apache-tomcat-9.0.46.zip

2.Add Spring jar file to Tomcat lib directory

3.Create a dynamic web project with web.xml

4.Register a DispatcherServlet in web.xml as below

<servlet>
<servlet-name>spring</servlet-name>
<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
<load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
<servlet-name>spring</servlet-name>
<url-pattern>/spring/*</url-pattern>
</servlet-mapping>

5.By default DispatcherServlet will load the file with name (DispatcherServletName-serlvet.xml) 
  So create a file spring-servlet.xml

6.Create a Root Web application Context
   by default it will search applicationContext.xml
  

<listener>
<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>


<context-param>
<param-name>contextConfigLocation</param-name>
<param-value>/WEB-INF/applicationContext.xml</param-value>
</context-param>

1.RootWebApplication created first









Spring Web MVC
==============
Develop a Spring Web MVC application to build RESTful Web API to perform CRUD Operations


URI                      METHOD                           OPERATION
============================================================== 

/customers               GET                               GET ALL CUSTOMERS
/customers/1             GET                               GET CUSTOMER BY ID
/customers/1             PUT                               UPDATE CUSTOMER BY ID
/customers/1             DELETE                            DELETE CUSTOMER BY ID
/customers               POST                              ADD CUSTOMER 


HTTP status codes
======================
200    :   OK
201    :   Created
500    :   INTERNAL SERVER ERROR
404    :   NOT FOUND
204    :   NO CONTENT
401    :   INVALID CREDENTAILS
403    :   FORBIDDEN
405    :   METHOD NOT ALLOWED


MVC (                 Model                   View                   Controller)
================================================================================
JSP Model-1          Java Bean                JSP                     JSP
JSP Model-2          Java Bean                JSP                     Servlet    (Struts1.x,JSF 1.x,2.x ,Spring Web MVC)
JSP Model-3          Java Bean                JSP                     Filter     (Struts2.x)
JSP Model-4          Java Bean                JSP                     Tag Handler


Spring Web MVC follows MVC2 /JSP Model2
==============================================   

 url      method      mapping                                                         new style                                         =========================================================================================================



/hello   GET         @RequestMapping(value="/hello",method=RequestMethod.GET)        @GetMapping("/hello")
/hello   POST        @RequestMapping(value="/hello",method=RequestMethod.POST)       @PostMapping("/hello")
/hello   DELETE      @RequestMapping(value="/hello",method=RequestMethod.DELETE)     @DeleteMapping("/hello")
/hello   PUT         @RequestMapping(value="/hello",method=RequestMethod.PUT)        @PutMapping("/hello")
/hello   PATCH       @RequestMapping(value="/hello",method=RequestMethod.PATCH)      @PatchMapping("/hello")





@RestController   =>  @Controller +  @ResponseBody 



<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven/>
</beans>
 



Java To JSON    : @ResponseBody

JSON to Java    : @RequestBody
================================


@ResponseBody  => Server to Client => Java Object to JSON or XML  => Accept       = application/json 

@RequestBody  => Client to Server =>  JSON or XML Java Object to  => Content-Type = application/json


@ResponseBody  => Server to Client => Java Object to JSON or XML  => Accept       = application/json 

@RequestBody  => Client to Server =>  JSON or XML Java Object to  => Content-Type = application/json


For Message Conversion :

Step 1:  add below tag in spring-config file
=======
<mvc:annotation-driven/>

Step 2:  Add below jars in class path
=======
jackson-core-2.9.8
jackson-annotations-2.9.8.jar
jackson-databind-2.9.8.jar



12-June-2021
=============
CustomerRestController
              CustomerService
                           CustomerDao
                                        MapCustomerServiceImpl
                                                                CustomerMap



CustomerSpringController
              CustomerService
                           CustomerDao
                                        MySQLCustomerDaoImpl
                                                                  
                                                     JdbcTemplate
                                                              DataSource
                                                                   driverClassName
                                                                   username
                                                                   password
                                                                   url



JdbcTemplate
===============
 
GET                   :  query()

UPDATE,INSERT,DELETE  :  update()



SQL Script
============
create database company;
use company;
create table customers(
  customerId int primary key,
  name text,
  pan text,
  mobile text,
  address text,
  dob date
  );

insert into customers values(1111,'Sachin patil','skxnd9834f','8737726736','Pune','1982-01-01');
insert into customers values(2222,'Sumit patil','abcnd9834f','6637726736','Mumbai','1985-01-01');
insert into customers values(3333,'Sunil patil','abcnd9834f','6637726736','Bangalore','1989-01-01');


select * from customers;


Day5      13-June-2021
========================
What is Spring Boot?
=====================
1.Spring Boot provides a good platform for Java developers to develop a stand-alone and 
production-grade spring application that you can just run.
2.You can get started with minimum configurations without the need for an entire Spring configuration setup.

Spring Boot offers the following advantages to its developers -
=================================================================
1.Easy to understand and develop spring applications
2.Increases productivity
3.Reduces the development time

Goals
======
1.To avoid complex XML configuration in Spring
2.To develop a production ready Spring applications in an easier way
3.To reduce the development time and run the application independently
4.Offer an easier way of getting started with the application

Why Spring Boot?
================

You can choose Spring Boot because of the features and benefits it offers as given here -

1.It provides a flexible way to configure Java Beans, XML configurations, and Database Transactions.

2.It provides a powerful batch processing and manages REST endpoints.

3.In Spring Boot, everything is auto configured; no manual configurations are needed.

4.It offers annotation-based spring application

5.Eases dependency management (POM)

6.It includes Embedded Servlet Container


How does it work?
=>Spring Boot automatically configures your application based on the dependencies you have added to the project by using
 @EnableAutoConfiguration annotation. 
 
 For example, if MySQL database is on your classpath, but you have not configured any database connection, 
 then Spring Boot auto-configures an in-memory database.

=>The entry point of the spring boot application is the class contains @SpringBootApplication annotation 
   and the main method.

Spring Boot automatically scans all the components included in the project by using @ComponentScan annotation.



Spring Boot Starters
=====================
=>Handling dependency management is a difficult task for big projects. 
=>Spring Boot resolves this problem by providing a set of dependencies for developers convenience.
=>For example, if you want to use Spring and JPA for database access, 
    it is sufficient if you include spring-boot-starter-data-jpa dependency in your project.

Note that all Spring Boot starters follow the same naming pattern spring-boot-starter- *, 
  where * indicates that it is a type of the application.

Examples
Look at the following Spring Boot starters explained below for a better understanding -

1.Spring Boot Starter Actuator dependency is used to monitor and manage your application. Its code is shown below -

<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>


2.Spring Boot Starter Security dependency is used for Spring Security. Its code is shown below -

<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-security</artifactId>
</dependency>


3.Spring Boot Starter web dependency is used to write a Rest Endpoints. Its code is shown below -

<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
</dependency>
      
4.Spring Boot Starter Test dependency is used for writing Test cases. Its code is shown below -

<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-test</artifactId>
</dependency>      
      
      
Auto Configuration
====================


https://start.spring.io/




Spring Web WEB
==================
Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container.

Spring Boot DevTools DEVELOPER TOOLS
=====================================
Provides fast application restarts, LiveReload, and configurations for enhanced development experience.

Spring Boot Actuator OPS
========================
Supports built in (or custom) endpoints that let you monitor and manage your application - 
such as application health, metrics, sessions, etc.

Spring Security SECURITY
=========================
Highly customizable authentication and access-control framework for Spring applications.

Spring Data JPA SQL
===================
Persist data in SQL stores with Java Persistence API using Spring Data and Hibernate.

CRUDRepository                CRUDRepository
     |                              |
PagingAndSortingRespistory    MongoRepository
     |
JPAReposiotry




Spring Data MongoDB NOSQL
=========================
Store data in flexible, JSON-like documents, meaning fields can vary from document to document and data structure can be changed over time.


Spring Security
================
Default username :user
Password         :generated on console


To customize it
================

add below properties in application.properties
==============================================

spring.security.user.name=pradeep
spring.security.user.password==pradeep


https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html




19-June-2021
=============
1.Spring Security
2.Hibernate Relations
3.Spring MongoRepository  (Mongo DB download :https://fastdl.mongodb.org/windows/mongodb-windows-x86_64-4.4.6-signed.msi)









Spring Security
================
Default username :user
Password         :generated on console


To customize it
================

add below properties in application.properties
==============================================

spring.security.user.name=pradeep
spring.security.user.password=pradeep



https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html




JAAS
====
Java Authentication and Authorization Service

Authentication
================
1.BASIC  (Before Spring Boot 2.x)
2.DIGEST
3.FORM BASED (From Spring Boot 2.x)  : Endpoints login,logout



Authorization (role)
====================



To Customize default JAAS


We should write a configuration class by extending WebSecurityConfigureerAdapter and override configure methods.




@Configuration
public class BankConfig  extends WebSecurityConfigurerAdapter{

	@Autowired
	private DataSource dataSource;
	
	
	public BankConfig() {
	System.out.println("==========BankConfig created=================");
	}
	
	
	@Override
	protected void configure(AuthenticationManagerBuilder auth) throws Exception {
		System.out.println("==========BankConfig created  AuthManagerBuilder=================");
		//super.configure(auth);
	
		
		/*
		 * auth.inMemoryAuthentication()
		 * .withUser("RAM").password("{noop}RAM").roles("ADMIN").and()
		 * .withUser("RAHIM").password("{noop}RAHIM").roles("STUDENT").and()
		 * .withUser("DAVID").password("{noop}DAVID").roles("TEACHER");
		 * 
		 * 
		 */
		
		auth.jdbcAuthentication()
		    .passwordEncoder(new BCryptPasswordEncoder())
		    .dataSource(dataSource);
		
	}
	
	
	@Override
	protected void configure(HttpSecurity http) throws Exception {
		System.out.println("==========BankConfig created  HttpSecurity=================");
		//super.configure(http);  Default is Form Based
		
		
		http.authorizeRequests()
		.antMatchers("/rest/*").permitAll()
		.antMatchers("/rest/*").denyAll()
		.antMatchers("/spring/*").hasRole("ADMIN")
		.antMatchers("/spring/welcome","/spring/today").hasRole("STUDENT")
		.antMatchers("/spring/hello","/spring/greet").hasAnyRole("ADMIN","TEACHER")
	
		
		    .anyRequest()
		    .authenticated()
		    .and()
		    .formLogin();//  Form Based
		    //.httpBasic();// Basic Auth
		
		
		
	}
	
	
	
}


MongoDB details
=================

https://www.tutorialspoint.com/mongodb/mongodb_overview.htm

Mongo DB                   RDBMS
==================================          
Database                  Database

Collection                Table        Class                    

Document                  Row          Object

Id                        Primary Key

Embeded documents         Joins



To start Mongo DB Server
========================



Create a folder in c drive :  c:\data\db

C:\Program Files\MongoDB\Server\3.4\bin>mongod   <enter>


To start Mongo DB Client
========================

C:\Program Files\MongoDB\Server\3.4\bin>mongo <enter>





20-June-2021
=============
1.Spring AOP
2.Spring Tx Management
3.Spring Boot Google Oauth security 
4.Hibernate Relations



Spring 

Core
Context
Web
Dao
AOP



@Transactional  =>Class / Method








AOP -Aspect Oriented Programming
=================================


Spring AOP
==========
AOP  -Aspect Oriented Programming
=====

Concern :Piece Of Code

                           Functional          Nonfunctional

Business Logic  =          Core Concern    +   Cross Cutting Concern

                            withdraw                  security
                            deposit                   logging 
                            transfer                  scalabilty tx mgmt


AOP is used to separate CCC from CC and attach CCC dynamically in a CC.

Can We Separate CCC from CC using OOP? Yes but it is a static approach.
 



Target  :It is a piece of code that implements Core Concern


Advice  :It is a piece of code that implements Cross Cutting  Concern
                what + when

               before,
               after
               after return
               after throwing
               around

JoinPoint  :
                 It is a well defined point in Core Concern where u want to execute CCC
                 Spring supports only method call as a join point

Point Cut  :
                 It is a set of one or more join points
                 

Aspect : advice +point cut  ->what +when+where


Weaving :Mechanism of attaching CCC to CC



@Component
@Aspect
public class Logging {
	
	
	
	public Logging() {
	System.out.println("Logging Advice created.....");
	}
	
	/**
	 * Following is the definition for a pointcut to select * all the methods
	 * available. So advice will be called * for all the methods.
	 */
	@Pointcut("execution(* com.pradeep.bank.service.CustomerService.*(..))")
	private void selectAll() {
	}

	@Pointcut("execution(* com.pradeep.bank.service.CustomerService.findCustomer(..))")
	private void select() {
	}

	
	
	/**
	 * * This is the method which I would like to execute * before a selected
	 * method execution.
	 */
	@Before("selectAll()")
	public void beforeAdvice() {
		System.err.println("Going to setup customer profile.");
	}

	/**
	 * * This is the method which I would like to execute * after a selected
	 * method execution.
	 */
	@After("selectAll()")
	public void afterAdvice() {
		System.err.println("Customer profile has been setup.");
	}

	
	
	/**
	 * * This is the method which I would like to execute * when any method
	 * returns.
	 */
    @AfterReturning(pointcut = "selectAll()", returning = "retVal")
	public void afterReturningAdvice(Object retVal) {
		System.err.println("Customer afterReturning:" + retVal);
	}

    
	/**
	 * * This is the method which I would like to execute * if there is an
	 * exception raised by any method.
	 */
	@AfterThrowing(pointcut = "selectAll()", throwing = "ex")
	public void AfterThrowingAdvice(Exception ex) {
		System.err.println("Customer There has been an exception: " + ex);
	}
	

    @Around("select()")
	public Object aroundAdvice(ProceedingJoinPoint joinPoint)throws Throwable{
	
    	Object returnVal=null;
    	System.err.println("In around Advice .....");
    	
    	
    	try {
    		System.err.println("Before Proceed :");
        	returnVal=joinPoint.proceed();
        	System.err.println("After  Proceed :"+returnVal);
        	 Customer value=(Customer)returnVal;
        	
        	 value.setName(value.getName().toUpperCase());   
		    
    	
    	} catch (Throwable e) {
             e.printStackTrace();
         System.out.println("around Advice  exception wrapped.....");
             
    		}
    	System.out.println("around Advice  over.....");
          return returnVal;
    }
    }




Spring Boot Google Oauth Sign In
===================================
A OAuth2 Server, sometimes also referred to as an OAuth 2.0 Server, OAuth Server, Authorization Server, is a software system that implements network protocol flows that allow a client software application to act on behalf of a user.

Cross site request forgery (CSRF), also known as XSRF, Sea Surf or Session Riding, is an attack vector that tricks a web browser into executing an unwanted action in an application to which a user is logged in. A successful CSRF attack can be devastating for both the business and user.

Cross-site request forgery, also known as one-click attack or session riding and abbreviated as CSRF or XSRF, is a type of malicious exploit of a website where unauthorized commands are submitted from a user that the web application trusts.



https://www.tutorialspoint.com/spring_boot/spring_boot_google_oauth2_sign_in.htm




Hiberntae relationship
======================

@Entity
@Table(name="pc_customer")
public class Customer{

@Id
@Column(name="customerId")
private int id;
private String name;

}


1.One  to One    => Employee => EmployeeAddress
2.One  to many   => Group    => Stories
3.Many to One    => Stories  => Group
2.Many to many   => Book     =>  Author




JPA is ORM specfication
=======================
Hibernate
toplink
ibatis
















Case Study
===========
https://o7planning.org/10683/create-a-shopping-cart-web-application-with-spring-boot-hibernate







