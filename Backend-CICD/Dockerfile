# Stage 1: Build with Maven + JDK 17
FROM maven:3.8.7-eclipse-temurin-17 AS builder

WORKDIR /app
COPY pom.xml .
COPY src ./src

# Build the Spring Boot JAR
RUN mvn clean package -DskipTests

# Stage 2: Run with lightweight JDK 17 (Correct image)
FROM eclipse-temurin:17-jdk-jammy

WORKDIR /app

# Copy built JAR from builder stage
COPY --from=builder /app/target/*.jar app.jar

# Create a non-root user for security
RUN groupadd -r spring && useradd -r -g spring spring
USER spring

# Expose backend port
EXPOSE 5050

# Start backend server
ENTRYPOINT ["java", "-jar", "app.jar"]
