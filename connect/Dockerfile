FROM confluentinc/cp-server-connect-base:6.1.0

ENV CONNECT_PLUGIN_PATH="/usr/share/java,/usr/share/confluent-hub-components"

ARG CONNECTOR_NAME
ARG CONNECTOR_VERSION
RUN confluent-hub install --no-prompt confluentinc/kafka-connect-replicator:6.1.0
