# Spring
- Dependency Injection framework
- The IoC container provides and manages the life cycle of the objects.
- @Component - denotes that Spring needs to create and manage the life cycle of the Bean (class)
- @Autowired
    - Denotes that the object will be created by Spring and injected. By default spring uses autowire by Type.
    - No need to provide constructor or setter to autowire the bean. Spring uses default setter injection to Autowire the bean.
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
- Bean scope
    - singleton - one instance per Spring Context - by default spring creates beans with this scope.
    - prototype - new bean created when requested
    - request - one bean per HTTP request
    - session - one bean per HTTP session

If we want to use combination of Singleton and Prototype beans, we need to create proxy for Prototype bean.
Example: here spring injects new instance of DBConnection when the request is made to context.
```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_SINGLETON)
public class SalesDaoImpl {
    
    @Autowired
    private DBConnection connection;
}
```
```java
@Component
@Scope(value=ConfigurableBeanFactory.SCOPE_PROTOTYPE, proxyMode = ScopedProxyMode.TARGET_CLASS)
public class DBConnection {

}
```