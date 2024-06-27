# Kafka-stock-market

Steps to get going:

1. Get a new AWS EC2 instance running, generate and download the key, and put that into a new folder.
2. Go to the terminal, go to the project folder, connect to it using the string from EC2 instance.

`ssh -i "key_kafka-stock-market-project.pem" ec2-user@ec2-18-191-237-197.us-east-2.compute.amazonaws.com`

> In this process, I need to do
> `chmod 400 path/of/the/certificate.pem`
> in order to give it enough permission.

3. Download Kafka into the EC2 instance.

`wget https://archive.apache.org/dist/kafka/3.7.0/kafka-3.7.0-src.tgz`

4. Download Java.

`sudo yum install java-22-amazon-corretto`

5. 

