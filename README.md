### Info
This simple project is meant to be a series of example showing how to use
Phosphor. Bear in mind that I created this in the process of learning
how to use Phosphor myself, so there are bound to be mistakes/inefficiencies in the examples.
These are solely my responsibility and should not be viewed as a reflection of anyone elses work.


### Running
In order to run the examples, you must download the Phosphor project and build it.
See [Phosphor](https://github.com/gmu-swe/phosphor) for more information. 
To setup Phosphor first clone the project from the link above, then follow the instructions below. 
Before you can start, you need to install `maven` and Oracle or OpenJDK Java 8. 

1. Find out JRE path
```
whereis java
```
or 
```
locate java
```
The path to my Java 8 JRE path is `/usr/lib/jvm/java-8-openjdk/jre/`. You probably need to alter part in the following commands.

1. setup Phosphor & create Phosphor*-SNAPSHOT.jar

```
cd /path/to/Phosphor/project
mvn install 
```

2. Insturument JRE with Phosphor (which will be placed in jre-inst)

```
java -jar Phosphor/target/Phosphor-0.0.5-SNAPSHOT.jar /usr/lib/jvm/java-8-openjdk/jre/ jre-inst
chmod +x jre-inst/bin/*
```       
For control flow tracking use instead:
```       
java -jar Phosphor/target/Phosphor-0.0.5-SNAPSHOT.jar -controlTrack /usr/lib/jvm/java-8-openjdk/jre/ jre-inst
chmod +x jre-inst/bin/*
```        

3. Clone this example into the main directory of the Phosphor project (so the path is  ..../phosphor/phosphor-example). For building the example, execute:
```
cd /path/to/phophor-examples
mvn install:install-file -Dfile=../Phosphor/target/Phosphor-0.0.5-SNAPSHOT.jar -DgroupId=edu.columbia.cs.psl.phosphor -DartifactId=Phosphor -Dversion=0.0.5-SNAPSHOT -Dpackaging=jar #installs jar as local artifacte in ~/.m2/
mvn package # creates jar with examples in phosphor-examples/target
```


4. To execute the `ImplicitFlowsExamples`: 
```
cd .. # now at phophor main directory
jre-inst/bin/java -Xbootclasspath/a:Phosphor/target/Phosphor-0.0.5-SNAPSHOT.jar -javaagent:Phosphor/target/Phosphor-0.0.5-SNAPSHOT.jar=taintSources=phosphor-examples/src/main/resources/taint-sources,taintSinks=phosphor-examples/src/main/resources/taint-sinks -cp phosphor-examples/target/phosphor-examples-1.0-SNAPSHOT.jar -ea com.josecambronero.ImplicitFlowsExamples 
```
Alternativly:
```
Phosphor/target/jre-inst/bin/java -Xbootclasspath/a:Phosphor/target/Phosphor-0.0.5-SNAPSHOT.jar -javaagent:Phosphor/target/Phosphor-0.0.5-SNAPSHOT.jar -cp phosphor-examples/target/phosphor-examples-1.0-SNAPSHOT.jar -ea com.josecambronero.ImplicitFlowsExamples
```



If you'd like to read along with the notes I made for this project, run
`mvn latex:latex` which creates a pdf report at target/site/notes.pdf
