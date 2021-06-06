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
jackson-annotations-2.9.0.jar
jackson-databind-2.9.8.jar












