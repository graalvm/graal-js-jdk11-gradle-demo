# Running GraalJS on stock JDK11

This is a simple Gradle project that demonstrates how it's possible to run
[GraalJS](http://www.graalvm.org/docs/reference-manual/languages/js/) on a
stock JDK11. The application is a simple JavaScript benchmark embedded in a
Java application which compares performance of GraalJS and Nashorn.

## Pre requirements

- Linux or Mac OS
- [JDK11](https://jdk.java.net/11/)

## Setup

- Clone this repository
```
git clone https://github.com/graalvm/graal-js-jdk11-gradle-demo.git
```

- Move to the newly cloned directory
```
cd graal-js-jdk11-gradle-demo
```

- Make sure that JAVA_HOME is pointed at a JDK11 (you can run the 
benchmark with older JDKs as well, but Graal won't be used)
```
export JAVA_HOME=/path/to/jdk11; java -version
```

## Execution

The project provides a custom [JavaExec](https://docs.gradle.org/current/dsl/org.gradle.api.tasks.JavaExec.html) `run` task
which sets up the JVM to use the Graal compiler to JIT compile JavaScript for better performance. You can turn off this
behaviour by setting the system property `graal` to `off`. The execution outputs benchmark results for GraalJS 
(via the [GraalVM Polyglot API](https://www.graalvm.org/truffle/javadoc/index.html?com/oracle/truffle/api/instrumentation/EventContext.html)
and the [Java Scripting API](https://docs.oracle.com/javase/8/docs/technotes/guides/scripting/prog_guide/api.html)) and Nashorn.



To Execute with Graal, run
```
./gradlew run
```

To Execute without Graal, run
```
./gradlew run -Dgraal=off
```

The benchmark prints the time per iteration in milliseconds, so lower values are better.

## Running on GraalVM

This project is also setup to run on GraalVM. The setup is the same except
that your JAVA_HOME should point to a directory contain GraalVM. In this case,
the `graal` system property has no effect since Graal is always available.
