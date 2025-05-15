## a. How much data does the publisher program send to the message broker in one run?**  
In one run, the publisher calls `publish_event` five times. Each call sends one AMQP message, totaling **5 messages**. Each message contains a Borsh-serialized `UserCreatedEventMessage`, which includes fields such as user ID, name, and email. While the exact size depends on the content and serialization, the message count is consistently five per run.

## b. What does the URL `amqp://guest:guest@localhost:5672` mean, and why is it the same in both publisher and subscriber programs?**  
This URL is the AMQP connection string used to access the RabbitMQ broker:

- `amqp://` — specifies the protocol (AMQP)
- `guest:guest` — username and password (default credentials)
- `localhost` — the broker is hosted on the local machine
- `5672` — the default TCP port for AMQP

By using the same URL in both the publisher and subscriber programs, both are connecting to the same RabbitMQ instance. This allows the publisher to send messages into exchanges/queues on the broker, and the subscriber to consume those messages from the same location.


<img width="1280" alt="running_rabbitmq" src="https://github.com/user-attachments/assets/9f7a7888-223b-4dcc-a556-f98842f9785e" />