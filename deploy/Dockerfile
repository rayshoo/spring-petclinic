FROM gradle:8.14.3-jdk17 AS builder
WORKDIR /app
COPY build.gradle settings.gradle ./
RUN gradle build --parallel --continue > /dev/null 2>&1 || true
COPY . .
RUN gradle build --parallel

FROM eclipse-temurin:17-ubi9-minimal
WORKDIR /app
COPY --from=builder /app/build/libs/app.jar .
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Duser.country=KR","-Duser.language=ko","-jar","/app/app.jar"]