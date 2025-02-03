# FROM docker.io/openjdk:8-jdk-alpine
# RUN addgroup -S spring && adduser -S spring -G spring
# USER spring:spring
# ARG DEPENDENCY=target/dependency
# COPY ${DEPENDENCY}/BOOT-INF/lib /app/lib
# COPY ${DEPENDENCY}/META-INF /app/META-INF
# COPY ${DEPENDENCY}/BOOT-INF/classes /app
# ENTRYPOINT ["java","-cp","app:app/lib/*","hello.Application"]


FROM docker.io/maven:3.9.9-amazoncorretto-17-alpine AS build
WORKDIR /app
RUN addgroup -S spring && adduser -S spring -G spring
USER root
ADD . .
RUN mvn -DskipTests clean package 

FROM docker.io/openjdk:17-jdk-alpine
COPY --from=build /app/target/*.jar /app/runner.jar
ENTRYPOINT ["java","-cp","app:app/lib/*","hello.Application"]
