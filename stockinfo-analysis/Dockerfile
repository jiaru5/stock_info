FROM openjdk:17-jdk-slim
VOLUME /tmp
COPY target/stockinfo-analysis-*.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"] 