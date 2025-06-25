FROM eclipse-temurin:11-jdk AS build
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

FROM oraclelinux:9-slim
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
