1. Clone the repository </br> ```git clone https://github.com/kheekheekhee/OTOT-D.git```
2. Go into the root folder
3. Run the following commands
4. ```docker-compose up -d```
5. To create a topic "test" with 3 partitions </br> ```docker exec otot_d_kafka-1_1 kafka-topics --create --topic test --bootstrap-server localhost:19092 --replication-factor 3 --partitions 3```
6. To create a message producer </br> ```docker exec --interactive --tty otot_d_kafka-1_1 kafka-console-producer --bootstrap-server localhost:19092 localhost:29092 localhost:39092 --topic test```
7. Open a new terminal in the same directory and run the following command to create a message consumer that's subscribed to the topic "test" </br> ```docker exec --interactive --tty otot_d_kafka-1_1 kafka-console-consumer --bootstrap-server localhost:19092 --topic test --from-beginning```
8. Type messages in the terminal hosting the producer to publish messages into the topic "test" and see messages in the terminal hosting the consumer subscribed to the topic "test"
9.  To check the nodes currently in charge of each partition in the Kafka node otot_d_kafka-1_1 that's linked to the topic "test" </br> ```docker exec --interactive --tty otot_d_kafka-1_1 kafka-topics --describe --topic test --bootstrap-server localhost:19092``` </br> You will see that there are currently three distinct Kafka instances each taking care of one partition
10. To temporarily kill 1 Kafka node </br> ```docker restart otot_d_kafka-1_1``` </br> or click the restart button on Docker Desktop
11. Run </br> ```docker exec --interactive --tty otot_d_kafka-1_1 kafka-topics --describe --topic test --bootstrap-server localhost:19092``` </br> again to check the status of the topic "test"
12. Notice that there are now only two distinct Kafka nodes that are taking care of the three partitions, indicating that when one of the Kafka nodes failed, another node takes over as the master node in the partition that failed