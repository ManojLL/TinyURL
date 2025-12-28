ARG GRADLE_VERSION=9.2.1
ARG JAVA_VERSION=21

FROM gradle:${GRADLE_VERSION}-jdk${JAVA_VERSION} AS builder
WORKDIR /workspace
COPY TiNyUrlService .
RUN gradle clean build --no-daemon

FROM gcr.io/distroless/java${JAVA_VERSION}-debian12 AS runner
WORKDIR /app
COPY --from=builder /workspace/build/libs/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]