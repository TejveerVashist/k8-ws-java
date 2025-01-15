FROM maven:3.9.4-eclipse-temurin-21 AS builder

WORKDIR /app

COPY pom.xml ./
COPY src ./src

RUN mvn dependency:go-offline

RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre

WORKDIR /app

# Copy the built JAR file from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Expose the default application port
EXPOSE 8080

# Set the default command to run the application
CMD ["java", "-jar", "app.jar"]