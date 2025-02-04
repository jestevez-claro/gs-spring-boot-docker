FROM docker.io/maven:3.9.9-amazoncorretto-17-alpine AS build
WORKDIR /app
RUN addgroup -S spring && adduser -S spring -G spring
USER root
ADD . .
RUN mvn -DskipTests clean package 

# FROM docker.io/openjdk:17-jdk-alpine
# COPY --from=build /app/target/*.jar /app/runner.jar
# CMD ["java", "-jar", "/app/runner.jar"]

FROM nexus.dev.cloudapps.claro.com.do:8450/ubi8/openjdk-8
COPY --from=build /app/target/*.jar /app/runner.jar
CMD ["java", "-jar", "/app/runner.jar"]
