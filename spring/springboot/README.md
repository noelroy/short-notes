# Spring Boot

## Controller

This is where the api requests come in and the results are served. To create a simple Controller :
1. Create a class to contain all the rest end points
2. Add `@RestController` annotation to the class
3. Add `@RequestMapping` to set the api path for the controller
4. For each separate method inside the class add the following annotation as per the call
    1. `@GetMapping`
    2. `@PostMapping`
    3. `@PutMapping`
    4. `@DeleteMapping`  

```java
@RestController
@RequestMapping(path = "/api/expenses")
public class ExpenseController {

    @GetMapping
    public List<String> getItems(){
        return List.of("Stationary", "Snacks");
    }
}
```

## Model

Create classes that represent the table to be created in the database
```java
// @Data is a lombok annotation that auto populates setter, getters and toString methods
@Data
public class Expense {
    private Long id;
    private String description;
    private Float amount;
    private LocalDate date;
}

```

For Postgres use the following configuration in the application.properties file
```properties
# Configurations for the database connection
spring.datasource.url=jdbc:postgresql://localhost:5432/springbootdb
spring.datasource.username=postgres
spring.datasource.password=postgres@123

# Show or not log for each sql query
spring.jpa.show-sql=true
# Hibernate ddl auto (create, create-drop, update): with "create-drop" the database
# schema will be automatically created afresh for every start of application
spring.jpa.hibernate.ddl-auto=create-drop

# Allows Hibernate to generate SQL optimized for a particular DBMS
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```

### Business Layer
Instead of writing all the logic in controller class,  business logic can be kept in  separate file called service. Annotate this class with the `@Service` or `@Component` to indicate that it has to be automatically injected