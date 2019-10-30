# example-grails-docker

This repo holds an example grails applications running as docker container.


Dockerfile is in `src/main/docker` folder. It gets copied to build folder by `prepareDocker` task defined in    build.gradle` file.

Note that the `prepareDocker` task depends on `assemble` task that builds a war file in `build/libs` folder. 
This war file is copied to docker work folder along with the copied `Dockerfile`. 

```bash
./gradlew prepareDocker
```

Use this command to build an image with tagging.

```bash
docker build --tag="binlecode/test-g400:0.1" build/docker/
```

Use this command to create a container listening on port `8080`.

```bash
docker run -p 8080:8080 --name ikali-test-g400 binlecode/test-g400:0.1
```

To attach to the running container for debugging or log tracking

```bash
docker exec -ti ikali-test-g400 /bin/sh
```