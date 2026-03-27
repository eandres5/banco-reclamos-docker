FROM eclipse-temurin:21-jre-alpine

RUN apk add --no-cache curl

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

WORKDIR /app

COPY api-reclamos-service-1.0.0.war app.war

COPY application.properties application.properties

USER appuser

EXPOSE 8080

ENTRYPOINT ["java", \
  "-jar", "app.war", \
  "--spring.config.location=file:./application.properties", \
  "-Djava.security.egd=file:/dev/./urandom"]