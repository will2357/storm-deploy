## Getting Started

This project makes it dead-simple to deploy Storm clusters on AWS. See [the wiki](https://github.com/nathanmarz/storm-deploy/wiki) for instructions on using this deploy.

## Acknowledgements

YourKit is kindly supporting open source projects with its full-featured Java Profiler. YourKit, LLC is the creator of innovative and intelligent tools for profiling Java and .NET applications. Take a look at YourKit's leading software products: [YourKit Java Profiler](http://www.yourkit.com/java/profiler/index.jsp) and [YourKit .NET Profiler](http://www.yourkit.com/.net/profiler/index.jsp).

## Dependencies

* [Leiningen 1.7.1](https://github.com/technomancy/leiningen)
* [Storm 0.8.1](https://github.com/nathanmarz/storm)

## EC2 Deployment

* Confirmed to work on 64-Bit Ubuntu 10.04 (ami-1db20274)
* Starting and stopping the server:
    * `lein run :deploy --start --name test-storm --release 0.8.1`
    * `lein run :deploy --stop --name test-storm`
* Attach local machine to storm-deploy cluster (this automatically configures `~/.storm/storm.yml`)
    * `lein run :deploy --attach --name test-storm`
* UI is available at http://[NimbusServer]:8080/
* Ganglia information is available at http://[NimbusServer]:8080/ganglia/index.php

## Examples

See this slightly modified [storm-starter](https://github.com/will2357/storm-starter)

### Java Example

Setup:
```
lein deps
mvn -f m2-pom.xml package
```

Submit topology to local Storm server:
```
java -cp target/storm-starter-0.0.1-SNAPSHOT-jar-with-dependencies.jar storm.starter.ExclamationTopology
```

Submit topology to EC2 Storm cluster:
```
storm jar target/storm-starter-0.0.1-SNAPSHOT.jar storm.starter.ExclamationTopology storm-java-test
```

Stop topology on EC2 Storm cluster:
```
storm kill storm-java-test
```

### Clojure Example

Setup:

```
lein deps
lein compile
```

Submit topology to local Storm server:
```
lein run -m storm.starter.clj.word-count
```

Submit topology to EC2 Storm cluster:
```
storm jar target/storm-starter-0.0.1-SNAPSHOT.jar storm.starter.clj.word_count storm-clojure-test
```

Stop topology on EC2 Storm cluster:
```
storm kill storm-clojure-test
```
