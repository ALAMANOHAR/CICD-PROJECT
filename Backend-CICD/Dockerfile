# # Multi-stage build for optimized image
# FROM maven:3.8-openjdk-17 AS builder
# WORKDIR /app
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package -DskipTests

# FROM openjdk:17-slim
# WORKDIR /app
# COPY --from=builder /app/target/*.jar app.jar

# # Create a non-root user for security
# RUN groupadd -r spring && useradd -r -g spring spring
# USER spring

# EXPOSE 5050
# ENTRYPOINT ["java", "-jar", "app.jar"]


# Stage 1: Build with Maven + JDK 17
FROM maven:3.8.7-eclipse-temurin-17 AS builder

WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Run with lightweight JDK 17
FROM eclipse-temurin:17-jdk-slim
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar

# Create a non-root user for security
RUN groupadd -r spring && useradd -r -g spring spring
USER spring

EXPOSE 5050
ENTRYPOINT ["java", "-jar", "app.jar"]
