# syntax=docker/dockerfile:1

# --- Build Stage ---
FROM eclipse-temurin:17-jdk AS build
WORKDIR /app

# Copy Maven wrapper and config first for caching
COPY --link pom.xml mvnw ./
COPY --link .mvn .mvn/

# Download dependencies (leverage Docker cache)
RUN chmod +x mvnw && ./mvnw dependency:go-offline

# Copy source code
COPY --link src ./src/

# Build the application (skip tests for faster build)
RUN ./mvnw package -DskipTests

# --- Runtime Stage ---
FROM eclipse-temurin:17-jre
WORKDIR /app

# Create non-root user for security
RUN useradd -m appuser
USER appuser

# Copy built jar from build stage
COPY --from=build /app/target/*.jar /app/app.jar

# Expose default Spring Boot port
EXPOSE 8080

# JVM container-aware flags for memory/resource management
ENV JAVA_OPTS="-XX:MaxRAMPercentage=80.0"

# Use exec form for proper signal handling
ENTRYPOINT ["sh", "-c", "exec java $JAVA_OPTS -jar /app/app.jar"]
