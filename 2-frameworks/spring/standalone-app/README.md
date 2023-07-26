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

## 2. Dependency Injection
Dependency injection can be configured in Spring using 3 strategies, which will be shown below.

We'll use a basic service interface to represent the services we'll be manipulating:
```java
package org.javawits.example.service;

/**
 * Basic operations for a Greeting service.
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
		// construct the Application Context from an annotated config class
		ApplicationContext annotationAppContext = new AnnotationConfigApplicationContext(SpringConfig.class);

		// Get the service
		GreetingService service = annotationAppContext.getBean(GreetingService.class);

		// call the service method
		service.greet();
		service.greet("Earthling");
	}

}
```

When we run the App.java class, the output looks like this:
<pre>
Hello! I'm a Java-based configured Spring service!
Hello Earthling!
</pre>

### 2.2. XML-based configuration

We'll create another implementation of the GreetingService interface:
```java
package org.javawits.example.service;

public class GreetingServiceXmlBasedConfigImpl implements GreetingService {

	@Override
	public void greet() {
		System.out.println("Hello! I'm an XML-based configured Spring service!");
	}

	@Override
	public void greet(String name) {
		System.out.println(String.format("Welcome to XML, %s!", name));
	}

}
```

The next step is to create the XML file, which we'll call 'spring-beans.xml', specifying which objects spring will manage for us (create the file in the 'src/main' directory, i.e., the file path will be 'src/main/spring-beans.xml':
```xml
<?xml version="1.0" encoding="UTF-8"?>

<!-- Define this file as a spring beans definition -->
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="
    http://www.springframework.org/schema/beans 
    http://www.springframework.org/schema/beans/spring-beans.xsd">

  <!-- Define a bean -->
  <bean id="xmlGreetingService" class="org.javawits.example.service.GreetingServiceXmlBasedConfigImpl" />
  
</beans>
```
Finally, let's add code to the main() method in App.java, that will load the Spring beans from the XML file (create a new Application context) and call the service:
```java
	// construct Application Context from XML file
	FileSystemXmlApplicationContext xmlAppContext = new FileSystemXmlApplicationContext(
			"src/main/spring-beans.xml");

	// get the service from the XML file context and call
	GreetingService serviceXml = xmlAppContext.getBean(GreetingService.class);
	serviceXml.greet();
	serviceXml.greet("Lennon");
```

After we run App.java again, now the output looks like this:
<pre>
Hello! I'm a Java-based configured Spring service!
Hello Earthling!
Hello! I'm an XML-based configured Spring service!
Welcome to XML, Lennon!
</pre>

# References
- https://www.baeldung.com/spring-application-context
- 
