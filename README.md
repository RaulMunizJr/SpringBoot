# SpringBoot

## Spring Bean Annotation
- Component Scanning
@ComponentScan configures which packages to scan for classes with annotation configuration. We can specify the base package names directly with one of the basePackages or value arguments (value is an alias for basePackages)
```
@Configuration                                                      @Configuration
@ComponentScan(basePackages = "com.baeldung.annotations")           @ComponentScan(basePackageClasses = VehicleFactoryConfig.class)
class VehicleFactoryConfig {}                                       class VehicleFactoryConfig {}
```
- Component
@Component is a class level annotation. During the component scan, Spring Framework automatically detects classes annotated with @Component.
```
@Component
class CarUtility {
    // ...
}
//By default, the bean instances of this class have the same name as the class name with a lowercase initial. 
//On top of that, we can specify a different name using the optional value argument of this annotation.
```
> Since @Repository, @Service, @Configuration, and @Controller are all meta-annotations of @Component, they share the same bean naming behavior. Also, Spring automatically picks them up during the component scanning process.

- Repository
DAO or Repository classes usually represent the database access layer in an application, and should be annotated with @Repository:
```
@Repository
class VehicleRepository {
    // ...
}
```
- Service
The business logic of an application usually resides within the service layer – so we'll use the @Service annotation to indicate that a class belongs to that layer:
```
@Service
public class VehicleService {
    // ...    
}
```
- Controller
@Controller is a class level annotation which tells the Spring Framework that this class serves as a controller in Spring MVC:
```
@Controller
public class VehicleController {
    // ...
}
```
- Configuration
Configuration classes can contain bean definition methods annotated with @Bean:
```
@Configuration
class VehicleFactoryConfig {
 
    @Bean
    Engine engine() {
        return new Engine();
    }
 
}
```
## Spring Data Annotations
- @NoRepositoryBean, @Transactional : https://www.baeldung.com/spring-data-annotations

- @Param
We can pass named parameters to our queries using @Param:
```
@Query("FROM Person p WHERE p.name = :name")
Person findByName(@Param("name") String name);
//More Details Here: https://www.baeldung.com/spring-data-jpa-query
```
- @Id
@Id marks a field in a model class as the primary key:
```
class Person {
 
    @Id
    Long id;
 
    // ...
     
}
```
- @Modifying
We can modify data with a repository method if we annotate it with @Modifying:
```
@Modifying
@Query("UPDATE Person p SET p.name = :name WHERE p.id = :id")
void changeName(@Param("id") long id, @Param("name") String name);
```
## Spring Web Annotations
- RequestMapping
> Simply put, @RequestMapping marks request handler methods inside @Controller classes; it can be configured using:
> path, or its aliases, name, and value: which URL the method is mapped to
> method: compatible HTTP methods
> params: filters requests based on presence, absence, or value of HTTP parameters
> headers: filters requests based on presence, absence, or value of HTTP headers
> consumes: which media types the method can consume in the HTTP request body
> produces: which media types the method can produce in the HTTP response bod
```
@Controller
class VehicleController {
 
    @RequestMapping(value = "/vehicles/home", method = RequestMethod.GET)
    String home() {
        return "home";
    }
}
```
We can provide default settings for all handler methods in a @Controller class if we apply this annotation on the class level. The only exception is the URL which Spring won't override with method level settings but appends the two path parts.
```
@Controller
@RequestMapping(value = "/vehicles", method = RequestMethod.GET)
class VehicleController {
 
    @RequestMapping("/home")
    String home() {
        return "home";
    }
}
```
- RequestBody
Let's move on to @RequestBody – which maps the body of the HTTP request to an object:
```
@PostMapping("/save")
void saveVehicle(@RequestBody Vehicle vehicle) {
    // ...
}
```
