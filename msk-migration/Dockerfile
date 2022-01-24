FROM confluentinc/cp-server-connect-base:7.0.1
USER root
RUN confluent-hub install confluentinc/kafka-connect-replicator:7.0.1 --no-prompt
RUN cp /usr/share/confluent-hub-components/confluentinc-kafka-connect-replicator/lib/replicator-rest-extension-7.0.1.jar /usr/share/java/kafka/
USER appuser
