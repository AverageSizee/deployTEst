# Use a compatible JDK 23 image
FROM eclipse-temurin:23-jdk AS build
COPY . .
RUN mvn clean package -DskipTests

FROM openjdk:25-slim
COPY --from=build /target/Backend-0.0.1-SNAPSHOT.jar backend.jar
EXPOSE 8080
ENTRYPOINT [ "java", "-jar", "backend.jar" ]