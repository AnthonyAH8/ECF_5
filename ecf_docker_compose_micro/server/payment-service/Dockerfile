FROM maven:3.8.3-jdk-11 AS builder

WORKDIR /app

COPY pom.xml ./
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn package -DskipTests


FROM openjdk:11

WORKDIR /app

COPY --from=builder /app/target/payment-service.jar .

EXPOSE 9050

ENTRYPOINT ["java", "-jar", "payment-service.jar"]