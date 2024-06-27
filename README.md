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

7. 


