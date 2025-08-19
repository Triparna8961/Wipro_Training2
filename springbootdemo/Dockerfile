ARG JDK_VERSION=17

# build stage uses the selected JDK version
FROM maven:3.9.0-eclipse-temurin-${JDK_VERSION} AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# runtime stage uses matching JRE
FROM eclipse-temurin:${JDK_VERSION}-jre-jammy
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
CMD ["java", "-jar", "app.jar"]
