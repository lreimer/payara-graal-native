# Payara Graal Native Image

Experiment on running Payara using GraalVM as native image. The idea was to build
an UberJar using the Gradle Plugin, then start Payara using the Graal tracing agent
and then call the `native-image` command with the generated JSON files.

```bash
$ ./gradlew assemble
$ ./gradlew microBundle microStart
$ ./gradlew graalNativeImage
```

Well, turns out it is not that easy! :disappointed:

The things seems to be that all dependencies are embedded JAR files in the UberJar.
When Graal tries to access these files during compilation these are obviously not
on the classpath. Graal Native Images have the limitation that dynamic class loading is
not supported.
https://github.com/oracle/graal/blob/master/substratevm/LIMITATIONS.md#dynamic-class-loading--unloading

## Maintainer

M.-Leander Reimer (@lreimer), <mario-leander.reimer@qaware.de>

## License

This software is provided under the MIT open source license, read the `LICENSE`
file for details.
