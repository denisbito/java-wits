# Standalone Spring App

This sections focuses on using the Spring Framework in a standalone Java application.

## Topics
  1. Creating the application
  2. Dependency Injection via XML

## 1. Creating the application

Run the command below to create a standalone Java application:
```console
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart \
    -DgroupId=org.javawits.example \
    -DartifactId=SpringStandaloneApp \
    -Dversion=1.0-SNAPSHOT \
    -DinteractiveMode=false
```

Now add a dependency in the pom.xml to the [spring-core](https://mvnrepository.com/artifact/org.springframework/spring-core) artifact:
```xml
  ...
  <dependencies>
    ...
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-core -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>6.0.11</version>
    </dependency>
  </dependencies>
```

## 2. Dependency Injection via XML
