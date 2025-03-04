
# Kafka connect image creation for elastic search and cloud object storage sinks and MQ source


## Get IBM MQ jars

```sh
git clone https://github.com/ibm-messaging/kafka-connect-mq-source
cd kafka-connect-mq-source
mvn clean package
mv target/kafka-connect-mq-source-*with-dependencies.jar ../my-plugins
```


## Get Cloud Object Storage jars


```sh
 git clone https://github.com/ibm-messaging/kafka-connect-ibmcos-sink
 cd kafka-connect-ibmcos-sink
 gradle shadowJar
 mv target/kafka-connect-elastic-sink-*with-dependencies.jar ../my-plugins
```

## Get Elastic Seach Sink connector

```sh
git clone https://github.com/ibm-messaging/kafka-connect-elastic-sink.git
cd kafka-connect-elastic-sink
mvn clean package
mv target/kafka-connect-elastic-sink-*with-dependencies.jar ../my-plugins
```

## Update the custom image

```sh
IMAGE_NAME=quay.io/ibmcase/eda-kconnect-cluster-image 
TAG=latest
docker build -t ${IMAGE_NAME}:${TAG} .
docker push ${IMAGE_NAME}:${TAG}
```

## Verify

```
docker run -ti  ${IMAGE_NAME}:${TAG}   bash -c "ls /opt/kafka/plugins"
```