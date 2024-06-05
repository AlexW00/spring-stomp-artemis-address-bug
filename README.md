# Bug reproduction for Artemis queue not being removed

## Requirements

Java 17+ and Maven.

## How to run and observe

1. `docker-compose up` to start the Artemis instance.
2. `mvn spring-boot:run` to start the Spring Boot application (or using play button in IntelliJ)
3. Open browser at [localhost:9123](http://localhost:9123)
4. Click Connect & Send a message & See the delivered message
5. Close the browser tab
6. Check the artemis queues: `docker exec -it artemis bash -c "./broker/bin/artemis address show"`
7. This produces the bug state:
  - The address `/topic/greetings` will still be there and not get removed...
  - even tho the broker is configured to clean it up (see [broker.xml](./broker.xml))
  - This problem also exists when using user queues...
  - which can lead to a great number of queues being created and never removed.
