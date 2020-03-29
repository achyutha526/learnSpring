# Spring
- Dependency Injection framework
- The IoC container provides and manages the life cycle of the objects.
- @Component - denotes that Spring needs to create and manage the life cycle of the Bean (class)
- @Autowired
    - Denotes that the object will be created by Spring and injected. By default spring uses autowire by Type.
    - We can also use combination of both Bean type and name for autowiring in case of conflicts (both beans implementing same interface)
```java
@Component
public class SpringComponentScanExample {
    
    @Autowired
    private IEmployeeDao salesPersonImpl;
}
```
```java
@Component
public class SalesPersonImpl {
    
}
```
- @Primary 
    - Denotes the bean to be autowired in case of multiple implementations are present for the given interface.
    - The bean with @Primary will be injected in case if there is a matching bean with name.
- @Qualifier
    - Denotes the type of bean to be injected matching with qualifier name (provided in arguments)
```java
@Component
public class SpringComponentScanExample {
    
    @Autowired("sales")
    private IEmployeeDao employeeDao;
}
```
```java
@Component
@Qualifier("sales")
public class SalesDaoImpl {
    
}
```
- @ComponentScan
    - Denotes packages and it sub packages where spring search for the beans (marked with @Component).
    - if a class is annotated with @ComponentScan, the current package and all it's sub packages will be scanned for beans.
    - We can pass a specific package info as argument to component scan.

```java
@Configuration
@ComponentScan(basePackages = "com.spring.demo")
public class SpringComponentScanExample {
 
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```