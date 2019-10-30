# example-grails-docker

This repo holds an example grails applications running as docker container.


Dockerfile is in `src/main/docker` folder. It gets copied to build folder by `prepareDocker` task defined in    build.gradle` file.

Note that in the `Dockerfile`, the jdk version is 8, from [openjdk docker hub](https://hub.docker.com/_/openjdk) documentation:
> On startup JVM tries to detect the number of available CPU cores and the amount of RAM to adjust its internal parameters (like the number of garbage collector threads to spawn) accordingly. When container is run with limited CPU/RAM, standard system API, used by JVM for probing, will return host-wide values. This can cause excessive CPU usage and memory allocation errors with older versions of JVM.
> In OpenJDK 11 this is turned on by default. In versions 8, 9, and 10 you have to enable the detection of container-limited amount of RAM using the following options: 
`$ java -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap ...`


Note that the `prepareDocker` task depends on `assemble` task that builds a war file in `build/libs` folder. 
This war file is copied to docker work folder along with the copied `Dockerfile`. 

```bash
./gradlew prepareDocker
```

Use this command to build an image with tagging.

```bash
docker build --tag="binlecode/example-grails-docker:0.1" build/docker/
```

To run the container in desposible mode (one-time run only), use `--rm` option. 
This container will be automatically removed after run.

```bash
docker run -p 8080:8080 --rm binlecode/example-grails-docker:0.1
```

Use this command to create a regular container.

```bash
docker run -p 8080:8080 --name ikali-grails-docker binlecode/example-grails-docker:0.1
```

To attach to the running container for debugging or log tracking

```bash
docker exec -ti ikali-grails-docker /bin/sh
```