# 1) build stage
FROM maven:3.8.1-openjdk-17-slim AS builder
WORKDIR /app
COPY pom.xml ./
COPY src ./src
RUN mvn package -DskipTests

# 2) runtime stage
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]

