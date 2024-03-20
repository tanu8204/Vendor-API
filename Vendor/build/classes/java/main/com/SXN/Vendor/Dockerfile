# Use the official OpenJDK 17 image as the base image for building
FROM gradle:jdk17 as builder

# Set the working directory inside the container
WORKDIR /app

# Copy the Gradle project files
COPY . .

# Build the application
RUN gradle build

# Use a lightweight base image for the runtime environment
FROM openjdk:17-jdk-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the compiled JAR file from the build stage to the container
COPY --from=builder /app/build/libs/*.jar app.jar

# Expose the port that your application runs on (adjust if necessary)
EXPOSE 8082

# Command to run the application when the container starts
CMD ["java", "-jar", "app.jar"]
