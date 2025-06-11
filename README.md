# Midas
Project repo for the JPMC Advanced Software Engineering Forage program
> ## About Midas
>> This project is the backend core for a financial system, such as a bank or a trading platform. Its job is to receive and process transactions coming from other services in real time using Apache Kafka.
> ## Technology Stack
>> Spring Boot + Kafka
# Kafka Listener
> * Listens to incoming Kafka messages (each message = a transaction)
> * Deserializes those messages into Transaction objects
> * Prepares to process and store those transactions (the actual processing may come in later tasks)
> *  Spring Boot will auto-deserialize JSON messages to Transaction objects in the listener.
>> **@KafkaListener is an annotation in Spring Kafka that tells Spring Boot**: “This method should automatically listen to a Kafka topic and handle any messages received.” It turns a normal method into a Kafka consumer.
>> When your Spring Boot app starts:
>>> * @KafkaListener automatically connects to the specified Kafka topic.
>>> * waits for messages to arrive.
>>> * Whenever a message is published to the topic, it will: 1.Deserialize the message (e.g., to a Transaction object) 2.Call a method with the deserialized object as a parameter


> ###  The @KafkaListener annotation:
>> 1. topics: "${general.kafka-topic}" pulls the topic name from application.yml.
>> 2. groupId: Arbitrary name for your consumer group.

# File
  > * application.yml     -----     Main Spring Boot configuration file for Kafka settings and topic names
  > * TransactionKafkaListener.java     -----     I setted Kafka consumer that listens to the topic and receives transactions
  > * KafkaProducer.java     -----     Kafka producer that sends transaction data into the Kafka topic
  > * Transaction.java     -----     Java POJO that defines the structure of a transaction message
  > * TaskTwoTests.java     -----     Test class that sends mock transactions and waits for the Kafka listener to receive them
  >> **The relationship between files**: KafkaProducer → Send message → Kafka → TransactionKafkalistener → Receive and process message

## Note
> 1. add @Component before public class TransactionKafkaListener, Spring Boot’s default @ComponentScan in MidasCoreApplication will find your @Component here automatically
> 2. add a breakpoint before public void listen(Transaction transaction)
> 3. right click the Debug button on TaskTwoTests.java, and to see the amount result(Automatically jump out window)
