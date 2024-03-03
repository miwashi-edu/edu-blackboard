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
    testLogging {
        showStandardStreams = true
        events "passed", "failed", "skipped"
    }
}
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


## Test it

```bash
gradle check --rerun-tasks
gradle test
gradle run
```

