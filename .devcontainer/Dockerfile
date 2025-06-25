FROM maven:3.9.4-eclipse-temurin-17 AS build
WORKDIR /app

# Copy pom.xml separately for caching
COPY pom.xml .

# Copy src and other resources (excluding .git if you want)
COPY src ./src
COPY mvnw .
COPY .mvn .mvn
# Run build skipping git plugin and tests
RUN ./mvnw clean package 

FROM openjdk:17-jdk-slim
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
