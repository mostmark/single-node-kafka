# Single Node Kafka cluster on OpenShift

Example of how to use a single node Kafka 3.7 cluster on OpenShift using a Helm chart. This can be deployed on the [Red Hat OpenShift Developer Sandbox](https://developers.redhat.com/developer-sandbox) environment for development and testing.

    git clone https://github.com/mostmark/single-node-kafka.git && cd single-node-kafka

    # To install the helm chart
    helm install single-node ./

    # Connect to the running pod
    oc rsh single-node-kafka-0

    # Create the topic my-topic
    kafka-topics.sh --bootstrap-server single-node-kafka-0:9092 --create --partitions 1 --replication-factor 1 --topic my-topic

    # Produce some messages on the topic
    kafka-console-producer.sh --bootstrap-server single-node-kafka-0:9092 --topic my-topic
    
    # Read the messages on the topic
    kafka-console-consumer.sh --bootstrap-server single-node-kafka-0:9092 --from-beginning --topic my-topic

    # List all topics
    kafka-topics.sh --list --bootstrap-server single-node-kafka-0:9092

    # To clean up
    helm uninstall single-node
    oc delete pvc kafka-data-single-node-kafka-0
