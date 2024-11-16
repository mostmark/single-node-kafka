# Single Node Kafka cluster on OpenShift

Example of how to use an ephemeral single node Kafka 3.9 cluster on OpenShift. This can be deployed on the [Red Hat OpenShift Developer Sandbox](https://developers.redhat.com/developer-sandbox) environment for development and testing.

##   To deploy the Kafka instance

```
oc apply -f https://raw.githubusercontent.com/mostmark/single-node-kafka/main/kafka.yaml
```

## To test the kafka instance
    
Get the name of the pod:
```
oc get pods | grep kafka
```

Connect to the running pod:
```
oc rsh kafka-NNN-NNN
````


Create the topic my-topic:
```
bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --partitions 1 --replication-factor 1 --topic my-topic
```

Produce some messages on the topic:
```
bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic my-topic
```

Read the messages on the topic:
```
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --from-beginning --topic my-topic
```

List all topics:
```
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```

## To clean up
```
oc delete deployment kafka
oc delete service my-cluster-kafka-bootstrap
```
