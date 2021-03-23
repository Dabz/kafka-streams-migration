# Kafka Streams migration example using Replicator

## Key points

- Replicator must be configured with `isolation.level=read_committed`
- Data must be extracted from the topics `connect-configs` and `connect-offsets` in order to migrate connectors
- Migrated application need to be restarted with `auto.offset.reset=latest`

## Process

* On the source cluster:
  * Stop Producers
  * Stop Connectors
  * Stop Kafka Streams
  * Wait for each topology to clear up lag.
  * Copy Kafka Connect source connector offset json payloads
* Migration start:
  * Start Replicator with `isolation.level=read_committed`
  * Wait for replicator to catch up
* Start application on the destination cluster
  * Setup connectors
  * Write source connect offset json playloads
  * Start connector
  * Start producers

[![Process](./images/process.png)](http://www.plantuml.com/plantuml/uml/dLF1Rjim3BtxAuYUcai_84Mn3jrXbst0SXXs6ZIBYRdAea1I2O9X_pxLib75mGwhOHW67_dq7aazgZcnF8PEdoac9sw4mKL_4ZB322OP6qW7v_b4yL21Rghk2cPan15kTiO9UeuHUsEvWTyTb6SxXPEmppsAtZT1vImzlfOiu1EdypK8QiwmfaGstC8kzmCuXL_-Pz_zwIwr21RDBgL0lPjYEcGh1k8Yx3HGGBXztwHyB6J17TvjW1HklwDkIkOawPiZgqTZz7FbPzwqH3kApujS6Dx2jBIb4BLDMLdxH0UfSgS9QFLJInipzrCGBITmqTTS-8eLPodmtCKJsG2a7AQoku1730-2pl_eUHp9qBSkNndUrAtj1mne2D88MK_kvJyUBcPNtgV0sJTBLRBMTYySyNwlQ7U2Bz_49U_yK2oYsio0bgzNSDx0BqSK8OyBNidqwf0aU2JE6iwWxeWUAEwvKVZF5LyFPZtp_tOpiJIth3IrK-FKFMBqUGn_0G00)

## How to run the example

```sh
export CCLOUD_CLUSTER=XXXXX.confluent.cloud:9092
export CLUSTER_API_KEY=XXXXX
export CLUSTER_API_SECRET=XXXXX

# Start the local environment, the connectors and Kafka Streams
./up

# Migrate Kafka Streams and connectors to Confluent Cloud
./migrate
echo "World" >> data/source.txt
sleep 10
cat data/sink.txt
````

