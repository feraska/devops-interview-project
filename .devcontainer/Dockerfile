FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn -version
RUN ls -l
RUN whoami
RUN mvn clean package -DskipTests

FROM openjdk
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
