FROM maven:3.6.3-jdk-8
COPY ./ ./
RUN mvn clean package
CMD ["java", "-javaagent:/tmp/prometheus/jmx_prometheus_javaagent-0.15.0.jar=2112:/tmp/prometheus/kafka-streams-prometheus.yaml", "-jar", "target/kafka-streams-app-1.0-SNAPSHOT-jar-with-dependencies.jar", "/tmp/conf.properties"]
