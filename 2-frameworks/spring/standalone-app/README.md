# Standalone Spring App

This sections focuses on using the Spring Framework in a standalone Java application.

## Topics
1. Creating the application
2. Dependency injection
    - 2.1 Java-based configuration
    - 2.2 XML-based configuration
    - 2.3 Annotation-based configuration

## 1. Creating the application

Run the command below to create a standalone Java application:
```console
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart \
    -DgroupId=org.javawits.example \
    -DartifactId=SpringStandaloneApp \
    -Dversion=1.0-SNAPSHOT \
    -DinteractiveMode=false
```

Now add a dependency in the pom.xml to the [spring-context](https://mvnrepository.com/artifact/org.springframework/spring-context) artifact:
```xml
  ...
  <dependencies>
    ...

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>6.0.11</version>
    </dependency>

  </dependencies>
```

The application can be run by running the App.java class (in your preffered IDE).

## 2. Dependenc Injection
Dependency injection can be configured in Spring using 3 strategies, which will be shown below.

We'll use a basic service interface to represent the services we'll be manipulating:
```java
package org.javawits.example.service;

/**
 * Basic operations for a Greeting serivice.
 */
public interface GreetingService {

	void greet();

	void greet(String name);

}
```

### 2.1. Java-based configuration
This is the preferred Spring bean configuration method.

First, we create the service class (implementing the interface):
```java
package org.javawits.example.service;

public class GreetingServiceJavaBasedConfigImpl implements GreetingService {

	@Override
	public void greet() {
		System.out.println("Hello! I'm Java-based configured Spring service!");
	}

	@Override
	public void greet(String name) {
		System.out.println(String.format("Hello %s!", name));
	}

}
```

Next, we create a class and annotate it with the @Configuration annotation, and add a method annotated with @Bean returning each service we want Spring to manage:
```java
@Configuration
public class SpringConfig {

	@Bean
	GreetingService greetingService() {
		return new GreetingServiceJavaBasedConfigImpl();
	}

}
```

Finally, we can modify the App.java class to create the application context (spring container that manages beans), load the service and call the service method:
```java
/**
 * Standalone app created with Maven
 */
public class App {

	public static void main(String[] args) {
		// construct the Application Context
		ApplicationContext annotationAppContext = new AnnotationConfigApplicationContext(SpringConfig.class);

		// Get the service
		GreetingService service = annotationAppContext.getBean(GreetingService.class);

		// call the service method
		service.greet();
		service.greet("Earthling");
	}

}
```
### 2.2. XML-based configuration

We'll create another implementation of the GreetingService interface:
```java
```

# References
- https://www.baeldung.com/spring-application-context
- 
