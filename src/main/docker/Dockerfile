FROM openjdk:8u151-jdk-alpine

EXPOSE 8080

WORKDIR /app
COPY *.war application.jar

# for jdk8, need to enable jvm to detect container limited memory
CMD ["java", "-Djava.security.egd=file:/dev/./urandom", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-jar","/app/application.jar"]