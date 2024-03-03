# edu-blackboard

## Prepare

> Determine your package, in this example we use net.miwashi as we own the domain miwashi.net.
> It will be up to you to figure out a package, you either own, or that isn't owned by someone.
> Replace net.miwashi with the package of your choice.

## Instructions

```bash
cd ~
cd ws
rm -rf blackboard #Careful not to delete wrong files
mkdir blackboard && cd blackboard
mkdir -p ./app/src/test/{java,resources}
mkdir -p ./app/src/main/{java,resources}
mkdir -p ./app/src/main/java/net/miwashi
mkdir -p ./app/src/test/java/net/miwashi
```


## ./settings.gradle

```bash
cd ~
cd ws
cd blackboard
cat > settings.gradle << 'EOF'
rootProject.name = 'blackboard'
include('app')
EOF
```

## ./app/build.gradle

```bash
cd ~
cd ws
cd blackboard
cat > ./app/build.gradle << 'EOF'
plugins {
    id 'application'
}

repositories {
    jcenter()
}

dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter-api:5.6.2'
    testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine'
}

application {
    mainClass = 'net.miwashi.App'
}

tasks.named('test') {
    useJUnitPlatform()
}
EOF
```

## pom.xml

```bash
cd ~
cd ws
cd blackboard
cat > ./pom.xml << 'EOF'
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>net.miwashi</groupId>
    <artifactId>blackboard</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>blackboard</name>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.target>1.8</maven.compiler.source>
        <junit.jupiter.version>5.6.2</junit.jupiter.version>
        <mainClass>net.miwashi.App</mainClass>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>${junit.jupiter.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>${junit.jupiter.version}</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>${maven.compiler.source}</source>
                    <target>${maven.compiler.target}</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.22.2</version>
                <configuration>
                    <useModulePath>false</useModulePath>
                    <includes>
                        <include>**/*Tests.java</include>
                        <include>**/*Test.java</include>
                    </includes>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.2.0</version>
                <configuration>
                    <archive>
                        <manifest>
                            <addClasspath>true</addClasspath>
                            <classpathPrefix>lib/</classpathPrefix>
                            <mainClass>${mainClass}</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
EOF
```

## ./app/src/main/java/net/miwashi/App.java

```bash
cd ~
cd ws
cd blackboard
cat > ./app/src/main/java/net/miwashi/App.java << EOF
package net.miwashi;

public class App {
    public String getGreeting() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        System.out.println(new App().getGreeting());
    }
}
EOF
```

## ./app/src/test/java/net/miwashi/AppTest.java

```bash
cd ~
cd ws
cd blackboard
cat > ./app/src/test/java/net/miwashi/App.java << EOF
package net.miwashi;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class AppTest {
    @Test void appShouldHaveAGreeting() {
        App classUnderTest = new App();
        assertNotNull(classUnderTest.getGreeting(), "app should have a greeting");
    }
}
EOF



