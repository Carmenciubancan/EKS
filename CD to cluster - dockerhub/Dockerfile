FROM eclipse-temurin:17-jre

# Use a fixed working directory inside the container
WORKDIR /app

# Copy the built jar from the Maven target/ directory
COPY target/*.jar /app/app.jar

# App listens on port 8080
EXPOSE 8080

# Run the Spring Boot app
ENTRYPOINT ["java", "-jar", "/app/app.jar"]