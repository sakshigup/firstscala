#### Getting started
To get started make sure you have sbt installed on your system.

#### Prerequisites
* Kafka.

* Apache Cassandra.
  
#### For running the Trailblazer application:

* Start the Zookeeper server.

* Start the Kafka brokers.

* Start Cassandra DB.

* Create a topic.
```
> bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic <TopicName>
```

**TopicName:** Provide the name of the topic you want to create.  
* Start a console producer
```
> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <TopicName>
```

* Produce some messages, the format should be like below:
```
> { "device-id": <String>, "timestamp": <String>, "temperature": <Double> }
```
  
#### Example:
```
> { "device-id": "Device11", "timestamp": "2018-08-31T21:33:56Z", "temperature": 40.2 }
```

* Export all the required environment variables explicitly.

To view list of environment variables: [ENVIRONMENT VARIABLES](https://github.com/KnoldusLabs/TrailBlazer/wiki)

* Start the application using the following command:
```
sbt runAll
```
This will compile and run all your files and starts the services.


#### To enter data manually, invoke the route through POSTMAN and make a POST call.
```
http://localhost:9000/api/temperatureData
```

#### Example:
```.env
{"deviceId":"Device100", "timestamp":"2014-02-20T12:33:40Z", "temperature":87}
```
This will persist your data manually in the database.

* To get the data, invoke the route by providing the start timestamp or end timestamp or device id or any combinations of all three:
```
http://localhost:9000/api/temperatureData?startTs&endTs&deviceId
```
  
#### Example:
```
http://localhost:9000/api/temperatureData?startTs=1422867820000&endTs=1550702020000
```  

```
http://localhost:9000/api/temperatureData?deviceId=device123
```  

```
http://localhost:9000/api/temperatureData?startTs=1422867820000&endTs=1550702020000&deviceId=device123
```  

#### Sample Response
```
  {
    "device-id": "Device11",
    "timestamp": "2018-08-31T21:33:56Z",
    "temperature": 27.2
  }
```

* Different quality tools and plugins are added in the application for better performance.

To view the use of these plugins and how to use them: [QUALITY TOOLS AND PLUGINS](https://github.com/KnoldusLabs/TrailBlazer/wiki)
