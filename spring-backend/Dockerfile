FROM maven:3.8-openjdk-17-alpine AS builder
WORKDIR /app
COPY pom.xml ./
RUN mvn dependency:go-offline -B && rm -rf /root/.m2/repository
COPY src ./src
RUN mvn package -DskipTests

FROM openjdk:17-alpine
RUN addgroup -S appuser && adduser -S appuser -G appuser
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
ENV JAVA_OPTS=""
USER appuser
ENTRYPOINT ["sh","-c","java $JAVA_OPTS -jar app.jar"]

