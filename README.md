# Spring Micro Services Application can be designed under various approaches.
1) Built as isolated services and calling them using .
2) Separating the internal services using CQRS design pattern.
3) Developing all the services using modular approach.

### Objective of the Project:
### Live Streaming of tweets into kafka server using Twitter4j Library and building a docker
    container using spring-boot-maven plugin. 
Once the data is  sent tp Kafka docker setup  entire results of the application
is wrapped inside the docker containers using kafka-spring-boot maven plugin.
-As everyone face issues in setting up with developer account, so even application got
implemented MockKafkaService which simulates the behaviour of real time streaming.

### Project has following modules.
1) app-config-data : This module is exclusively to handle the configuration that are used
across the project.
KafkaConfiguration:  
KafkaAdminConfiguration:
KafKaProducerConfiguration:   

2) common-config: As we are using Kafka as it being an independent system, we need to 
make sure that we are making enough number of attempts while creating the Topics or
before declaring the broker is down.
To perform the retry logic we are using common-config.


# Running the application

- Please enter the correct credentials in twitter4j.properties file.
- Then go to docker-compose folder and run docker-compose up command to run local kafka cluster
- Then run TwitterToKafkaServiceApplication inside IntelliJ, or run with mvn spring-boot:run command
- Check the new TwitterStatusToAvroTransformer and updated TwitterKafkaStatusListener classes, where we implemented the part 
that transforms twitter status object to kafka compatible avro object and send the message to kafka using producer  
- Check the StreamInitializer and KafkaStreamInitializer in twitter-to-kafka-service, where we added initializing logic for kafka cluster
and then used this initializer in the TwitterToKafkaServiceApplication prior to starting streaming data
  
- We be using Spring-boot-maven-plugin at the end to generate a docker image.
- <goal>build-image</goal> is responsible for creating the docker image.
- When we run mvn install , it tries to load the context and execute the tests if exists.
- Use mvn run skip tests
- Spring-boot follows a layered approach
- Prevents creating a single fat jar
- if there is update there is no need of updating the complete jar as it uses caching internally.
  With the help of cloud native build packs - buildpacks.io
- docker is build in layered fashion, and layer is designed to change the code.
     
