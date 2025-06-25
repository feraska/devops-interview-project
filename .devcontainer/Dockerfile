FROM maven AS build
WORKDIR /app

# Copy pom.xml first to leverage Docker layer caching
COPY pom.xml .

# Copy the rest of the project files
COPY . .

# Optional: verify POM exists
RUN ls -l /app/pom.xml

# Skip git plugin to avoid .git directory issues
RUN mvn clean package -Dgit-commit-id.skip=true -DskipTests

FROM openjdk
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
