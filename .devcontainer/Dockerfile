FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn -version && ls -l && ls -l target || true
# Print files to verify content
RUN ls -l && cat pom.xml || echo "No pom.xml"

# Run Maven with clean output
RUN mvn clean package -X || (echo "Build failed" && cat /app/target/*.log || true)
FROM openjdk
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 80
CMD ["java", "-jar", "app.jar"]
