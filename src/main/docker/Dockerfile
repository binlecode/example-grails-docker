FROM openjdk:8u151-jdk-alpine

EXPOSE 8080

WORKDIR /app
COPY *.war application.jar

CMD ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar","/app/application.jar"]