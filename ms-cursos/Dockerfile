FROM openjdk:17-jdk-alpine as builder

WORKDIR /app/ms-cursos

COPY ./pom.xml /app
COPY ./ms-cursos/.mvn ./.mvn
COPY ./ms-cursos/mvnw .
COPY ./ms-cursos/pom.xml .

RUN ./mvnw clean package -Dmaven.test.skip -Dmaven.main.skip -Dspring-boot.repackage.skip && rm -r ./target/

COPY ./ms-cursos/src ./src

RUN ./mvnw clean package -DskipTests

FROM openjdk:17-jdk-alpine

WORKDIR /app

COPY --from=builder /app/ms-cursos/target/ms-cursos-0.0.1-SNAPSHOT.jar .
EXPOSE 8002

ENTRYPOINT ["java", "-jar", "ms-cursos-0.0.1-SNAPSHOT.jar"]