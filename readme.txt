
Day1    23-Jan-2021
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

Write a Java application to perform standard CRUD operations on Customer and Account Domain Objects

Account:
        accno
		name 
        balance
        doc
        type
        
        
Customer
        customerId
        name
        pan
        mobile         
        account
        address
        dob
        
        
         
CustomerMainApp
              CustomerService
                           CustomerDao
                                        MapCustomerServiceImpl
                                                                CustomerMap
                                                                   



Day2  :24-Jan-2021
======
IOC -Inversion of Control -Don't call me I  will call you
DI  -It is a mechanism of initializing the dependencies 

      1.setter injection
      2.constructor injection      
      
      
Step 1: create a Java Project and add spring jar files to class path


Step 2: create a spring container

1.Core Container -BeanFactory based
2.Advanced Container -ApplicationContext
3.Web Container -WebApplicationContext


                             BeanFactory (I)
                                 |
                                 |XMLBeanFactory (C) :Lazy Initialization
                                 |
                            ApplicationContext(I)   :Eager Initialization
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

