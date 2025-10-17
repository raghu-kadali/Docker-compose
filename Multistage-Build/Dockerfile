FROM maven:latest AS builder
RUN apt update -y
RUN apt install git -y
WORKDIR /app
RUN git clone https://github.com/spring-projects/spring-petclinic.git 
RUN cd /app/spring-petclinic && mvn clean package -DskipTests

FROM openjdk:25-jdk
WORKDIR /app2
COPY --from=builder /app/spring-petclinic/target/*.jar  /app2/sai.jar
EXPOSE 8080
CMD [ "java","-jar","/app2/sai.jar" ]




# ---------- Builder Stage ----------
FROM eclipse-temurin:25-jdk AS builder

# Install required tools
RUN apt-get update && apt-get install -y git maven

# Clone and build the Spring Petclinic project
WORKDIR /sai
RUN git clone https://github.com/spring-projects/spring-petclinic.git
WORKDIR /sai/spring-petclinic
RUN mvn clean package -DskipTests

# ---------- Runtime Stage ----------
FROM eclipse-temurin:25-jdk

WORKDIR /app2
COPY --from=builder /sai/spring-petclinic/target/*.jar /app2/sai.jar

EXPOSE 8080
CMD ["java", "-jar", "/app2/sai.jar"]




# FROM ubuntu:18.04 AS builder
# RUN apt update -y
# RUN apt install git -y
# RUN apt install maven -y
# WORKDIR /sai
# RUN git clone https://github.com/spring-projects/spring-petclinic.git 
# RUN cd /sai/spring-petclinic && mvn clean package -DskipTests

# FROM openjdk:21-jdk
# WORKDIR /app2
# COPY --from=builder /sai/spring-petclinic/target/*.jar  /app2/sai.jar
# EXPOSE 8080
# CMD [ "java","-jar","/app2/sai.jar" ]

