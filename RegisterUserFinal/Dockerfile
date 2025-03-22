#Etapa de construção
#FROM maven:3.9.6-openjdk-21 AS build
#FROM ubuntu:latest AS build
FROM maven:3.9.6-eclipse-temurin-21 AS build
#RUN apt-get update && apt-get-install -y maven && apt-get clean && rm -rf/var/lib/lists/*

#Definir o diretorio dentro do container para a aplicação
WORKDIR /app

#Copiar o pom.xml para o container
COPY RegisterUserFinal/pom.xml /app/
COPY RegisterUserFinal/src/ /app/src/

#Executar o Maven para compilar o projeto e gerar o JAR File
RUN mvn clean package -DskipTests

#Etapa de execução
FROM openjdk:21-slim

#Definir o diretório de trabalho para a aplicação
WORKDIR /app

#Copiar o JAR construído na etapa anterior
COPY --from=build /app/target/app-1.jar app.jar

#Definir a porta que será utilizada na aplicação
EXPOSE 8188

#Comando para executar a aplicação
ENTRYPOINT [ "java", "-jar", "app.jar" ]