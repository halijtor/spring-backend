FROM openjdk:17-alpine AS builder

RUN apk update && apk add --no-cache maven

WORKDIR /app
COPY pom.xml ./

RUN mvn dependency:go-offline -B

COPY src ./src

RUN mvn package -DskipTests \
 && rm -rf /root/.m2/repository /var/cache/apk/*

FROM openjdk:17-alpine

RUN addgroup -S appuser && adduser -S appuser -G appuser

WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar

ENV JAVA_OPTS=""

USER appuser
ENTRYPOINT ["sh","-c","java $JAVA_OPTS -jar app.jar"]
