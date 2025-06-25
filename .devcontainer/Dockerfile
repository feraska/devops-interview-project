FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn clean package
FROM openjdk
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
