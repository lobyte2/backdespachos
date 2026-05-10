# Etapa 1: Build (Multi-stage) [cite: 36, 158]
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# Etapa 2: Runtime (Seguridad y Optimización) [cite: 39, 220]
FROM eclipse-temurin:17-jdk-jammy
WORKDIR /app

# Ejecución con usuario no root (Requisito IE1 / Seguridad) [cite: 37, 258]
RUN addgroup --system springuser && adduser --system springuser --ingroup springuser
USER springuser

COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]