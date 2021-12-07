FROM confluentinc/cp-server-connect-base:7.0.0

ENV CONNECT_PLUGIN_PATH="/usr/share/java,/usr/share/confluent-hub-components,/usr/share/filestream-connectors"

RUN confluent-hub install --no-prompt confluentinc/kafka-connect-replicator:7.0.0
