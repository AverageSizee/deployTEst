# Use a stable JDK (21) to build the project
FROM eclipse-temurin:21-jdk AS build


# Copy Maven Wrapper and project files
COPY mvnw ./
COPY .mvn .mvn
COPY pom.xml .

# Ensure Maven wrapper is executable
RUN chmod +x mvnw

# Download dependencies (cached layer)
RUN ./mvnw dependency:go-offline -B

# Copy the source code
COPY src src

# Build the application
RUN ./mvnw clean package -DskipTests

# Use a smaller JRE for the final image
FROM eclipse-temurin:21-jre

# Copy the built JAR file
COPY --from=build /app/target/*.jar backend.jar

# Expose the application port
EXPOSE 8080

# Start the application
ENTRYPOINT [ "java", "-jar", "backend.jar" ]
