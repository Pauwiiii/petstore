# --- Stage 1: Build the Maven application ---
FROM maven:3.8.5-openjdk-17-slim AS build
WORKDIR /app

# Copy the pom.xml and source code
COPY backend/pom.xml .
COPY backend/src ./src

# Package the application (skipping tests for faster build times)
RUN mvn clean package -DskipTests

# --- Stage 2: Run the application ---
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app

# Copy the built jar from the build stage
COPY --from=build /app/target/petstore-backend-0.0.1-SNAPSHOT.jar app.jar

# Expose port 8080 (Render dynamic port binding)
EXPOSE 8080

# Run the jar file
ENTRYPOINT ["java", "-jar", "app.jar"]
