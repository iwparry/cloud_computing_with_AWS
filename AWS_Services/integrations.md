# Cloud Integrations
When we be begin to deploy multiple applications, we would like them to eventually communicate with one another.

The two patterns of application communication are:
1. Synchronous communications (application to application)
2. Asynchronous/Event based (application to queue to application)

Note synchronous communication between applications can be problematic if there are sudden spikes of traffic, in which case it's better to decouple your applications, and there are few ways we can do this in AWS.

## Amazon SQS (Simple Queue Service)
SQS is a fully managed service and is used to decouple applications and is able to scale seamlessly. By default the queue retains messages for 4 days, there is no limit on how many messages can be in a queue, and messages are deleted after they're read by consumers. It is able to perform with low latency and consumers share the work to read messages and scale horizontally.

## Amazon Kinesis
Amazon Kinesis is a managed service for processing big data in real time. You can use Kinesis data streams to collect and process large streams of data records in real time.

## Amazon SNS (Simple Notification Service)
SNS is a managed service that provides message deliver from publishers to subscribers. Publishers communicate asynchronously with subscribers by sending messages to a topic, which is a logical access point and communication channel.

## Amazon MQ
Amazon MQ is a managed message broker service for Apache ActiveMQ and RabbitMQ that streamlines setup, operation, and management of message brokers on AWS. ActiveMQ and RabbitMQ are on-premises technologies that provide you access to open protocols such as MQTT, ZMQP, STOMP, Openwire, WSS. When migrating to the cloud, instead of re-engineering the application to use SQS and SNS, you can use Amazon MQ.