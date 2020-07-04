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
