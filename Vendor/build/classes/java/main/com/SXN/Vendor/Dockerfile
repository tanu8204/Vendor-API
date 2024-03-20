# # Use the official OpenJDK 17 image as the base image for building
# FROM gradle:jdk17 as builder

# # Set the working directory inside the container
# WORKDIR /app

# # Copy the Gradle project files
# COPY . .

# # Build the application
# RUN gradle build

# # Use a lightweight base image for the runtime environment
# FROM openjdk:17-jdk-alpine

# # Set the working directory inside the container
# WORKDIR /app

# # Copy the compiled JAR file from the build stage to the container
# COPY --from=builder /app/build/libs/*.jar app.jar

# # Expose the port that your application runs on (adjust if necessary)
# EXPOSE 8082

# # Command to run the application when the container starts
# CMD ["java", "-jar", "app.jar"]

# Use JDK 17 instead of JDK 8
FROM openjdk:17-jdk-slim AS build

# Copy the project files to the container
COPY . .

# Set the working directory
WORKDIR /Vendor/build/classes/java/main/com/SXN/vENDOR/gradle/src

# Run the Gradle build
RUN ./gradlew build --no-daemon

# Use JDK 17 slim image for the runtime environment
FROM openjdk:17-jre-slim

# Expose port 8080
EXPOSE 8082

# Create a directory for the application
RUN mkdir /app

# Copy the built JAR from the build stage to the runtime stage
COPY --from=build /Vendor/build/classes/java/main/com/SXN/vENDOR/gradle/src
/build/libs/*.jar /app/spring-boot-application.jar

# Set the entry point to run the Spring Boot application
ENTRYPOINT ["java", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/app/spring-boot-application.jar"]

