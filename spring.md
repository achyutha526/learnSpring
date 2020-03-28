# Spring
- Dependency Injection framework
- The IoC container provides and manages the life cycle of the objects.
- @Component - denotes that Spring needs to create and manage the life cycle of the Bean (class)
- @Autowired - denotes that the object will be created by Spring and injected.
- @ComponentScan
    - Denotes packages and it sub packages where spring search for the beans (marked with @Component).
    - if a class is annotated with @ComponentScan, the current package and all it's sub packages will be scanned for beans.
    -  We can pass a specific package info as argument to component scan.

```java
@Configuration
@ComponentScan(basePackages = "com.spring.demo")
public class SpringComponentScanExample {
 
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
```