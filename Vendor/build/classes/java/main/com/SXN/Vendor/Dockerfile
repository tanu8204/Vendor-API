# Use JDK 17 instead of JDK 8
FROM openjdk:17-jdk-slim AS build


# Copy the project files to the container
COPY . .

# Set the working directory
WORKDIR /Vendor/build/classes/java/main/com/SXN/Vendor/gradle/src

# Run the Gradle build
RUN Vendor/build/classes/java/main/com/SXN/Vendor/gradle build --no-daemon

# Use JDK 17 slim image for the runtime environment
FROM openjdk:17.0.1-jdk-slim

# Expose port 8080
EXPOSE 8082

# Create a directory for the application
RUN mkdir /app

# Copy the built JAR from the build stage to the runtime stage
COPY --from=build /Vendor/build/classes/java/main/com/SXN/Vendor/gradle/src/build/libs/Vendor.0.0.1-SNAPSHOT.jar /app/spring-boot-application.jar

# Set the entry point to run the Spring Boot application
ENTRYPOINT ["java", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/app/spring-boot-application.jar"]

CMD ["/bin/bash"]
