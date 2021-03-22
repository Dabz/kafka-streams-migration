# Kafka Streams migration example using Replicator

## Key points

- Replicator must be configured with `isolation.level=read_committed`
- Data must be extracted from the topics `connect-configs` and `connect-offsets` in order to migrate connectors

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

[![Process](./images/process.png)](http://www.plantuml.com/plantuml/uml/bLCzRzj03DtrAuXCyP8Vu21eYYvTsg6PEXNi7MsnEHq5acV1AFBV6-aYvAoWWsym33v-lFT8FPgZUXbIPy-SHrGSeCSS9sLtok1Qg86inoWJvsC5bkBk5N9sbWmtJouZ1CcPWelUmDyENj_Uvl2e4aiWjVicQ58qq7l92WOPpnz1C4UdcfB5QGzMGWzey2V-3jtB9HKb7037CN709MPzyIXJNdbDFIU2syzDobSqI7Zyj0CskFr9jkjWUVi9sUjaol6jyhlisaPFd9zNjj1VtQbnfMcqU7AXx1iVjR9T_BSgfrOsMkwN87aP0NEikV23AYuwmzN3YRq7DabBsLsY4wK79Oo_WWm3EyLMv7k7wytQRcZ-duyNEv8CNvAKsDmEgczrhSe-dCWRA2TIvKWhBeU3aLj56zMZqecbM3g3uOaYS3v8C_U_zxdrTRknxQ1Au4vf_XqbSJW_97GoRwQrdyXBD--pUwGSov3-0G00)

## How to run the example

```sh
export CCLOUD_CLUSTER=pkc-xxxx.europe-west1.gcp.confluent.cloud:9092
export CLUSTER_API_KEY=XXXXX
export CLUSTER_API_SECRET=XXXXX

# Start the local environment, the connectors and Kafka Streams
./up
echo "toto tata" >> data/source.txt
sleep 10
cat data/sink.txt

# Migrate Kafka Streams and connectors to Confluent Cloud
./migrate
echo "toto tata" >> data/source.txt
sleep 10
cat data/sink.txt
````

