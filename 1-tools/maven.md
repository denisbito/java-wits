# Maven

Apache [Maven](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) is a popular tool for managing Java software projects. It can help create, build, test, document, and deploy apps.

## Create a new Java project

This command creates a new bare bones java project, interactively:
```console
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart
```

when asked, inform theses arguments:
- 'groupId': group identifier; normally a dot separated Java package structure, i.e, "org.javawits.example"
- 'artifactId': name of the artifact or project, i.e. "HelloWorldApp" or anything similar
- 'version': the version string. Leave empty to accept the default version "1.0-SNAPSHOT"
- 'package': base java package for the Java classes in the project. Leave empty to default to the 'groupId'
- lastly, you may be asked confirmation; just press 'Enter'

Or, to create the project in one go (non-interactively), run:
```console
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart \
    -DgroupId=org.javawits.example
    -DartifactId=HelloWorldApp
    -DarchetypeVersion=1.0-SNAPSHOT
```

