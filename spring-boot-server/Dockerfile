# Étape 1 : Builder le jar avec Maven
FROM maven:3.9.3-eclipse-temurin-17 AS build
WORKDIR /app

# Copier pom.xml et télécharger les dépendances
COPY pom.xml .
RUN mvn dependency:go-offline

# Copier le reste du projet et builder le jar
COPY src ./src
RUN mvn clean package -DskipTests

# Étape 2 : Exécuter le jar avec OpenJDK 17
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
