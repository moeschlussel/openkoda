# ---- Build Stage ----
FROM maven:3.8.7-eclipse-temurin-17 AS build
WORKDIR /app
COPY . .
RUN mvn -f openkoda/pom.xml clean package -DskipTests

# ---- Run Stage ----
FROM eclipse-temurin:17-jdk
WORKDIR /app
COPY docker/entrypoint.sh /app/
COPY --from=build /app/openkoda/target/openkoda*.jar application.jar
RUN chmod +x /app/entrypoint.sh
ENTRYPOINT ["/app/entrypoint.sh"]

