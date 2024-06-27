# Kafka-stock-market

Steps to get going:

1. Get a new AWS EC2 instance running, generate and download the key, and put that into a new folder.
2. Go to the terminal, go to the project folder, connect to it using the string from EC2 instance.

`ssh -i "key_kafka-stock-market-project.pem" ec2-user@ec2-18-191-237-197.us-east-2.compute.amazonaws.com`

> In this process, I need to do
> `chmod 400 path/of/the/certificate.pem`
> in order to give it enough permission.

3. Download Kafka into the EC2 instance.
   - **Do not download a source files from appache kafka, download a binary file**

`wget https://archive.apache.org/dist/kafka/3.7.0/kafka_2.12-3.7.0.tgz`

Unarchive it by `tar -xvf kafka_2.12-3.7.0.tgz`.

4. Download Java.

`sudo yum install java-22-amazon-corretto`

5. Get the zookeeper running. (ZooKeeper plays a crucial role in coordinating and managing the distributed environment. )

`cd kafka_2.12-3.7.0`

`bin/zookeeper-server-start.sh config/zookeeper.properties`

6. Now that the zookeeper is running in one terminal window, we now go to another new window. We first assign more memory to the EC2 server.

`export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"`

7. Run Kafka and change the IP address to public.

`cd kafka_2.12-3.7.0`

`bin/kafka-server-start.sh config/server.properties`

> The IP address right now is private as *ip-172-31-4-130.us-east-2.compute.internal/172.31.4.130:9092*, which we cannot access without being in the same address. So we need to make this IP address public so that we can access it.
> First we need to stop the two running windows.
> 
> `sudo nano config/server.properties` then find the block
> `# Listener name, hostname and port the broker will advertise to clients. # If not set, it uses the value for "listeners". advertised.listeners=PLAINTEXT://YOUR.IP.ADDRESS:9092`
>
> Change the *YOUR.IP.ADDRESS* to the Public IPv4 address you have on EC2.

- **When restarting the zookeeper and kafka, you may need to reopen a new window and start the EC2 instance again to perform the following instructions.**

8. Provide the EC2 security access from the local machine.
From the EC2 page, click `Security`, and `Edit inbound rules`. Add another rule there to make it *Allowing all traffic*, and it's advised to provide your own IP address there.

> Here we need to note this is mostly **NOT** the secure way to do things. But for practice purpose we are just allowing all traffic.

9. Create a topic. Go to another terminal window, and repeat all the necessary steps to start the EC2.

`cd kafka_2.12-3.7.0`

`bin/kafka-topics.sh --create --topic kafka_topic1 --bootstrap-server 18.191.237.197:9092 --replication-factor 1 --partitions 1`

10. Start Producer

`bin/kafka-console-producer.sh --topic kafka_topic1 --bootstrap-server 18.191.237.197:9092 `

Start Consumer:
-------------------------
Duplicate the session & enter in a new console --
cd kafka_2.12-3.3.1
bin/kafka-console-consumer.sh --topic demo_testing2 --bootstrap-server {Put the Public IP of your EC2 Instance:9092}


