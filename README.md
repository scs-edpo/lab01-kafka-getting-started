# lab01-kafka-getting-started

In this lab, you will install Kafka with Docker and verify that it is working by creating a topic and sending some messages.

This lab is adapted from [here](https://github.com/SciSpike/kafka-lab).

## Objectives

1. Install [Kafka](http://kafka.apache.org/) using [Docker](https://www.docker.com/products/overview)
2. Create a topic
3. Send some messages to the topic
4. Start a consumer and retrieve the messages

## Prerequisitesdoc

One of the easiest ways to get started with Kafka is through the use of [Docker](https://www.docker.com). 
If you do not already have a version of Docker installed on your computer: [install Docker by following the directions appropriate for your operating system.](https://www.docker.com/products/overview) 
Make sure that you can run both the `docker` and `docker compose` command from the terminal.

## Instructions

1. Open a terminal in this lab directory: `lab01-kafka-getting-started`.

2. Start the Kafka processe using Docker Compose:

  ```
  $ docker compose up
  ```

The first time you run this command, it will take a while to download the appropriate Docker images.

3. Open an additional terminal window in the lab directory, `lab01-kafka-getting-started`. We are going to create a topic called `helloworld` with a single partition and one replica:

  ```
  $ docker compose exec kafka kafka-topics --create --bootstrap-server 'kafka:9092' --replication-factor 1 --partitions 1 --topic 'helloworld'
  ```

4. You can now see the topic that was just created with the `--list` flag:

  ```
  $ docker compose exec kafka kafka-topics --list --bootstrap-server 'kafka:9092'
  helloworld
  ```

5. Normally you would use the Kafka API from within your application to produce messages but Kafka comes with a command line _producer_ client that can be used for testing purposes. Each line from standard input will be treated as a separate message. Type a few messages and leave the process running.

  ```
  $ docker compose exec kafka kafka-console-producer --bootstrap-server 'kafka:9092' --topic 'helloworld'
  Hello world!
  Welcome to Kafka.
  ```

6. Open another terminal window in the lab directory. In this window, we can use Kafka's command line _consumer_ that will output the messages to standard out.

  ```
  $ docker compose exec kafka kafka-console-consumer --bootstrap-server 'kafka:9092' --topic 'helloworld' --from-beginning
  Hello world!
  Welcome to Kafka.
  ```

7. In the _producer_ client terminal, type a few more messages that you should now see echoed in the _consumer_ terminal.

8. Stop the producer and consumer terminals by issuing a **Ctrl-C**.

9. Finally, stop Kafka server with Docker Compose:

  ```
  $ docker compose down
  ```

Congratulations, this lab is complete!

