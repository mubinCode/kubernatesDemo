# Stage 1: Build with Gradle
FROM gradle:8.5-jdk17 AS build
WORKDIR /home/app

# Copy project files
COPY . .

# Build the project
RUN gradle bootJar --no-daemon

# Stage 2: Run the application
FROM eclipse-temurin:17-jdk-jammy

# Set environment variables
ENV JAVA_OPTS="" \
    SPRING_PROFILES_ACTIVE=prod

WORKDIR /app

# Copy the built JAR from the build stage
COPY --from=build /home/app/build/libs/*.jar app.jar

# Expose the port your Spring Boot app runs on
EXPOSE 8080

# Run the app
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
