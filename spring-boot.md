# Spring Boot

## Externalizing configuration
- Spring supports reading external properties file.

```java
@Configuration
@PropertySource("classpath:demo.properties")
public class PropsUsingJavaConf {
}
```
- Spring boot supports reading properties files from application.properties.
- We can provide different value at run time using --spring.config.location=classpath:/diff-app.properties
- We can provide environment specific properties file using application-DEV.properties and we can invoked appropriate file using spring profile -Dspring.profiles.active=DEV
- We can provide Hierarchical properties using @ConfigurationProperties annotation.
```
    server.hostname=localhost
    server.port=9090
```
```java
@ConfigurationProperties("server")
public class Application {
    String hostname;
    String port;

    // getters and setters here
}
```
- Spring boot supports reading properties from YAML file. This is good for hirerarchical property storage
```yaml
server:
 hostname: localhost
 port: 9090
```
- We can pass the proprties using below types
    - passed at command line ( java -jar app.jar --serverName=test)
    - passed as system property (java -DserverName=test -jar app.jar)
    - passed from environment variables (export servername=test)
- We can create random property values in property file(random.number=${random.int})
- We can access the property values using
    - @Value("${serverName}")
    - Environment API.
```java
@Autowired
private Environment env;

//in the code
env.getProperty("serverName");
```
- In order to get full control on the configuration, We need to create PropertySourcesPlaceholderConfigurer Bean and register it manually.
```java
@Bean
    public PropertySourcesPlaceholderConfigurer propertySourcesPlaceholderConfigurer() {
        PropertySourcesPlaceholderConfigurer propertySourcesPlaceholderConfigurer = new PropertySourcesPlaceholderConfigurer();
        propertySourcesPlaceholderConfigurer.setLocations(new ClassPathResource("app.properties"));
        return propertySourcesPlaceholderConfigurer;
    }
```