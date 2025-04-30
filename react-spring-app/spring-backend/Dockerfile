FROM maven:3.8-openjdk-17-slim AS build

WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests && \
    rm -rf ~/.m2/repository

FROM openjdk:17-slim

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

RUN adduser --system --group spring && \
    chown spring:spring /app

USER spring

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"] 